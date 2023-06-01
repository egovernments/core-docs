# eDCR Approach Guide

## Introduction <a href="#introduction" id="introduction"></a>

This document mainly aims to help the implementation team in configuring and customizing the eDCR engine as per the state/city rules and regulations. Samples are given for each of the activities that are to be done. This can be considered as a handbook on how to approach the DCR automated scrutiny for a newcomer.&#x20;

### Activities Involved <a href="#activities-involved" id="activities-involved"></a>

Below mentioned are the various activities to be done as part of eDCR customization and configurations for the state/city. Also, it mentioned the training needs for the end-users.

### Layer Matrix/Template <a href="#layer-matrix-template" id="layer-matrix-template"></a>

Layer Matrix contains the colour and layer names to be applied while drawing a plan that needs to be scrutinized in the eDCR system. A sample is provided [here](https://drive.google.com/open?id=0B6DZY63wggn5SzJHMjF5Qm05alFFV3RRZ0tsVnViU3BWZHFz). If there are new layers to be added or a new occupancy type to be considered, additions will have to be made to layers and colours. This needs to be done by a person having architecture and Auto Cad knowledge. The document needs to be updated with the new layers and colours and the same need to be shared with the architects.

### Drawing Manual <a href="#drawing-manual" id="drawing-manual"></a>

Drawing manual maps list of layers used in marking for a feature. [Here](https://drive.google.com/open?id=11clYEfBCSOXAZUpA8eAbngRdLg9huOiK) is a sample drawing manual for a client. Similarly, this customer-specific manual needs to be created.

### Drawing Details <a href="#drawing-details" id="drawing-details"></a>

Drawing details provide additional details required for marking or drawing a part or full feature.

Drawing details can be understood and prepared using the column “Parameters /Additional details to be addressed in drawings “ column from this [sheet](https://docs.google.com/spreadsheets/d/1dloyJRCYfEBfed-Nowx-d9t2pKnOeuTm6Vdl4OGy-II/edit#gid=484175232).&#x20;

### Data Collection Template <a href="#data-collection-template" id="data-collection-template"></a>

Rules need to be read and understood from the state rule book and this information has to be translated into a data template. This will enable the customization team to validate and codify the rules efficiently. [Here](https://drive.google.com/open?id=1EMF0ugi2wS0031ZtBeuJa9Kr4l8GnzO0rPITWqhWRwY) is a reference to a sample data collection template. This may need to be enhanced for any state-specific rules if it cannot fit into the sample one.

## Configuration & Customization <a href="#configuration-and-customization" id="configuration-and-customization"></a>

Based on the rules documented in the data template, the implementation team needs to make the required configuration changes in the existing features. In cases where the default implementation is different from the state rules, customization needs to be done by the implementation team. If there are any rules in a state which are not covered in any of the features in eDCR, this needs to be coded afresh.

**Example 1:** where there is a change in the existing rule and the rule number-

Change in the FAR (Floor Area Ratio) in a particular state, where the expected value is 1.4 instead of 1.2 which is the default. Changes will need to be done in the FAR.java file for this.

**Example 2:** Where there is a new rule, say -distance from the monument -

If this rule is not currently available in eDCR, you will need to add a new file with the rule name, where the implementation of the rule will be written.

## Help Videos <a href="#help-videos" id="help-videos"></a>

Videos are helping tools for architects to make a plan drawing as per the standards defined by the eDCR system. Implementation partners will be training the end-user which is an architect using these help videos. These are the [Sample videos](https://kozhikode.egovernments.org/egi/resources/guide/bpaHelpDocument.jsp) that are done for Kozhikode, Kerala state.

\
