# Write Employee Module Code

Before starting with Employee Module Code**,** make sure you have set up the [Project Structure](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2206957569), [installed dependencies](../citizen-module-setup/install-dependency.md) and [imported the required components](../citizen-module-setup/import-required-components.md).

This section will walk you through the code that needs to be developed for the application. Detailed user screen wireframes should be available at this point for development.

<details>

<summary>Employee Module Card</summary>

In the Employee module, we create the "home card" to show the birth module in the portal. The employee card contains the following metrics: "Total application", "Inbox", and "Create Birth-registration".

#### BRCard

In BrCard.js we are reusing the components that are already present in the DIGIT-UI-component. Import the Icon and EmployeeModuleCard.

```jsx
import { PersonIcon, EmployeeModuleCard } from "@egovernments/digit-ui-react-components";
import React from "react";
import { useTranslation } from "react-i18next";

const BRCard = () => {
  const ADMIN = Digit.Utils.hrmsAccess();
  if (!ADMIN) {
    return null;
  }
    const { t } = useTranslation();
    const tenantId = Digit.ULBService.getCurrentTenantId();
   
    const propsForModuleCard = {
        Icon : <PersonIcon/>,
        moduleName: t("Birth Registration"),
        kpis: [
            {
                // count:  isLoading ? "-" : data?.EmployeCount?.totalEmployee,
                label: t("TOTAL Application"),
                link: `/digit-ui/employee/br/Inbox`
            },
         
        ],
        links: [
            {
                label: t("Inbox"),
                link: `/digit-ui/employee/br/Inbox`
            },
            {
                label: t("Create Birth-Registration"),
                link: `/digit-ui/citizen/br/birth`
            }           
        ]
    }

    return <EmployeeModuleCard {...propsForModuleCard} />
};

export default BRCard;


```



</details>

<details>

<summary>Inbox Screen</summary>

On the **"**Birth-Registration" card, we will add the Inbox link. Once we open the inbox, we can see the search, filter, create and list of applications.

![](<../../../../.gitbook/assets/image (183).png>)

**Inbox.js**

```jsx
import React, { useState, useCallback ,  useEffect  } from "react";
import { useTranslation } from "react-i18next";
import { format, isValid } from "date-fns";
import { Header ,Loader } from "@egovernments/digit-ui-react-components";
import DesktopInbox from "./DesktopInbox";
import axios from 'axios';
const Inbox = ({ tenants, parentRoute }) => {
  const { t } = useTranslation()
  Digit.SessionStorage.set("ENGAGEMENT_TENANTS", tenants);
  const tenantId = Digit.ULBService.getCurrentTenantId();
  const [pageSize, setPageSize] = useState(10);
  const [pageOffset, setPageOffset] = useState(0);
  const [searchParams, setSearchParams] = useState({
    eventStatus: [],
    range: {
      startDate: null,
      endDate: new Date(""),
      title: ""
    },
    ulb: tenants?.find(tenant => tenant?.code === tenantId)
  });
  let isMobile = window.Digit.Utils.browser.isMobile();
  const [data, setData] = useState([]);
const {isLoading } = data;
  // Using useEffect to call the API once mounted and set the data
  useEffect(() => {
    (async () => {
      const result = await axios("https://62f0e3e5e2bca93cd23f2ada.mockapi.io/birth");
      setData(result.data);
      console.log("gooo" ,result.data);
    })();
  }, []);

  const getSearchFields = () => {
    return [
      {
        label: t("EVENTS_ULB_LABEL"),
        name: "ulb",
        type: "ulb",
      },
      {
        label: t("Baby's NAME"),
        name: "babyLastName"
      }
    ]
  }

  const links = [
    {
      text: t("Create Birth-Registration"),
      link: "/digit-ui/citizen/br/birth",
    }
  ]


    
  const onSearch = (params) => {
    let updatedParams = { ...params };
    if (!params?.ulb) {
      updatedParams = { ...params, ulb: { code: tenantId } }
    }
    setSearchParams({ ...searchParams, ...updatedParams });
  }

  const handleFilterChange = (data) => {
    setSearchParams({ ...searchParams, ...data })
  }

  const globalSearch = (rows, columnIds) => {
    // return rows;
    return rows?.filter(row =>
     
      (searchParams?.babyLastName ? row.original?.babyLastName?.toUpperCase().startsWith(searchParams?.babyLastName.toUpperCase()) : true) 
     ) }

  const fetchNextPage = useCallback(() => {
    setPageOffset((prevPageOffSet) => ((parseInt(prevPageOffSet) + parseInt(pageSize))));
  }, [pageSize])

  const fetchPrevPage = useCallback(() => {
    setPageOffset((prevPageOffSet) => ((parseInt(prevPageOffSet) - parseInt(pageSize))));
  }, [pageSize])

  const handlePageSizeChange = (e) => {
    setPageSize((prevPageSize) => (e.target.value));
  };


  if (isLoading) {
    return (
      <Loader />
    );
  }
  

  return (
    <div>
      <Header>
        {t("Birth-registration")}
      
      </Header>
      <p>{}</p>
      <DesktopInbox
        t={t}
        data={data}
        links={links}
        parentRoute={parentRoute}
        searchParams={searchParams}
        onSearch={onSearch}
        globalSearch={globalSearch}
        searchFields={getSearchFields()}
        onFilterChange={handleFilterChange}
        pageSizeLimit={pageSize}
        totalRecords={data?.totalCount}
        title={"Birth-registration"}
        iconName={"calender"}
        currentPage={parseInt(pageOffset / pageSize)}
        onNextPage={fetchNextPage}
        onPrevPage={fetchPrevPage}
        onPageSizeChange={handlePageSizeChange}
      />
    </div>
  );
}

export default Inbox;
```

#### DesktopInbox.js

```jsx
import React, { useState, useCallback ,  useEffect  } from "react";
import { useTranslation } from "react-i18next";
import { format, isValid } from "date-fns";
import { Header ,Loader } from "@egovernments/digit-ui-react-components";
import DesktopInbox from "./DesktopInbox";
import axios from 'axios';
const Inbox = ({ tenants, parentRoute }) => {
  const { t } = useTranslation()
  Digit.SessionStorage.set("ENGAGEMENT_TENANTS", tenants);
  const tenantId = Digit.ULBService.getCurrentTenantId();
  const [pageSize, setPageSize] = useState(10);
  const [pageOffset, setPageOffset] = useState(0);
  const [searchParams, setSearchParams] = useState({
    eventStatus: [],
    range: {
      startDate: null,
      endDate: new Date(""),
      title: ""
    },
    ulb: tenants?.find(tenant => tenant?.code === tenantId)
  });
  let isMobile = window.Digit.Utils.browser.isMobile();
  const [data, setData] = useState([]);
const {isLoading } = data;
  // Using useEffect to call the API once mounted and set the data
  useEffect(() => {
    (async () => {
      const result = await axios("https://62f0e3e5e2bca93cd23f2ada.mockapi.io/birth");
      setData(result.data);
      console.log("gooo" ,result.data);
    })();
  }, []);

  const getSearchFields = () => {
    return [
      {
        label: t("EVENTS_ULB_LABEL"),
        name: "ulb",
        type: "ulb",
      },
      {
        label: t("Baby's NAME"),
        name: "babyLastName"
      }
    ]
  }

  const links = [
    {
      text: t("Create Birth-Registration"),
      link: "/digit-ui/citizen/br/birth",
    }
  ]


    
  const onSearch = (params) => {
    let updatedParams = { ...params };
    if (!params?.ulb) {
      updatedParams = { ...params, ulb: { code: tenantId } }
    }
    setSearchParams({ ...searchParams, ...updatedParams });
  }

  const handleFilterChange = (data) => {
    setSearchParams({ ...searchParams, ...data })
  }

  const globalSearch = (rows, columnIds) => {
    // return rows;
    return rows?.filter(row =>
     
      (searchParams?.babyLastName ? row.original?.babyLastName?.toUpperCase().startsWith(searchParams?.babyLastName.toUpperCase()) : true) 
     ) }

  const fetchNextPage = useCallback(() => {
    setPageOffset((prevPageOffSet) => ((parseInt(prevPageOffSet) + parseInt(pageSize))));
  }, [pageSize])

  const fetchPrevPage = useCallback(() => {
    setPageOffset((prevPageOffSet) => ((parseInt(prevPageOffSet) - parseInt(pageSize))));
  }, [pageSize])

  const handlePageSizeChange = (e) => {
    setPageSize((prevPageSize) => (e.target.value));
  };


  if (isLoading) {
    return (
      <Loader />
    );
  }
  

  return (
    <div>
      <Header>
        {t("Birth-registration")}
      
      </Header>
      <p>{}</p>
      <DesktopInbox
        t={t}
        data={data}
        links={links}
        parentRoute={parentRoute}
        searchParams={searchParams}
        onSearch={onSearch}
        globalSearch={globalSearch}
        searchFields={getSearchFields()}
        onFilterChange={handleFilterChange}
        pageSizeLimit={pageSize}
        totalRecords={data?.totalCount}
        title={"Birth-registration"}
        iconName={"calender"}
        currentPage={parseInt(pageOffset / pageSize)}
        onNextPage={fetchNextPage}
        onPrevPage={fetchPrevPage}
        onPageSizeChange={handlePageSizeChange}
      />
    </div>
  );
}

export default Inbox;
```



</details>

<details>

<summary>Application Table</summary>

This lists the birth registration applications in a table-like format.

![](<../../../../.gitbook/assets/image (210).png>)

We import the `Table` component already present in our digit-UI-react-component. In the table, we are passing the data, column, global search, onSearch, filter, pagination, pagesize limit, total record, current page, Next page, PreviousPage, pagesizechange.

```jsx
import React from "react";
import { Table } from "@egovernments/digit-ui-react-components";

const ApplicationTable = ({
  t,
  data,
  columns,
  globalSearch,
  onSearch,
  getCellProps,
  pageSizeLimit,
  totalRecords,
  currentPage,
  onNextPage,
  onPrevPage,
  onPageSizeChange,

}) => {
  return (
    <Table
      t={t}
      data={data}
      columns={columns}
      onSearch={onSearch}
      globalSearch={globalSearch}
      manualGlobalFilter={true}
      manualPagination={true}
      pageSizeLimit={pageSizeLimit}
      getCellProps={getCellProps}
      totalRecords={totalRecords}
      currentPage={currentPage}
      onNextPage={onNextPage}
      onPrevPage={onPrevPage}
      onPageSizeChange={onPageSizeChange}

    />
  )
}

export default ApplicationTable;
```

\


</details>

<details>

<summary>Add Small Card</summary>

![](<../../../../.gitbook/assets/image (56).png>)

In this file, we will add code to create a "small card with a create link.

```jsx
import React from "react";
import { Card, DocumentIcon, EventCalendar } from "@egovernments/digit-ui-react-components";
import { useTranslation } from "react-i18next";
import { Link } from "react-router-dom";

const EventLink = ({ title = "Birth", links, icon = 'calender' }) => {
  const { t } = useTranslation();

  const GetLogo = () => (
    <div className="header" style={{ justifyContent: "flex-start" }}>
      <span className="logo" style={{ backgroundColor: "#fff" }}>
        {icon === "calender" ? <EventCalendar /> : icon === "survey" ? 'surveyIcon' :  <DocumentIcon />}
      </span>
      {" "}
      <span className="text">{t(title)}</span>
    </div>
  );
  
return (
  <Card className="employeeCard filter inboxLinks">
    <div className="complaint-links-container">
      {GetLogo()}
      <div className="body">
        {links.map(({ link, text, hyperlink = false, accessTo = [] }, index) => {
          return (
            <span className="link" key={index}>
        <Link to={"citizen/br/birth"}>{"create"}</Link>
            </span>
          );
        })}
      </div>
    </div>
  </Card>
)
};

export default EventLink;
```

</details>

<details>

<summary>Search</summary>

We can enable searching for the baby's details from the baby's first name using the search box.

![](<../../../../.gitbook/assets/image (140).png>)

```
import React from "react";
import { useForm, Controller } from "react-hook-form";
import { TextInput, Label, SubmitBar, LinkLabel, ActionBar, CloseSvg, DatePicker } from "@egovernments/digit-ui-react-components";
import DropdownUlb from "./DropdownUlb";
import { alphabeticalSortFunctionForTenantsBasedOnName } from "../../../utils";

const Search = ({ onSearch, searchParams, searchFields, type, onClose, isInboxPage, t }) => {
  const { register, handleSubmit, formState, reset, watch, control } = useForm({
    defaultValues: searchParams,
  });
  const mobileView = innerWidth <= 640;
  const ulb = Digit.SessionStorage.get("ENGAGEMENT_TENANTS");
  const tenantId = Digit.ULBService.getCurrentTenantId();
  const userInfo = Digit.UserService.getUser().info;
  // const userUlbs = ulb.filter(ulb => userInfo?.roles?.some(role => role?.tenantId === ulb?.code)).sort(alphabeticalSortFunctionForTenantsBasedOnName)
  
  const getFields = (input) => {
    switch(input.type) {
      case "ulb":
        return (
          <Controller
          rules={{ required: true }}
            render={props => (
              <DropdownUlb
                onAssignmentChange={props.onChange}
                value={props.value}
                // ulb={userUlbs}
                t={t}
              />
            )}
            name={input.name}
            control={control}
            defaultValue={null}
          />
        )
      default:
        return (
          <Controller
            render={(props) => <TextInput onChange={props.onChange} value={props.value} />}
            name={input.name}
            control={control}
            defaultValue={null}
          />
        )
    }
  }

  const onSubmitInput = (data) => {
    // searchFields.forEach((field) => {
    //   if (!data[field.name]) data.delete.push(field.name);
    // });

    onSearch(data);
    if (type === "mobile") {
      onClose();
    }
  }

  const clearSearch = () => {
    reset({ ulb: null, eventName: '' });
    onSearch({ ulb: null, eventName: '' })
  };

  const clearAll = (mobileView) => {
    const mobileViewStyles = mobileView ? { margin: 0 } : {};
    return (
      <LinkLabel style={{ display: "inline", ...mobileViewStyles }} onClick={clearSearch}>
        {t("ES_COMMON_CLEAR_SEARCH")}
      </LinkLabel>
    );
  };

  return (
    <form onSubmit={handleSubmit(onSubmitInput)}>
      <div className="search-container" style={{ width: "auto", marginLeft: isInboxPage ? "24px" : "revert" }}>
          <div className="search-complaint-container">
            {(type === "mobile" || mobileView) && (
              <div className="complaint-header">
                <h2>{t("ES_COMMON_SEARCH_BY")}</h2>
                <span onClick={onClose}>
                  <CloseSvg />
                </span>
              </div>
            )}
            <div className={"complaint-input-container for-pt " + (!isInboxPage ? "for-search" : "")} style={{ width: "100%" }}>
              {searchFields
                ?.map((input, index) => (
                  <div key={input.name} className="input-fields">
                    {/* <span className={index === 0 ? "complaint-input" : "mobile-input"}> */}
                    <span className={"mobile-input"}>
                      <Label>{t(input.label) + ` ${input.isMendatory ? "*" : ""}`}</Label>
                      {getFields(input)}
                    </span>
                    {formState?.dirtyFields?.[input.name] ? (
                      <span
                        style={{ fontWeight: "700", color: "rgba(212, 53, 28)", paddingLeft: "8px", marginTop: "-20px", fontSize: "12px" }}
                        className="inbox-search-form-error"
                      >
                        {formState?.errors?.[input.name]?.message}
                      </span>
                    ) : null}
                  </div>
                ))}

     
              {type === "desktop" && !mobileView && (
                <div style={{ maxWidth: "unset", marginLeft: "unset", marginTop: "55px"}} className="search-submit-wrapper">
                  <SubmitBar
                    className="submit-bar-search"
                    label={t("ES_COMMON_SEARCH")}
                    // disabled={!!Object.keys(formState.errors).length || formValueEmpty()}
                    submit
                  />
                  {/* style={{ paddingTop: "16px", textAlign: "center" }} className="clear-search" */}
                  <div>{clearAll()}</div>
                </div>
              )}
            </div>
          </div>
        </div>
        {(type === "mobile" || mobileView) && (
          <ActionBar className="clear-search-container">
            <button className="clear-search" style={{ flex: 1 }}>
              {clearAll(mobileView)}
            </button>
            <SubmitBar disabled={!!Object.keys(formState.errors).length} label={t("ES_COMMON_SEARCH")} style={{ flex: 1 }} submit={true} />
          </ActionBar>
        )}
    </form>
  )

}

export default Search;
```





</details>

<details>

<summary>Set Up Filters</summary>

We will set up filters by date range here.

![](<../../../../.gitbook/assets/image (130).png>)

```jsx
import React, { useState } from "react";
import { ActionBar, RemoveableTag, CloseSvg, Loader, DateRange, Localities, ApplyFilterBar, SubmitBar, Dropdown, RefreshIcon } from "@egovernments/digit-ui-react-components";
import { useTranslation } from "react-i18next";


const Filter = ({ type = "desktop", onClose, onSearch, onFilterChange, searchParams }) => {
  const { t } = useTranslation();
  const [localSearchParams, setLocalSearchParams] = useState(() => ({ ...searchParams }));
  const tenantId = Digit.ULBService.getCurrentTenantId();
  const state = tenantId?.split('.')[0];
  const { isLoading, data } = Digit.Hooks.useCommonMDMS(state, "mseva", ["EventCategories"]);

  const clearAll = () => {
    setLocalSearchParams({ eventCategory: null, eventStatus: [], range: { startDate: null, endDate: new Date(""), title: "" } })
    onFilterChange({ eventCategory: null, eventStatus: [], range: { startDate: null, endDate: new Date(""), title: "" } });
    onClose?.();
  };

  const applyLocalFilters = () => {
    onFilterChange(localSearchParams);
    onClose?.();
  };
  const handleChange = (data) => {
    setLocalSearchParams({ ...localSearchParams, ...data });
  };
  const onStatusChange = (e, type) => {
    if (e.target.checked) handleChange({ eventStatus: [...(localSearchParams?.eventStatus || []), type] })
    else handleChange({ eventStatus: localSearchParams?.eventStatus?.filter(status => status !== type) })
  }

  if (isLoading) {
    return (
      <Loader />
    );
  }
  
  return (
    <div className="filter">
      <div className="filter-card">
        <div className="heading">
          <div className="filter-label">{t("ES_COMMON_FILTER_BY")}:</div>
          <div className="clearAll" onClick={clearAll}>
            {t("ES_COMMON_CLEAR_ALL")}
          </div>
          {type === "desktop" && (
            <span className="clear-search" onClick={clearAll}>
              <RefreshIcon />
            </span>
          )}
          {type === "mobile" && (
            <span onClick={onClose}>
              <CloseSvg />
            </span>
          )}
        </div>
        <div className="filter-label">{`${t(`BR `)}`}</div>
        <Dropdown option={data?.mseva?.EventCategories} optionKey="code" t={t} selected={localSearchParams?.eventCategory} select={val => handleChange({ eventCategory: val })} />
        <DateRange t={t} values={localSearchParams?.range} onFilterChange={handleChange} labelClass="filter-label" />
        {/* <div>
          <Status onAssignmentChange={onStatusChange} searchParams={localSearchParams} />
        </div> */}
        <div>
          <SubmitBar style={{ width: '100%' }} onSubmit={() => applyLocalFilters()} label={t("ES_COMMON_APPLY")} />
        </div>
      </div>
    </div>
  )
}

export default Filter;
```



</details>

<details>

<summary>Set Up Routes</summary>

```jsx
import { PrivateRoute } from "@egovernments/digit-ui-react-components";
import React from "react";
import { useTranslation } from "react-i18next";
import { Link, Switch, useLocation , Route } from "react-router-dom";
import Inbox from "./Inbox/Inbox";
import ResponseEmployee from "./ResponseEmployee";

const EmployeeApp = ({ path, url, userType ,tenants, parentRoute }) => {
  const { t } = useTranslation();

  const BRManageApplication = Digit?.ComponentRegistryService?.getComponent("BRManageApplication");
  const RegisterDetails = Digit?.ComponentRegistryService?.getComponent("RegisterDetails");
  const Inbox = Digit?.ComponentRegistryService?.getComponent("Inbox");
  const ResponseEmployee = Digit?.ComponentRegistryService?.getComponent("ResponseEmployee");

  return (
    <Switch>
      <React.Fragment>
        <div className="ground-container">
       
        <PrivateRoute path={`${path}/responseemp`} component={() => <ResponseEmployee/>} />
        <PrivateRoute path={`${path}/inbox`} component={props => <Inbox {...props} tenants={tenants} parentRoute={parentRoute} />} />
        {/* <PrivateRoute path={`${path}/details`} component={() => <RegisterDetails />} /> */}
          <PrivateRoute path={`${path}/myapplication`} component={() => <BRManageApplication />} />
          <PrivateRoute path={`${path}/details/:id`} component={(props) => <RegisterDetails {...props} />} />
        </div>
      </React.Fragment>
    </Switch>
  );
};

export default EmployeeApp;

```



</details>

<details>

<summary>Display Application Details</summary>

This component shows the details of the application.&#x20;

```jsx
import { Header, ActionBar, SubmitBar, ExternalLinkIcon, Menu, GenericFileIcon, LinkButton } from '@egovernments/digit-ui-react-components';
import React, { useState , useEffect } from 'react'
import { useTranslation } from 'react-i18next';
import { openDocumentLink, openUploadedDocument } from '../../utils';
import axios from 'axios';
import { useParams } from "react-router-dom";



const RegisterDetails = ({ location, match, history, }) => {

  const params = useParams();
  const [data, setData] = useState([]);

  useEffect(() => {
    (async () => {
      const result = await axios(`https://62f0e3e5e2bca93cd23f2ada.mockapi.io/birth/${params.id}`);
      setData(result.data);
      console.log("gooo" ,result.data);
    })();
  }, [params.id]);


    let isMobile = window.Digit.Utils.browser.isMobile();
    const { t } = useTranslation();
   
    const [displayMenu, setDisplayMenu] = React.useState(false);
    const [showModal, setShowModal] = useState(false);


    function onActionSelect(action) {
        // setSelectedAction(action);
     
          history.push(`/digit-ui/employee/br/responseemp`)
    }


    return (
        <div>
            {/* {showModal ? <Confirmation
                t={t}
                heading={'CONFIRM_DELETE_DOC'}
                docName={details?.name}
                closeModal={() => setShowModal(!showModal)}
                actionCancelLabel={'CS_COMMON_CANCEL'}
                actionCancelOnSubmit={onModalCancel}
                actionSaveLabel={'ES_COMMON_Y_DEL'}
                actionSaveOnSubmit={onModalSubmit}
            />

                : null} */}
            <Header>{t(`Birth-Registration Details`)}</Header>
            <div className="notice_and_circular_main gap-ten">
                <div className="documentDetails_wrapper">
                    {/* <div className="documentDetails_row_items"><p className="documentDetails_title">{`${t('ULB')}:`}</p> <p>{data?.tenantId}</p> </div> */}
                    <div className="documentDetails_row_items"><p className="documentDetails_title">{`${t('Babys First NAME')}:`}</p> <p>{data?.babyFirstName}</p> </div>
                    <div className="documentDetails_row_items"><p className="documentDetails_title">{`${t('Babys Last NAME')}:`}</p> <p>{t(data?.babyLastName)}</p> </div>
                    <div className="documentDetails_row_items"><p className="documentDetails_title">{`${t('Father NAME')}:`}</p> <p>{t(data?.fatherName)}</p> </div>
                    <div className="documentDetails_row_items"><p className="documentDetails_title">{`${t('Mother NAME')}:`}</p> <p>{t(data?.motherName)}</p> </div>
                    <div className="documentDetails_row_items"><p className="documentDetails_title">{`${t('Doctor NAME')}:`}</p> <p>{t(data?.doctorName)}</p> </div>
                    <div className="documentDetails_row_items"><p className="documentDetails_title">{`${t('Hospital NAME')}:`}</p> <p>{t(data?.hospitalName)}</p> </div>
                    <div className="documentDetails_row_items"><p className="documentDetails_title">{`${t('Applicant MobileNumber')}:`}</p> <p>{t(data?.applicantMobileNumber)}</p> </div>
                    <div className="documentDetails_row_items"><p className="documentDetails_title">{`${t('Correspondence Address')}:`}</p> <p>{t(data?.correspondenceAddress)}</p> </div>
                    <div className="documentDetails_row_items"><p className="documentDetails_title">{`${t('Correspondence City')}:`}</p> <p>{t(data?.correspondenceCity)}</p> </div>
                    <div className="documentDetails_row_items"><p className="documentDetails_title">{`${t('Permanent Address')}:`}</p> <p>{t(data?.permanentAddress)}</p> </div>
                    <div className="documentDetails_row_items"><p className="documentDetails_title">{`${t('Place Of Birth')}:`}</p> <p>{t(data?.placeOfBirth)}</p> </div>
    
                    {/* <div className="documentDetails_row_items"><p className="documentDetails_title">{`${t('DCOUMENT_DESCRIPTION')}:`}</p> <p className="documentDetails__description">{details?.description?.length ? details?.description : 'NA'}</p> </div> */}
                    {/* <div className="documentDetails_row_items"><p className="documentDetails_title">{`${t('ES_COMMON_LINK_LABEL')}:`}</p>
                        {details?.documentLink ? <LinkButton
                            label={
                                <div className="link" onClick={() => openDocumentLink(details?.documentLink, details?.name)}>
                                    <p>{t(`CE_DOCUMENT_OPEN_LINK`)}</p>
                                </div>
                            }
                        /> : 'NA'}
                    </div> */}
                  
                </div>
            </div>
            <ActionBar>
        {displayMenu ? (
          <Menu
            localeKeyPrefix={"BR"}
            options={['Approve', 'Reject']}
            t={t}
            onSelect={onActionSelect}
          />
        ) : null}
        <SubmitBar label={t("ES_COMMON_TAKE_ACTION")} onSubmit={() => setDisplayMenu(!displayMenu)} />
      </ActionBar>
      {showModal &&
        <Modal
          headerBarMain={<Heading label={t('ES_EVENT_DELETE_POPUP_HEADER')} />}
          headerBarEnd={<CloseBtn onClick={() => setShowModal(false)} />}
          actionCancelLabel={t("CS_COMMON_CANCEL")}
          actionCancelOnSubmit={() => setShowModal(false)}
          actionSaveLabel={t('APPROVE')}
          actionSaveOnSubmit={handleDelete}
        >
          <Card style={{ boxShadow: "none" }}>
            <CardText>{t(`REJECT`)}</CardText>
          </Card>
        </Modal>
          }
        </div>
    )
}

export default RegisterDetails;

```

![](<../../../../.gitbook/assets/image (212).png>)







</details>

<details>

<summary>Registering All Components &#x26; Modules</summary>

`module.js` is the entry point where we can register all components and modules.

```jsx
import {  CitizenHomeCard, PTIcon } from "@egovernments/digit-ui-react-components";
import React, { useEffect } from "react";
import { useTranslation } from "react-i18next";
import { useRouteMatch } from "react-router-dom";
import CitizenApp from "./pages/citizen";
import Create from "./pages/citizen/create/index";
import EmployeeApp from "./pages/employee";
import BrSelectName from "./pagecomponents/BrSelectName";
import BRSelectPhoneNumber from "./pagecomponents/BrSelectPhoneNumber";
import BRSelectGender from "./pagecomponents/BRSelectGender";
import BRSelectEmailId from "./pagecomponents/SelectEmailId";
import BRSelectPincode from "./pagecomponents/BRSelectPincode";
import BrSelectAddress from "./pagecomponents/BrSelectAddress";
import SelectCorrespondenceAddress from "./pagecomponents/SelectCorrespondenceAddress";
import SelectDocuments from "./pagecomponents/SelectDocuments";
import BRCard from "./components/config/BRCard";
import BRManageApplication from "./pages/employee/BRManageApplication";
import RegisterDetails from "./pages/employee/RegisterDetails";
import Response from "./pages/citizen/create/Response";
import Inbox from "./pages/employee/Inbox/Inbox";
import DesktopInbox from "./pages/employee/Inbox/DesktopInbox";
import ResponseEmployee from "./pages/employee/ResponseEmployee";

const componentsToRegister = {
  ResponseEmployee,
  DesktopInbox,
  Inbox,
 Response,
  RegisterDetails,
  BRManageApplication,
  BRCard,
  SelectDocuments,
  SelectCorrespondenceAddress,
  BrSelectAddress,
  BRSelectPincode,
  BRSelectEmailId,
  BRSelectGender,
  BRSelectPhoneNumber,
  BrSelectName,
  BRCreate : Create,
};

export const BRModule = ({ stateCode, userType, tenants }) => {
  const { path, url } = useRouteMatch();

  const moduleCode = "BR";
  const language = Digit.StoreData.getCurrentLanguage();
  const { isLoading, data: store } = Digit.Services.useStore({ stateCode, moduleCode, language });


  if (userType === "citizen") {
    return <CitizenApp path={path} stateCode={stateCode} />;
  }

  return <EmployeeApp path={path} stateCode={stateCode} />;
};

export const BRLinks = ({ matchPath, userType }) => {
  const { t } = useTranslation();


  const links = [
  
    {
      link: `${matchPath}/birth`,
      i18nKey: t("Create BirthRegistration"),
    },
 

   
  ];

  return <CitizenHomeCard header={t("BirthRegistration")} links={links} Icon={() => <PTIcon className="fill-path-primary-main" />} />;
};

export const initBRComponents = () => {
  Object.entries(componentsToRegister).forEach(([key, value]) => {
    Digit.ComponentRegistryService.setComponent(key, value);
  });
};


```

So after adding all components to the module.js, we need to enable modules in `web/src/app.js` and `example/src/index.js`.&#x20;

In app.js, add the following code:

```jsx
import React from 'react';

import { initDSSComponents } from "@egovernments/digit-ui-module-dss";
import { PaymentModule, PaymentLinks, paymentConfigs } from "@egovernments/digit-ui-module-common";
import { DigitUI } from "@egovernments/digit-ui-module-core";
import { initLibraries } from "@egovernments/digit-ui-libraries";
import { initEngagementComponents } from "@egovernments/digit-ui-module-engagement";
import {initCustomisationComponents} from "./Customisations";
import { BRModule ,initBRComponents ,BRLinks} from "@egovernments/digit-ui-module-br";

initLibraries();

const enabledModules = ["Payment","QuickPayLinks", "DSS","Engagement", "BR"];
window.Digit.ComponentRegistryService.setupRegistry({
  ...paymentConfigs,
  PaymentModule,
  PaymentLinks,
  BRModule,
  BRLinks,

});

initBRComponents();
initDSSComponents();
initEngagementComponents();
initCustomisationComponents();




function App() {
  const stateCode = window.globalConfigs?.getConfig("STATE_LEVEL_TENANT_ID") || process.env.REACT_APP_STATE_LEVEL_TENANT_ID;
  if (!stateCode) {
    return <h1>stateCode is not defined</h1>
  }
  return (
    <DigitUI stateCode={stateCode} enabledModules={enabledModules}  />
  );
}

export default App;

```

In `index.js`, add the following:

```jsx
import React from "react";
import ReactDOM from "react-dom";
import { initLibraries } from "@egovernments/digit-ui-libraries";
 import { BRModule, initBRComponents ,BRLinks} from "@egovernments/digit-ui-module-br";
import { initDSSComponents } from "@egovernments/digit-ui-module-dss";
import { PaymentModule, PaymentLinks, paymentConfigs } from "@egovernments/digit-ui-module-common";
import { initEngagementComponents } from "@egovernments/digit-ui-module-engagement";
import { DigitUI } from "@egovernments/digit-ui-module-core";
import "@egovernments/digit-ui-css/example/index.css";



var Digit = window.Digit || {};

const enabledModules = [ "Payment","QuickPayLinks", "DSS","Engagement","BR"];

const initTokens = (stateCode) => {
  const userType = window.sessionStorage.getItem("userType") || process.env.REACT_APP_USER_TYPE || "CITIZEN";

  const token =window.localStorage.getItem("token")|| process.env[`REACT_APP_${userType}_TOKEN`];
 
  const citizenInfo = window.localStorage.getItem("Citizen.user-info")
 
  const citizenTenantId = window.localStorage.getItem("Citizen.tenant-id") || stateCode;

  const employeeInfo = window.localStorage.getItem("Employee.user-info");
  const employeeTenantId = window.localStorage.getItem("Employee.tenant-id");

  const userTypeInfo = userType === "CITIZEN" || userType === "QACT" ? "citizen" : "employee";
  window.Digit.SessionStorage.set("user_type", userTypeInfo);
  window.Digit.SessionStorage.set("userType", userTypeInfo);

  if (userType !== "CITIZEN") {
    window.Digit.SessionStorage.set("User", { access_token: token, info: userType !== "CITIZEN" ? JSON.parse(employeeInfo) : citizenInfo });
  } else {
    // if (!window.Digit.SessionStorage.get("User")?.extraRoleInfo) window.Digit.SessionStorage.set("User", { access_token: token, info: citizenInfo });
  }

  window.Digit.SessionStorage.set("Citizen.tenantId", citizenTenantId);
 
 if(employeeTenantId && employeeTenantId.length) window.Digit.SessionStorage.set("Employee.tenantId", employeeTenantId);
};

const initDigitUI = () => {
  window?.Digit.ComponentRegistryService.setupRegistry({

    PaymentModule,
    BRModule,
    PaymentLinks,
    BRLinks,

  });

  initDSSComponents();
  initEngagementComponents();
  initBRComponents();
  
  const stateCode = window?.globalConfigs?.getConfig("STATE_LEVEL_TENANT_ID") || "pb";
  initTokens(stateCode);

  const registry = window?.Digit.ComponentRegistryService.getRegistry();
  ReactDOM.render(<DigitUI stateCode={stateCode} enabledModules={enabledModules} />, document.getElementById("root"));
};

initLibraries().then(() => {
  initDigitUI();
});

```





</details>



\


[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this website by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
