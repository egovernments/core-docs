---
description: Design System - File Uploader component
---

# File Uploader

The File Uploader component allows users to easily upload documents and images through drag-and-drop, browse, or click actions. Built with accessibility and clarity in mind, this component ensures seamless interaction, feedback on file status, and visual clarity. It accommodates various upload needs like single, multiple, or preview-based, with consistent interaction feedback.

<figure><img src="../../../../../.gitbook/assets/image (459).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Component React" %}
```
// Sample code

<FileUpload
  multiple
  showDownloadButton
  showReUploadButton
  uploadedFiles={[]}
  validations={{
    maxSizeAllowedInMB: 5,
    minSizeRequiredInMB: 1
  }}
  variant="uploadWidget"
/>
```
{% endtab %}

{% tab title="Component Flutter" %}
```
// Sample code

FileUpload(
        allowMultiples: true,
        label: 'Upload', 
        onFilesSelected: (List<PlatformFile> files) {
            Map<PlatformFile, String?> fileErrors = {};

            return fileErrors;
        },
        openFile: true,
        showPreview: true,
        errorMessage: 'Error Message',
      ),
```
{% endtab %}

{% tab title="Component Design" %}

{% endtab %}
{% endtabs %}

## Anatomy

<figure><img src="../../../../../.gitbook/assets/image (460).png" alt=""><figcaption></figcaption></figure>

***

## Variants

***

<table data-header-hidden><thead><tr><th width="321"></th><th></th></tr></thead><tbody><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (461).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Uploader Field</strong></p><p>A compact file upload input paired with an action button. Best suited for single file uploads in form layouts.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (462).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Uploader Widget</strong></p><p>A more interactive drag-and-drop style uploader. Useful when multiple files need to be uploaded or where visual cues are important.</p></td></tr><tr><td><div><figure><img src="../../../../../.gitbook/assets/image (464).png" alt=""><figcaption></figcaption></figure></div></td><td><p><strong>Image Upload</strong></p><p>A visual first variant designed to upload and preview images. Users can click to add, preview thumbnails, or remove images directly.</p></td></tr></tbody></table>

***

## Interaction States

<table><thead><tr><th width="334.98046875"></th><th></th></tr></thead><tbody><tr><td><p><strong>Hover State for Multiple Image Load</strong></p><p>When the user hovers over the field or an item, it highlights to indicate interactivity and help the user discover selectable areas.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (466).png" alt=""><figcaption></figcaption></figure></div></td></tr><tr><td><p><strong>Mouse Down State for Multiple Image Load</strong></p><p>When the user performs a mouse-down action on the Image Upload area, a contextual menu appears offering multiple options for uploading. This menu typically includes: <br>Camera – Opens the device’s camera to capture and upload a new image instantly.<br>My Files – Opens the file explorer or gallery to choose existing images from the device. <br>This interaction provides flexibility and enhances the upload experience, especially on mobile devices or when real-time photo capture is required.</p></td><td><div><figure><img src="../../../../../.gitbook/assets/image (467).png" alt=""><figcaption></figcaption></figure></div></td></tr></tbody></table>

## Properties

|                                                                                                                                                                    |                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Single Upload</strong></p><p>Allows only one file to be uploaded at a time. Automatically replaces existing files.</p>                                  | <div><figure><img src="../../../../../.gitbook/assets/image (472).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Multiple Upload</strong></p><p>Enables uploading of several files. Each file is shown with a re-upload and download option.</p>                         | <div><figure><img src="../../../../../.gitbook/assets/image (471).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Error</strong></p><p>Displays error messages per file or globally. Indicates upload failure, unsupported format, or size limit.</p>                     | <div><figure><img src="../../../../../.gitbook/assets/image (470).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Label</strong></p><p>Each uploader can have a custom label to define the upload purpose clearly.</p>                                                    | <div><figure><img src="../../../../../.gitbook/assets/image (469).png" alt=""><figcaption></figcaption></figure></div> |
| <p><strong>Actions</strong></p><p>Includes an option to upload using the “device camera” and “my files” options, only applicable for the image upload variant.</p> | <div><figure><img src="../../../../../.gitbook/assets/image (468).png" alt=""><figcaption></figcaption></figure></div> |

## Property Configuration Table

Each design component offers a range of configurable options. These options are intentionally platform-agnostic, allowing implementations to adapt and tailor them to align with the specific requirements of the chosen framework.

{% tabs %}
{% tab title="React" %}
<table><thead><tr><th width="257">Property</th><th>Value</th><th>Default</th></tr></thead><tbody><tr><td>variant</td><td>text</td><td></td></tr><tr><td>multiple</td><td>text</td><td></td></tr><tr><td>onUpload</td><td>yes/no</td><td>no</td></tr><tr><td>validations</td><td>yes/no</td><td>no</td></tr><tr><td>removeTargetedFile</td><td>number</td><td></td></tr><tr><td>showHint</td><td>yes/no</td><td></td></tr><tr><td>showLabel</td><td>yes/no</td><td>no</td></tr><tr><td>accept</td><td>yes/no</td><td>no</td></tr><tr><td>additionalElements</td><td>yes/no</td><td>no</td></tr><tr><td>showErrorCard</td><td>number</td><td>no</td></tr><tr><td>iserror</td><td>yes/no</td><td>no</td></tr><tr><td>showDownloadButton</td><td>text</td><td>no</td></tr><tr><td>showReUploadButton</td><td>yes/no</td><td>no</td></tr><tr><td>customClass</td><td>yes/no</td><td></td></tr><tr><td>disabled</td><td>yes/no</td><td></td></tr><tr><td>style</td><td>yes/no</td><td></td></tr><tr><td>id</td><td>yes/no</td><td></td></tr><tr><td>extraStyles</td><td>yes/no</td><td></td></tr><tr><td>disabledButton</td><td>yes/no</td><td></td></tr><tr><td>textStyles</td><td>yes/no</td><td></td></tr><tr><td>buttonType</td><td>yes/no</td><td></td></tr><tr><td>showAsTags</td><td>yes/no</td><td></td></tr><tr><td>showAsPreview</td><td>yes/no</td><td></td></tr><tr><td>inline</td><td>yes/no</td><td></td></tr><tr><td>label</td><td>yes/no</td><td></td></tr></tbody></table>
{% endtab %}

{% tab title="Flutter" %}
<table><thead><tr><th>Property</th><th width="209">Value</th><th>Default</th></tr></thead><tbody><tr><td>onFilesSelected</td><td>OnFilesSelectedCallback</td><td>required</td></tr><tr><td>label</td><td>String</td><td>required</td></tr><tr><td>errorMessage</td><td>String</td><td>-</td></tr><tr><td>downloadText</td><td>String</td><td>-</td></tr><tr><td>isErrorChip</td><td>bool</td><td>-</td></tr><tr><td>reUploadText</td><td>String</td><td>-</td></tr><tr><td>showPreview</td><td>bool</td><td>false</td></tr><tr><td>allowMultiples</td><td>bool</td><td>false</td></tr><tr><td>cameraTitle</td><td>String</td><td>-</td></tr><tr><td>galleryTitle</td><td>String</td><td>-</td></tr><tr><td>cancelText</td><td>String</td><td>-</td></tr><tr><td>captureText</td><td>String</td><td>-</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Behaviours

|                                                                                                                        |                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| <div><figure><img src="../../../../../.gitbook/assets/image (473).png" alt=""><figcaption></figcaption></figure></div> | <p><strong>Drag &#x26; Drop Support</strong></p><p>Uploader Widget allows users to drag and drop files into the designated area.</p> |

***

## Usage Guide

***

| <p><strong>Allow to preview uploaded files</strong></p><p>Provide a thumbnail or preview option for the uploaded images. This helps users verify that they uploaded the correct file before submitting it.</p><p></p><p>Avoid using generic error messages like "Upload failed" without explanation. Users need to know why their file wasn't accepted and what they should do next.</p> | <p></p><div><figure><img src="../../../../../.gitbook/assets/image (474).png" alt=""><figcaption></figcaption></figure></div> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
|                                                                                                                                                                                                                                                                                                                                                                                          | <div><figure><img src="../../../../../.gitbook/assets/image (475).png" alt=""><figcaption></figcaption></figure></div>        |

## Changelog

***

| Date         | Number  | Notes                                                                                           |
| ------------ | ------- | ----------------------------------------------------------------------------------------------- |
| Dec 15, 2024 | v-0.0.2 | <p>This component is added to the website.<br>This component is now individually versioned.</p> |

## Design Checklist

***

<table data-header-hidden><thead><tr><th width="129" data-type="checkbox"></th><th></th></tr></thead><tbody><tr><td>true</td><td><strong>All interactive states</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>true</td><td><strong>Accessible use of colours</strong> - Colour is not used as the only visual means of conveying information (WCAG 2.1 1.4.1)</td></tr><tr><td>true</td><td><strong>Accessible contrast for text</strong> - Text has a contrast ratio of at least 4.5:1 for small text and at least 3:1 for large text (WCAG 2.0 1.4.3).</td></tr><tr><td>true</td><td><strong>Accessible contrast for UI components</strong> - Visual information required to identify components and states (except inactive components) has a contrast ratio of at least 3:1 (WCAG 2.1 1.4.11).</td></tr><tr><td>true</td><td><strong>Keyboard interactions</strong> - Includes all interactive states that are applicable (hover, down, focus, keyboard focus, disabled).</td></tr><tr><td>false</td><td><strong>Screen reader accessible</strong> - All content, including headings, labels, and descriptions, is meaningful, concise, contextual and accessible by screen readers.</td></tr><tr><td>true</td><td><strong>Responsive for all breakpoints</strong> - Responsiveness for 3 breakpoints - Mobile, Tablet and Desktop</td></tr><tr><td>true</td><td><strong>Usage guidelines</strong> - Includes a list of dos and don'ts that highlight best practices and common mistakes.</td></tr><tr><td>false</td><td><strong>Writing guidelines</strong> - Content standards and usage guidelines for writing and formatting in-product content for the component.</td></tr><tr><td>true</td><td><strong>Defined variants and properties</strong> - Includes relevant variants and properties (style, size, orientation, optional iconography, decorative elements, selection states, error states, etc.)</td></tr><tr><td>true</td><td><strong>Defined behaviours</strong> - Guidelines for keyboard navigation and focus, layout management (including wrapping, truncation, and overflow), animations, and user interactions.</td></tr><tr><td>true</td><td><strong>Design Kit</strong> - Access to the design file for the component in Figma, multiple options, states, colour themes, and platform scales.</td></tr></tbody></table>
