# Development Control Rules (Digit-DCR)

## Introduction <a href="#developmentcontrolrules-digit-dcr-introduction" id="developmentcontrolrules-digit-dcr-introduction"></a>

Currently, ULBs follow a complete manual mass mode of providing various building-related approvals and related NOCs. This delays the approval process and creates a lot of inconvenience for applicants and architects. There is also a lack of transparency and accountability in this manual approach. Due to the complexity of scrutiny and approval processes and the involvement of various stakeholders, there are several challenges in the system. Some of the issues are-Complex rules and bye-laws and their interpretation, the time-consuming process of issuance of Planning Permission, increased chances of human errors due to manual submission and scrutiny, inadequate citizen interface and no single point of contact, etc.

The manual scrutiny of the building bye-laws is replaced with “**Digit-DCR**”.Digit-DCR is capable of reading the drawing, extracting parameter values, applying them to bylaws and generating the acceptance or rejection information in seconds. This process provides a leap of  **15 days of cumbersome manual work to a few seconds**. The Digit-DCR is even capable of marking mistakes and failing details. It converts details of drawing like Site plans, Floor plans, Elevation, etc to pdf and saves them in the system.

## Prerequisites  <a href="#developmentcontrolrules-digit-dcr-prerequisites" id="developmentcontrolrules-digit-dcr-prerequisites"></a>

Knowledge on following&#x20;

1. Java
2. Basics of 2D Drawing like ( Top view, Front view, Side view, etc)
3. Basic Math

## Functionality <a href="#developmentcontrolrules-digit-dcr-functionality" id="developmentcontrolrules-digit-dcr-functionality"></a>

### High-level design <a href="#developmentcontrolrules-digit-dcr-high-leveldesign" id="developmentcontrolrules-digit-dcr-high-leveldesign"></a>

<figure><img src="../../../../.gitbook/assets/image (197).png" alt=""><figcaption></figcaption></figure>

Sequence Diagram

<figure><img src="../../../../.gitbook/assets/image (187).png" alt=""><figcaption></figcaption></figure>

## Configuration and Set up

### References and Notes <a href="#developmentcontrolrules-digit-dcr-referencesandnotes" id="developmentcontrolrules-digit-dcr-referencesandnotes"></a>

### **Layer Name Standards**  <a href="#developmentcontrolrules-digit-dcr-layernamestandards" id="developmentcontrolrules-digit-dcr-layernamestandards"></a>

The general Practice of the Architects is to draw diagrams in the default layer with the name “0” with portions stating Section Plan, Floor Plan, etc. With this approach, it is not possible to extract parts of the building for Bye-Laws validation. Hence Parts of the buildings should be drawn in specific layers. These layers also should have a standard format for machine reading.

For example, Plan will have a “Bathroom” and "Washbasin” which should be validated for dimensions and counts for Sanitation. Hence these sanitation-related parts should be drawn in a layer called “BLK\_1\_WATER\_CLOSET” layer, where “BLK\_1” states it is block 1 and “WATER\_CLOSET” states it is a toilet. Another example is Toilets for the disabled should be validated floor wise Hence it should be defined as Floorwise layer names like “BLK\_1\_FLR\_0\_SP\_WC” layer.

We cannot define a complete set of layer names with these combinations because it is based on the following parameters

1. Number of Blocks
2. Number of Floors in each Block
3. Number of Polygons on each floor&#x20;
4. Number of levels

So when data is required at Plan Level, Block Level, Floor Level, or Height it is named and prefixed accordingly

### Plan Level <a href="#developmentcontrolrules-digit-dcr-planlevel" id="developmentcontrolrules-digit-dcr-planlevel"></a>

At the Plan level, the layer names are used without any prefixes. The list of  such layer names are&#x20;

<table data-header-hidden><thead><tr><th width="105"></th><th></th></tr></thead><tbody><tr><td>1</td><td>PLOT_BOUNDARY</td></tr><tr><td>2</td><td>VERT_CLEAR_OHEL</td></tr><tr><td>3</td><td>HORIZ_CLEAR_OHEL</td></tr><tr><td>4</td><td>WASTE_DISPOSAL</td></tr><tr><td>5</td><td>PLAN_INFO</td></tr></tbody></table>

### Block Level

| Block Level Layer Names |                                |
| ----------------------- | ------------------------------ |
| 1                       | BLK\_\*\_COVERED\_AREA         |
| 2                       | BLK\_\*\_COVERED\_AREA\_DEDUCT |
| 3                       | BLK\_\*\_BATH                  |
| 4                       | BLK\_\*\_WC                    |

### Floor Level <a href="#developmentcontrolrules-digit-dcr-floorlevel" id="developmentcontrolrules-digit-dcr-floorlevel"></a>

| Floor Level Layer Names |                                         |
| ----------------------- | --------------------------------------- |
| 1                       | BLK\_\*\_FLR\_\*\_BLT\_UP\_AREA         |
| 2                       | BLK\_\*\_FLR\_\*\_BLT\_UP\_AREA\_DEDUCT |

### **Color Code Standards** <a href="#developmentcontrolrules-digit-dcr-colorcodestandards" id="developmentcontrolrules-digit-dcr-colorcodestandards"></a>

Some parts of the building and its validation is based on Usage(Occupancy) types. For example, every floor in which all types of usage present have to be defined. Based on usage type parking has to be calculated. So only layer name is not sufficient to differentiate but colour also to include. Hence Floorwise built-up area will be defined in “BLK\_1\_FLR\_0\_BLT\_UP\_AREA” with index colour 2 for Residential type of usage. All colours are defined based on Occupancy type. The below list provides the colour codes for each occupancy-&#x20;

| 1 | Residential                                             | 1  | <p><br></p> |
| - | ------------------------------------------------------- | -- | ----------- |
| 2 | Commercial                                              | 8  | <p><br></p> |
| 3 | Apartment/Group Housing                                 | 2  | <p><br></p> |
| 4 | Hostel/ Residential building Lodging purpose/Guesthouse | 19 | <p><br></p> |

### **Drawing Standards**

The following components are used in the drawing. EDCR deals with only a defined set of drawing components.&#x20;

| Drawing Components | <p><br></p> | <p><br></p>   | <p><br></p>  |
| ------------------ | ----------- | ------------- | ------------ |
| **Serial No**      | **Type**    | **Supported** | **Required** |
| 1                  | Line        | YES           | YES          |
| 2                  | Dimension   | YES           | YES          |
| 3                  | PolyLine    | YES           | YES          |
| 4                  | Circle      | YES           | YES          |
| 5                  | Arc         | NO            | NO           |

{% file src="../../../../.gitbook/assets/BPA Final Template - Drawing standards (1).pdf" %}
