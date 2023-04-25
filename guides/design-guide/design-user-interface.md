# Design User Interface

**Design Transactional User Interface**

To identify the points different roles interact with the system from the process model.

| Activity                    | User Interface Required                                           |
| --------------------------- | ----------------------------------------------------------------- |
| Apply for Birth Certificate | <p>New Application UI<br>Applicated Submitted UI</p>              |
| Make Payment                | <p>Payment UI<br>Payment Successful UI</p>                        |
| Verify Application          | <p>Verify Application UI<br>Application Verified UI</p>           |
| Send Notification           | Notification UI                                                   |
| Update Application          | <p>Edit Application UI <br>Update Successful UI</p>               |
| Approve Application         | <p>Approve Application UI<br>Application Approved/Rejected UI</p> |
| Download Certificate        | <p>Download Birth Certificate UI<br>Birth Certificate UI</p>      |

DIGIT UI Design Guidelines are available here - [https://egovernments.github.io/ui-docs/](https://egovernments.github.io/ui-docs/)&#x20;

FIGMA Designs using the above Guidelines are available here. Feel free to copy and modify as per your needs.

DIGIT UI Accelerators available in React and Flutter implement these Guidelines as reusable components and UI frameworks. The entire source code is open and available here - [https://github.com/egovernments/DIGIT-OSS/tree/master/frontend/mono-ui/web/rainmaker](https://github.com/egovernments/DIGIT-OSS/tree/master/frontend/mono-ui/web/rainmaker) &#x20;

**Design Performance Dashboard**

DIGIT Decision Support Dashboard (DSS) looks like below.&#x20;

![Cantonment Citizen Dashboard - All Services](<../../.gitbook/assets/image (68).png>)

Each of the widgets corresponds to one service and that displays basic performance metrics for that service. This can be further drilled down to the below view for deeper analysis.&#x20;

![Cantonment Citizen Dashboard - Complaints Dashboard](<../../.gitbook/assets/image (20).png>)

The performance metrics and dimensions identified of the service can be mapped to different available visualizations in DSS.

| Metric                               | Dimension   | Comparison    | Visualisation |
| ------------------------------------ | ----------- | ------------- | ------------- |
| Total Birth Certificate Applications | None        | Previous Year | Metric        |
| Average Time                         | None        | Previous Year | Metric        |
| Total Applications                   | By Location |               | Pie Chart     |
| Total Applications                   | By Status   |               | Pie Chart     |
| Total Applications                   | By Week     |               | Line Chart    |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this website by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
