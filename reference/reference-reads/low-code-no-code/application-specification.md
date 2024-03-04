---
description: Work in Progress
---

# Application Specification

**Application Schema**

|          |                 |
| -------- | --------------- |
| ID       |                 |
| Name     |                 |
| Entities | Array of Entity |
|          |                 |

**Entity Schema**&#x20;

|             |                    |
| ----------- | ------------------ |
| ID          |                    |
| Name        |                    |
| Attributes  | Array of Attribute |
| Accesses    | Array of Access    |



**Entity Attribute Schema**

<table><thead><tr><th></th><th></th><th data-hidden></th></tr></thead><tbody><tr><td>ID</td><td></td><td><br></td></tr><tr><td>Name</td><td></td><td><br></td></tr><tr><td>Type</td><td></td><td><br></td></tr><tr><td>Required</td><td></td><td><br></td></tr><tr><td>MaxLength</td><td></td><td><br></td></tr><tr><td>MinLength</td><td></td><td><br></td></tr><tr><td>MaxValue</td><td></td><td><br></td></tr><tr><td>MinValue</td><td></td><td><br></td></tr><tr><td>DefaultValue</td><td></td><td><br></td></tr><tr><td>PossibleValues</td><td></td><td></td></tr></tbody></table>

**Access**

<table><thead><tr><th></th><th></th><th data-hidden></th></tr></thead><tbody><tr><td>Role</td><td></td><td><br></td></tr><tr><td>Type of Access</td><td>e.g. Owner, Editor, Viewer, Commenter</td><td></td></tr></tbody></table>

\


**EntityView**&#x20;

|            |                               |
| ---------- | ----------------------------- |
| ID         |                               |
| Name       |                               |
| DisplayAs  |                               |
| ViewType   | e.g.  Form, Table, List, Chat |
| EntityID   |                               |
| Groups     | Array of Group. Optional      |
| Tabs       | Array of Tab. Optional        |
| Fields     | Array of Field                |
| Conditions | Array of Condition            |
|            |                               |

**Group**

|      |   |
| ---- | - |
| ID   |   |
| Name |   |

**Tab**

|      |   |
| ---- | - |
| ID   |   |
| Name |   |

**Field**

|                   |                                                                |
| ----------------- | -------------------------------------------------------------- |
| ID                |                                                                |
| EntityAttributeID | The ID of the entity attribute to which the field is mapped to |
| DisplayAs         |                                                                |
| GroupID           | Optional. The ID of the Group to which the field belongs.      |
| TabID             | Optional. The ID of the Tab to which the field belongs.        |
| Help              | Help to be displayed on the field.                             |
| IsPII             | Is the field a Personally Identifiable Information.            |

**Condition**

|                |                                                                                                           |
| -------------- | --------------------------------------------------------------------------------------------------------- |
| ID             |                                                                                                           |
| Target1FieldID | The ID of the target field whose value needs to be checked.                                               |
| ConditionType  | e.g. Equals, Not Equals, Greater Than, Less Than, etc.                                                    |
| Target2Type    | Type of the Target 2 e.g. Field or Value                                                                  |
| TargetValue    | Fixed Value to compare with.                                                                              |
| Target2FieldID | The Field ID whose value the Target 1 Field value needs to be compared with.                              |
| Action         | The action to be performed if condition is met e,g Hide or Show, Required or Optional, Disable or Enable. |
