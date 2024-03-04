# Workflow Component

## Overview

There are two common components for workflow related actions and timeline management.

* WorkflowActions - [WorkflowActions](https://github.com/egovernments/DIGIT-Works/blob/c2a234bb4b21f0e54ca9664ee3e99d72ce871168/frontend/micro-ui/web/micro-ui-internals/packages/react-components/src/atoms/WorkflowActions.js)
* WorkflowTimeline - [WorkflowTimeline](https://github.com/egovernments/DIGIT-Works/blob/6de6633cb1da5c5bd17b8a4f258a090d5b68a28d/frontend/micro-ui/web/micro-ui-internals/packages/react-components/src/atoms/WorkflowTimeline.js)

Both of these components are available on each View Screen. The WorkflowTimeline component is responsible for presenting the workflow history at the bottom of the View Screen. Similarly, the WorkflowActions component renders an action bar at the bottom of the view screens, showcasing pertinent actions based on the logged-in user's role and workflow configuration.

## Workflow Timeline

This component is directly integrated with the [ApplicationDetailsContent](https://github.com/egovernments/DIGIT-Works/blob/6de6633cb1da5c5bd17b8a4f258a090d5b68a28d/frontend/micro-ui/web/micro-ui-internals/packages/modules/templates/ApplicationDetails/components/ApplicationDetailsContent.js) component that renders all the relevant data in view screens. WorkflowTimeline component is called in this component like this:

<figure><img src="https://lh3.googleusercontent.com/dj6pwKQixOCFzXGkq1kc3A0eGLbI9wdmyAhKO0t9Tahn4Y-aLZk6CuaMZoARljtpVYgz5kvtTg7lUcLe9jlb8gGK4v09DOZNC_r-cVAGwPko88wBv8XFpaiVdB1VfiInc-KNlZrOibT3FaDVMdsRMbk" alt=""><figcaption></figcaption></figure>

It expects a few props:

* BusinessService -> Name of the businessService from workflow configuration
* applicationNo -> Idgen generated application number
* tenantId
* timelineStatusPrefix -> prefix used in localisation of every checkpoint in timeline
* statusAttribute -> here we can pass the attribute(either status/state) that is the key in the workflow process instance response, whichever we want to show in the checkpoint.

This component internally calls the workflow APIs to fetch the process instance of the application and renders the history accordingly. It also makes a check for the current state of the application. If the current state is not terminated state then it will show an extra checkpoint at the top with statusAttribute as status to show pending states checkpoint. If the current state is terminated state then it will not show pending states.&#x20;

Refer to the below snapshots, notice they both have 4 checkpoints. Approved refers to terminate state.

## Workflow Actions

This component is rendered on every View component separately to render the action bar with relevant actions.&#x20;

<img src="https://lh5.googleusercontent.com/iZGt5H07sBU52a9ntoWoziJNgghqEjeDqFkSud8g2ghjFXTjek-gT3fbSRQwLpUlI6Fo2zS3PqzOs64hr_98me6WPUI9oiUf2LW5d08Splg8LqG9MT7YVmP-eEU4gQv4BTfblDWwchJ8JEBmGzJ4WuY" alt="" data-size="original"><img src="https://lh5.googleusercontent.com/ed7OYzOF4J9mjvP_NzVRlwf52zwpO9ZDSBl9C1XjtHT1u2FWe9GWmhOb7h07wEdCfsBcGJ_-6VdDnbXicy9D1t6h11Df-fzhhF-W-r-CZJ-Z7kWdbi2hsSot-LMR5sZHaWjm5pTxdOpxXvuzcvsaKho" alt="" data-size="original">\


Sample code Snapshot:

<figure><img src="https://lh4.googleusercontent.com/CCJDim9OwrU_dIS58ENrRl95THBIn4nIiTbFRvv7gupqg6_0PsN4iDRFo6QqnCN06nN1yVv83ncTriwVN4iT2LAzz2LDKTeV7TN8QAyvXhMhA449ZKXK_kxY_zTXzcmK7yd0Hv74cv6QlpfnrlHdxMQ" alt=""><figcaption></figcaption></figure>

It expects a few props:

* BusinessService -> Name of the businessService from workflow configuration
* forcedActionPrefix -> for localization
* applicationNo -> Idgen generated application number
* tenantId
* applicationDetails -> same data returned from hook used on view screen
* Url -> update API url to hit&#x20;
* setStateChanged -> when update is successful this is called. Hence search apis will be called again and workflow history and workflow actions will be updated without screen refresh
* moduleCode
* editApplicationNumber -> Used in case of edit/modify action

This component internally calls the update apis and shows a relevant toast on success/failure or a response screen in case of edit action.&#x20;

A significant part of this component is another component called the [WorkflowPopup](https://github.com/egovernments/DIGIT-Works/blob/c2a234bb4b21f0e54ca9664ee3e99d72ce871168/frontend/micro-ui/web/micro-ui-internals/packages/react-components/src/atoms/Modals/WorkflowPopup.js). This is the popup that renders whenever the user clicks on a specific action. This popup is fully configurable through this configuration file [Popup Config](https://github.com/egovernments/DIGIT-Works/blob/b001e1e4ed39a09830389fe258e164b0b4570531/frontend/micro-ui/web/micro-ui-internals/packages/react-components/src/atoms/Modals/config/configEstimateModal.js). Popup configs are defined in this configuration file which are organised as per the businessService of the workflow configuration. Refer to the configMap object in this file for more details.\
