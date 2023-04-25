# Payment Backupdate

Once payment is done the application status has to be updated. Since we have a microservice architecture the two services can communicate with each other either through API calls or using message queues(kafka in our case). To avoid any service specific code in collection service we use the second approach to notify the service of payment for its application. Whenever a payment is done the collection service will publish the payment details on a kafka topic. Any microservice which wants to get notified when payments are done can subscribe to this topic. Once the service consumes the payment message it will check if the payment is done for its service by checking the businessService code. If it is done for the given service it will update the application status to PAID or will trigger workflow action PAY depending on the use case.

For our guide, we will follow the following steps to create payment backupdate consumer -

i) Create a consumer class by the name of PaymentBackUpdateConsumer. Annotate it with @Component annotation and add the following content to it -

```java
package digit.kafka;

import digit.service.PaymentUpdateService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.kafka.annotation.KafkaListener;
import org.springframework.kafka.support.KafkaHeaders;
import org.springframework.messaging.handler.annotation.Header;
import org.springframework.stereotype.Component;

import java.util.HashMap;

@Component
public class PaymentBackUpdateConsumer {

    @Autowired
    private PaymentUpdateService paymentUpdateService;

    @KafkaListener(topics = {"${kafka.topics.receipt.create}"})
    public void listenPayments(final HashMap<String, Object> record, @Header(KafkaHeaders.RECEIVED_TOPIC) String topic) {
        paymentUpdateService.process(record);
    }
}

```

ii) Next, under service folder create a new class by the name of PaymentUpdateService and annotate it with @Service. Put the following content in this class -

```java
package digit.service;

import com.fasterxml.jackson.databind.ObjectMapper;
import digit.repository.BirthRegistrationRepository;
import digit.web.models.*;
import lombok.extern.slf4j.Slf4j;
import org.egov.common.contract.request.RequestInfo;
import org.egov.common.contract.request.Role;
import org.egov.tracer.model.CustomException;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.util.CollectionUtils;

import java.util.Collections;
import java.util.HashMap;
import java.util.List;

@Slf4j
@Service
public class PaymentUpdateService {

    @Autowired
    private WorkflowService workflowService;

    @Autowired
    private ObjectMapper mapper;

    @Autowired
    private BirthRegistrationRepository repository;

    public void process(HashMap<String, Object> record) {

        try {

            PaymentRequest paymentRequest = mapper.convertValue(record, PaymentRequest.class);
            RequestInfo requestInfo = paymentRequest.getRequestInfo();

            List<PaymentDetail> paymentDetails = paymentRequest.getPayment().getPaymentDetails();
            String tenantId = paymentRequest.getPayment().getTenantId();

            for (PaymentDetail paymentDetail : paymentDetails) {
                updateWorkflowForBirthRegistrationPayment(requestInfo, tenantId, paymentDetail);
            }
        } catch (Exception e) {
            log.error("KAFKA_PROCESS_ERROR:", e);
        }

    }

    private void updateWorkflowForBirthRegistrationPayment(RequestInfo requestInfo, String tenantId, PaymentDetail paymentDetail) {

        Bill bill  = paymentDetail.getBill();

        BirthApplicationSearchCriteria criteria = BirthApplicationSearchCriteria.builder()
                .applicationNumber(bill.getConsumerCode())
                .tenantId(tenantId)
                .build();

        List<BirthRegistrationApplication> birthRegistrationApplicationList = repository.getApplications(criteria);

        if (CollectionUtils.isEmpty(birthRegistrationApplicationList))
            throw new CustomException("INVALID RECEIPT",
                    "No applications found for the consumerCode " + criteria.getApplicationNumber());

        Role role = Role.builder().code("SYSTEM_PAYMENT").tenantId(tenantId).build();
        requestInfo.getUserInfo().getRoles().add(role);

        birthRegistrationApplicationList.forEach( application -> {

            BirthRegistrationRequest updateRequest = BirthRegistrationRequest.builder().requestInfo(requestInfo)
                    .birthRegistrationApplications(Collections.singletonList(application)).build();

            ProcessInstanceRequest wfRequest = workflowService.getProcessInstanceForBirthRegistrationPayment(updateRequest);

            State state = workflowService.callWorkFlow(wfRequest);

        });
    }

}

```

iii) Create the following POJOs under models folder:

PaymentRequest.java

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
import org.egov.common.contract.request.RequestInfo;

import javax.validation.Valid;
import javax.validation.constraints.NotNull;


@Data
@NoArgsConstructor
@AllArgsConstructor
public class PaymentRequest {

    @NotNull
    @Valid
    @JsonProperty("RequestInfo")
    private RequestInfo requestInfo;

    @NotNull
    @Valid
    @JsonProperty("Payment")
    private Payment payment;

}
```

Payment.java

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import com.fasterxml.jackson.databind.JsonNode;
import lombok.*;

import javax.validation.Valid;
import javax.validation.constraints.NotNull;
import javax.validation.constraints.Size;
import java.math.BigDecimal;
import java.util.ArrayList;
import java.util.List;

@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
@EqualsAndHashCode
public class Payment {

    @Size(max = 64)
    @JsonProperty("id")
    private String id;

    @NotNull
    @Size(max = 64)
    @JsonProperty("tenantId")
    private String tenantId;

    @JsonProperty("totalDue")
    private BigDecimal totalDue;

    @NotNull
    @JsonProperty("totalAmountPaid")
    private BigDecimal totalAmountPaid;

    @Size(max = 128)
    @JsonProperty("transactionNumber")
    private String transactionNumber;

    @JsonProperty("transactionDate")
    private Long transactionDate;

    @NotNull
    @JsonProperty("paymentMode")
    private String paymentMode;

    @JsonProperty("instrumentDate")
    private Long instrumentDate;

    @Size(max = 128)
    @JsonProperty("instrumentNumber")
    private String instrumentNumber;

    @JsonProperty("instrumentStatus")
    private String instrumentStatus;

    @Size(max = 64)
    @JsonProperty("ifscCode")
    private String ifscCode;

    @JsonProperty("auditDetails")
    private AuditDetails auditDetails;

    @JsonProperty("additionalDetails")
    private JsonNode additionalDetails;

    @JsonProperty("paymentDetails")
    @Valid
    private List<PaymentDetail> paymentDetails;

    @Size(max = 128)
    @NotNull
    @JsonProperty("paidBy")
    private String paidBy;

    @Size(max = 64)
    @NotNull
    @JsonProperty("mobileNumber")
    private String mobileNumber;

    @Size(max = 128)
    @JsonProperty("payerName")
    private String payerName;

    @Size(max = 1024)
    @JsonProperty("payerAddress")
    private String payerAddress;

    @Size(max = 64)
    @JsonProperty("payerEmail")
    private String payerEmail;

    @Size(max = 64)
    @JsonProperty("payerId")
    private String payerId;

    @JsonProperty("paymentStatus")
    private String paymentStatus;

    public Payment addpaymentDetailsItem(PaymentDetail paymentDetail) {
        if (this.paymentDetails == null) {
            this.paymentDetails = new ArrayList<>();
        }
        this.paymentDetails.add(paymentDetail);
        return this;
    }

}

```

PaymentDetail.java

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import com.fasterxml.jackson.databind.JsonNode;
import lombok.*;

import javax.validation.constraints.NotNull;
import javax.validation.constraints.Size;
import java.math.BigDecimal;

@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
@EqualsAndHashCode
public class PaymentDetail {

    @Size(max = 64)
    @JsonProperty("id")
    private String id;

    @Size(max = 64)
    @JsonProperty("tenantId")
    private String tenantId;

    @JsonProperty("totalDue")
    private BigDecimal totalDue;

    @NotNull
    @JsonProperty("totalAmountPaid")
    private BigDecimal totalAmountPaid;

    @Size(max = 64)
    @JsonProperty("receiptNumber")
    private String receiptNumber;

    @Size(max = 64)
    @JsonProperty("manualReceiptNumber")
    private String manualReceiptNumber;

    @JsonProperty("manualReceiptDate")
    private Long manualReceiptDate;

    @JsonProperty("receiptDate")
    private Long receiptDate;

    @JsonProperty("receiptType")
    private String receiptType;

    @JsonProperty("businessService")
    private String businessService;

    @NotNull
    @Size(max = 64)
    @JsonProperty("billId")
    private String billId;

    @JsonProperty("bill")
    private Bill bill;

    @JsonProperty("additionalDetails")
    private JsonNode additionalDetails;

    @JsonProperty("auditDetails")
    private AuditDetails auditDetails;

}

```

Bill.java

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonCreator;
import com.fasterxml.jackson.annotation.JsonProperty;
import com.fasterxml.jackson.annotation.JsonValue;
import com.fasterxml.jackson.databind.JsonNode;
import lombok.*;
import org.springframework.util.CollectionUtils;

import javax.validation.Valid;
import java.math.BigDecimal;
import java.util.ArrayList;
import java.util.List;

@Getter
@Setter
@ToString
@Builder
@NoArgsConstructor
@AllArgsConstructor
@EqualsAndHashCode
public class Bill {

    @JsonProperty("id")
    private String id;

    @JsonProperty("mobileNumber")
    private String mobileNumber;

    @JsonProperty("paidBy")
    private String paidBy;

    @JsonProperty("payerName")
    private String payerName;

    @JsonProperty("payerAddress")
    private String payerAddress;

    @JsonProperty("payerEmail")
    private String payerEmail;

    @JsonProperty("payerId")
    private String payerId;

    @JsonProperty("status")
    private StatusEnum status;

    @JsonProperty("reasonForCancellation")
    private String reasonForCancellation;

    @JsonProperty("isCancelled")
    private Boolean isCancelled;

    @JsonProperty("additionalDetails")
    private JsonNode additionalDetails;

    @JsonProperty("billDetails")
    @Valid
    private List<BillDetail> billDetails;

    @JsonProperty("tenantId")
    private String tenantId;

    @JsonProperty("auditDetails")
    private AuditDetails auditDetails;

    @JsonProperty("collectionModesNotAllowed")
    private List<String> collectionModesNotAllowed;

    @JsonProperty("partPaymentAllowed")
    private Boolean partPaymentAllowed;

    @JsonProperty("isAdvanceAllowed")
    private Boolean isAdvanceAllowed;

    @JsonProperty("minimumAmountToBePaid")
    private BigDecimal minimumAmountToBePaid;

    @JsonProperty("businessService")
    private String businessService;

    @JsonProperty("totalAmount")
    private BigDecimal totalAmount;

    @JsonProperty("consumerCode")
    private String consumerCode;

    @JsonProperty("billNumber")
    private String billNumber;

    @JsonProperty("billDate")
    private Long billDate;

    @JsonProperty("amountPaid")
    private BigDecimal amountPaid;



    public enum StatusEnum {
        ACTIVE("ACTIVE"),

        CANCELLED("CANCELLED"),

        PAID("PAID"),

        EXPIRED("EXPIRED");

        private String value;

        StatusEnum(String value) {
            this.value = value;
        }


        @Override
        @JsonValue
        public String toString() {
            return String.valueOf(value);
        }

        public static boolean contains(String test) {
            for (StatusEnum val : StatusEnum.values()) {
                if (val.name().equalsIgnoreCase(test)) {
                    return true;
                }
            }
            return false;
        }

        @JsonCreator
        public static StatusEnum fromValue(String text) {
            for (StatusEnum b : StatusEnum.values()) {
                if (String.valueOf(b.value).equals(text)) {
                    return b;
                }
            }
            return null;
        }

    }

    public Boolean addBillDetail(BillDetail billDetail) {

        if (CollectionUtils.isEmpty(billDetails)) {

            billDetails = new ArrayList<>();
            return billDetails.add(billDetail);
        } else {

            if (!billDetails.contains(billDetail))
                return billDetails.add(billDetail);
            else
                return false;
        }
    }


}

```

BillDetail.java

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import com.fasterxml.jackson.databind.JsonNode;
import lombok.*;
import org.springframework.util.CollectionUtils;

import javax.validation.constraints.NotNull;
import java.math.BigDecimal;
import java.util.ArrayList;
import java.util.List;

@Setter
@Getter
@ToString
@Builder
@NoArgsConstructor
@AllArgsConstructor
@EqualsAndHashCode(of = { "id" })
public class BillDetail {

    @JsonProperty("id")
    private String id;

    @JsonProperty("tenantId")
    private String tenantId;

    @JsonProperty("demandId")
    private String demandId;

    @JsonProperty("billId")
    private String billId;

    @JsonProperty("amount")
    @NotNull
    private BigDecimal amount;

    @JsonProperty("amountPaid")
    private BigDecimal amountPaid;

    @NotNull
    @JsonProperty("fromPeriod")
    private Long fromPeriod;

    @NotNull
    @JsonProperty("toPeriod")
    private Long toPeriod;

    @JsonProperty("additionalDetails")
    private JsonNode additionalDetails;

    @JsonProperty("channel")
    private String channel;

    @JsonProperty("voucherHeader")
    private String voucherHeader;

    @JsonProperty("boundary")
    private String boundary;

    @JsonProperty("manualReceiptNumber")
    private String manualReceiptNumber;

    @JsonProperty("manualReceiptDate")
    private Long manualReceiptDate;

    @JsonProperty("billAccountDetails")
    private List<BillAccountDetail> billAccountDetails;

    @NotNull
    @JsonProperty("collectionType")
    private String collectionType;

    @JsonProperty("auditDetails")
    private AuditDetails auditDetails;

    private String billDescription;

    @NotNull
    @JsonProperty("expiryDate")
    private Long expiryDate;


    public Boolean addBillAccountDetail(BillAccountDetail billAccountDetail) {

        if (CollectionUtils.isEmpty(billAccountDetails)) {

            billAccountDetails = new ArrayList<>();
            return billAccountDetails.add(billAccountDetail);
        } else {

            if (!billAccountDetails.contains(billAccountDetail))
                return billAccountDetails.add(billAccountDetail);
            else
                return false;
        }
    }

}
```

BillAccountDetail.java

```java
package digit.web.models;

import com.fasterxml.jackson.annotation.JsonProperty;
import com.fasterxml.jackson.databind.JsonNode;
import lombok.*;

import javax.validation.constraints.Size;
import java.math.BigDecimal;

@Setter
@Getter
@ToString
@Builder
@NoArgsConstructor
@AllArgsConstructor
@EqualsAndHashCode
public class BillAccountDetail {

    @Size(max = 64)
    @JsonProperty("id")
    private String id;

    @Size(max = 64)
    @JsonProperty("tenantId")
    private String tenantId;

    @Size(max = 64)
    @JsonProperty("billDetailId")
    private String billDetailId;

    @Size(max = 64)
    @JsonProperty("demandDetailId")
    private String demandDetailId;

    @JsonProperty("order")
    private Integer order;

    @JsonProperty("amount")
    private BigDecimal amount;

    @JsonProperty("adjustedAmount")
    private BigDecimal adjustedAmount;

    @JsonProperty("isActualDemand")
    private Boolean isActualDemand;

    @Size(max = 64)
    @JsonProperty("taxHeadCode")
    private String taxHeadCode;

    @JsonProperty("additionalDetails")
    private JsonNode additionalDetails;

    @JsonProperty("auditDetails")
    private AuditDetails auditDetails;
}

```

_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
