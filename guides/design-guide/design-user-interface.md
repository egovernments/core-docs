# Design User Interface

## **Overview**

This page provides the details on designing the transactional user interface and performance dashboards.

## Steps

### **Design Transactional User Interface**

Identify the points different roles interact with the system from the process model.

<table><thead><tr><th width="247">Activity</th><th>User Interface Required</th></tr></thead><tbody><tr><td>Apply for Birth Certificate</td><td>New Application UI<br>Applicated Submitted UI</td></tr><tr><td>Make Payment</td><td>Payment UI<br>Payment Successful UI</td></tr><tr><td>Verify Application</td><td>Verify Application UI<br>Application Verified UI</td></tr><tr><td>Send Notification</td><td>Notification UI</td></tr><tr><td>Update Application</td><td>Edit Application UI <br>Update Successful UI</td></tr><tr><td>Approve Application</td><td>Approve Application UI<br>Application Approved/Rejected UI</td></tr><tr><td>Download Certificate</td><td>Download Birth Certificate UI<br>Birth Certificate UI</td></tr></tbody></table>

DIGIT UI design guidelines are [available here](https://design.digit.org/ui-docs/).

FIGMA designs using the above Guidelines are available here. Feel free to copy and modify as per your needs.

DIGIT UI Accelerators available in React and Flutter implement these Guidelines as reusable components and UI frameworks. The entire source code is open and [available here](https://github.com/egovernments/DIGIT-OSS/tree/master/frontend/mono-ui/web/rainmaker).

### **Design Performance Dashboard**

DIGIT Decision Support Dashboard (DSS) looks like below.&#x20;

![Cantonment Citizen Dashboard - All Services](<../../.gitbook/assets/image (71).png>)

Each of the widgets corresponds to one service and that displays basic performance metrics for that service. This can be further drilled down to the below view for deeper analysis.&#x20;

![Cantonment Citizen Dashboard - Complaints Dashboard](<../../.gitbook/assets/image (179).png>)

The performance metrics and dimensions identified of the service can be mapped to different available visualizations in DSS.

<table><thead><tr><th>Metric</th><th width="150">Dimension</th><th width="150">Comparison</th><th>Visualisation</th></tr></thead><tbody><tr><td>Total Birth Certificate Applications</td><td>None</td><td>Previous Year</td><td>Metric</td></tr><tr><td>Average Time</td><td>None</td><td>Previous Year</td><td>Metric</td></tr><tr><td>Total Applications </td><td>By Location</td><td></td><td>Pie Chart</td></tr><tr><td>Total Applications</td><td>By Status</td><td></td><td>Pie Chart</td></tr><tr><td>Total Applications</td><td>By Week</td><td></td><td>Line Chart</td></tr></tbody></table>
