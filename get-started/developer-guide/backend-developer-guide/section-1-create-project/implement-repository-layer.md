# Implement Repository Layer

## **Overview**

Methods in the service layer, upon performing all the business logic, call methods in the repository layer to persist or lookup data i.e. it interacts with the configured data store. For executing the queries, JdbcTemplate class is used. JdbcTemplate takes care of the creation and release of resources such as creating and closing the connection etc. All database operations namely insert, update, search and delete can be performed on the database using methods of JdbcTemplate class.

## **Steps**

On DIGIT the create and update operations are handled asynchronously.&#x20;

The persister service listens on the topic to which service applications are pushed for insertion and updation. Persister then takes care of executing insert and update operations on the database without clogging the application’s threads.

The execution of search queries on the database returns applications as per the search parameters provided by the user.

### **Implement Repository Layer**

1. **Create packages -** Add the`querybuilder` and `rowmapper` packages within the repository folder.
2.  **Create a class -** by the name of BirthApplicationQueryBuilder in `querybuilder` folder and annotate it with `@Component` annotation.&#x20;

    Insert the following content in BirthApplicationQueryBuilder class -

{% code lineNumbers="true" %}
```java
package digit.repository.querybuilder;

import digit.web.models.BirthApplicationSearchCriteria;
import org.springframework.stereotype.Component;
import org.springframework.util.CollectionUtils;
import org.springframework.util.ObjectUtils;

import java.util.List;

@Component
public class BirthApplicationQueryBuilder {

    private static final String BASE_BTR_QUERY = " SELECT btr.id as bid, btr.tenantid as btenantid, btr.applicationnumber as bapplicationnumber, btr.babyfirstname as bbabyfirstname, btr.babylastname as bbabylastname, btr.fatherid as bfatherid, btr.motherid as bmotherid, btr.doctorname as bdoctorname, btr.hospitalname as bhospitalname, btr.placeofbirth as bplaceofbirth, btr.timeofbirth as btimeofbirth, btr.createdby as bcreatedby, btr.lastmodifiedby as blastmodifiedby, btr.createdtime as bcreatedtime, btr.lastmodifiedtime as blastmodifiedtime, ";

    private static final String ADDRESS_SELECT_QUERY = " add.id as aid, add.tenantid as atenantid, add.type as atype, add.address as aaddress, add.city as acity, add.pincode as apincode, add.registrationid as aregistrationid ";

    private static final String FROM_TABLES = " FROM eg_bt_registration btr LEFT JOIN eg_bt_address add ON btr.id = add.registrationid ";

    private final String ORDERBY_CREATEDTIME = " ORDER BY btr.createdtime DESC ";

    public String getBirthApplicationSearchQuery(BirthApplicationSearchCriteria criteria, List<Object> preparedStmtList){
        StringBuilder query = new StringBuilder(BASE_BTR_QUERY);
        query.append(ADDRESS_SELECT_QUERY);
        query.append(FROM_TABLES);

        if(!ObjectUtils.isEmpty(criteria.getTenantId())){
            addClauseIfRequired(query, preparedStmtList);
            query.append(" btr.tenantid = ? ");
            preparedStmtList.add(criteria.getTenantId());
        }
        if(!ObjectUtils.isEmpty(criteria.getStatus())){
            addClauseIfRequired(query, preparedStmtList);
            query.append(" btr.status = ? ");
            preparedStmtList.add(criteria.getStatus());
        }
        if(!CollectionUtils.isEmpty(criteria.getIds())){
            addClauseIfRequired(query, preparedStmtList);
            query.append(" btr.id IN ( ").append(createQuery(criteria.getIds())).append(" ) ");
            addToPreparedStatement(preparedStmtList, criteria.getIds());
        }
        if(!ObjectUtils.isEmpty(criteria.getApplicationNumber())){
            addClauseIfRequired(query, preparedStmtList);
            query.append(" btr.applicationnumber = ? ");
            preparedStmtList.add(criteria.getApplicationNumber());
        }

        // order birth registration applications based on their createdtime in latest first manner
        query.append(ORDERBY_CREATEDTIME);

        return query.toString();
    }

    private void addClauseIfRequired(StringBuilder query, List<Object> preparedStmtList){
        if(preparedStmtList.isEmpty()){
            query.append(" WHERE ");
        }else{
            query.append(" AND ");
        }
    }

    private String createQuery(List<String> ids) {
        StringBuilder builder = new StringBuilder();
        int length = ids.size();
        for (int i = 0; i < length; i++) {
            builder.append(" ?");
            if (i != length - 1)
                builder.append(",");
        }
        return builder.toString();
    }

    private void addToPreparedStatement(List<Object> preparedStmtList, List<String> ids) {
        ids.forEach(id -> {
            preparedStmtList.add(id);
        });
    }
}
```
{% endcode %}

5.  **Create a class -** by the name of BirthApplicationRowMapper within the rowmapper package and annotate it with @Component.&#x20;

    Add the following content to the class.

    ```java
    package digit.repository.rowmapper;

    import digit.web.models.*;
    import org.egov.common.contract.models.Address;
    import org.egov.common.contract.models.AuditDetails;
    import org.egov.common.contract.request.User;
    import org.egov.common.contract.user.enums.AddressType;
    import org.springframework.dao.DataAccessException;
    import org.springframework.jdbc.core.ResultSetExtractor;
    import org.springframework.stereotype.Component;

    import java.sql.ResultSet;
    import java.sql.SQLException;
    import java.util.*;

    @Component
    public class BirthApplicationRowMapper implements ResultSetExtractor<List<BirthRegistrationApplication>> {
        public List<BirthRegistrationApplication> extractData(ResultSet rs) throws SQLException, DataAccessException {
            Map<String,BirthRegistrationApplication> birthRegistrationApplicationMap = new LinkedHashMap<>();

            while (rs.next()){
                String uuid = rs.getString("bapplicationnumber");
                BirthRegistrationApplication birthRegistrationApplication = birthRegistrationApplicationMap.get(uuid);

                if(birthRegistrationApplication == null) {

                    Long lastModifiedTime = rs.getLong("blastModifiedTime");
                    if (rs.wasNull()) {
                        lastModifiedTime = null;
                    }


                    User father = User.builder().uuid(rs.getString("bfatherid")).build();
                    User mother = User.builder().uuid(rs.getString("bmotherid")).build();

                    AuditDetails auditdetails = AuditDetails.builder()
                            .createdBy(rs.getString("bcreatedBy"))
                            .createdTime(rs.getLong("bcreatedTime"))
                            .lastModifiedBy(rs.getString("blastModifiedBy"))
                            .lastModifiedTime(lastModifiedTime)
                            .build();

                    birthRegistrationApplication = BirthRegistrationApplication.builder()
                            .applicationNumber(rs.getString("bapplicationnumber"))
                            .tenantId(rs.getString("btenantid"))
                            .id(rs.getString("bid"))
                            .babyFirstName(rs.getString("bbabyfirstname"))
                            .babyLastName(rs.getString("bbabylastname"))
                            .father(father)
                            .mother(mother)
                            .doctorName(rs.getString("bdoctorname"))
                            .hospitalName(rs.getString("bhospitalname"))
                            .placeOfBirth(rs.getString("bplaceofbirth"))
                            .timeOfBirth(rs.getInt("btimeofbirth"))
                            .auditDetails(auditdetails)
                            .build();
                }
                addChildrenToProperty(rs, birthRegistrationApplication);
                birthRegistrationApplicationMap.put(uuid, birthRegistrationApplication);
            }
            return new ArrayList<>(birthRegistrationApplicationMap.values());
        }

        private void addChildrenToProperty(ResultSet rs, BirthRegistrationApplication birthRegistrationApplication)
                throws SQLException {
            addAddressToApplication(rs, birthRegistrationApplication);
        }

        private void addAddressToApplication(ResultSet rs, BirthRegistrationApplication birthRegistrationApplication) throws SQLException {
            Address address = Address.builder()
                    .tenantId(rs.getString("atenantid"))
                    .address(rs.getString("aaddress"))
                    .city(rs.getString("acity"))
                    .pinCode(rs.getString("apincode"))
                    .build();

            BirthApplicationAddress birthApplicationAddress= BirthApplicationAddress.builder()
                            .id(rs.getString("aid"))
                            .tenantId(rs.getString("atenantid"))
                            .applicantAddress(address)
                            .build();

            birthRegistrationApplication.setAddress(birthApplicationAddress);

        }

    }
    ```

{% code lineNumbers="true" %}
```java
```
{% endcode %}

6.  **Create a class -** by the name of BirthRegistrationRepository within the repository folder and annotate it with @Repository annotation.&#x20;

    Add the following content to the class.

{% code lineNumbers="true" %}
```java
package digit.repository;

import digit.repository.querybuilder.BirthApplicationQueryBuilder;
import digit.repository.rowmapper.BirthApplicationRowMapper;
import digit.web.models.BirthApplicationSearchCriteria;
import digit.web.models.BirthRegistrationApplication;
import lombok.extern.slf4j.Slf4j;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Repository;

import java.util.ArrayList;
import java.util.List;


@Slf4j
@Repository
public class BirthRegistrationRepository {

    @Autowired
    private BirthApplicationQueryBuilder queryBuilder;

    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Autowired
    private BirthApplicationRowMapper rowMapper;

    public List<BirthRegistrationApplication>getApplications(BirthApplicationSearchCriteria searchCriteria){
        List<Object> preparedStmtList = new ArrayList<>();
        String query = queryBuilder.getBirthApplicationSearchQuery(searchCriteria, preparedStmtList);
        log.info("Final query: " + query);
        return jdbcTemplate.query(query, preparedStmtList.toArray(), rowMapper);
    }
}
```
{% endcode %}

The repository layer is implemented.
