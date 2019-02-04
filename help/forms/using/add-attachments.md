---
title: Adding attachments
seo-title: Adding attachments
description: null
seo-description: Add photographs and scribble notes as annotations to your task in the AEM Forms app
uuid: 8cebecd0-70e8-4499-abc6-38e9d9b731e9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 60ba4e9d-6acb-4321-9819-30edac02fce1
index: y
internal: n
snippet: y
---

# Adding attachments{#adding-attachments}

## Adding attachments in forms synced with AEM Forms Workflow server (AEM Forms on JEE) {#adding-annotations}

AEM Forms app lets you attach images, scribbled notes, and text notes to your form synced with AEM Forms JEE server. If your form is loaded from an AEM Forms Workflow server, your attachments are added to the form. You can tap the attachment button ![](assets/attachments-app.png) to see all the attachments in a form together. The red notification specifies the number of attachments in the form. If there are no attachments in the form, you cannot see the red notifications button. If there are no attachments in the form, when you tap the attachments button ![](assets/attch.png), you get options to attach photos or scribbles.

Your options are:

* **Gallery**: Lets you add a picture from the pictures saved on your device.  

* **Camera**: Lets you take a picture and add it to the form.  

* **Notes**: Lets you add a scribble or a text note. Use ![](assets/scribble.png) to add a scribble, and ![](assets/keyboard.png) to add a text note.

>[!NOTE]
>
>Attachments added by one user are visible to other AEM Forms app users. Other users cannot delete attachments added by a user. 
>

### The Attachments screen {#the-attachments-screen}

To see all the attachments in a place, tap ![](assets/attachments-app.png). You can add, rename, and delete attachments here. 

![All attachments in a place](assets/attachments-screen.png)

You can use the **+ **button in the Attachments screen to attach another picture, scribble, or text.

### Adding a photograph {#adding-a-photograph}

You can use the camera of your mobile device or saved pictures in your device to attach a picture in the form.

1. Tap the attachment button ![](assets/attch.png) at the bottom of the window.
1. Tap **Gallery** or **Camera** in the pop-up that appears. 
1. Based on the option you select, perform the following:

    1. If you select **Camera**.

       Take a photograph. Then tap the **Use** ![](assets/use-pic.png) button.

       Or tap the **Retake ** ![](assets/retake.png) button to retake the photograph.
    
    1. If you select **Gallery**.

       The image browser of device pops up. In the picture browser of your device, tap the picture you want to attach.

### Adding a note {#adding-a-note}

The **Notes** option lets you add freehand scribbles and text attachments in your form.

1. Tap the attachment button ![](assets/attch.png) at the bottom of the window.
1. Tap **Notes** in the pop-up that appears.
1. In the Notes user interface that is launched, capture a freehand scribble.

   ![Scribble interface](assets/scribble-ui.png)

   You can use the following options in the Scribble interface:

    * **Clear**: Clears the screen.
    * **Done button**: Attaches the current scribble.
    * **Cancel button**: Discards the current scribble and exits the Scribble user interface.
    * ![](assets/keyboard.png): Clears the scribble and lets you add a text note.

   ![Keyboard in AEM Forms app scribble](assets/keyboard-inapp.png)

## Attachments in forms synced with the AEM Forms servers without AEM Forms Workflow (AEM Forms on OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

Attachments for mobile forms synced with AEM Forms OSGi servers work similar to the AEM Forms JEE servers.

Form level attachments are not supported for adaptive forms loaded in the app from an AEM Forms OSGi server. To attach images or text notes, enable field level attachments in the form when you author it. Drag-drop the file attachment component from the components browser on the field.

In case of adaptive forms, you can view the attached files in the document of record (DoR). See, [Generate Document of Record for non-XFA adaptive forms](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).

[**Contact Support**](https://www.adobe.com/account/sign-in.supportportal.html)

>[!MORE_LIKE_THIS]
>
>* [Opening a task](../../forms/using/open-task.md)
>* [Working with a Form](../../forms/using/working-with-form.md)
>* [Adding attachments](../../forms/using/add-attachments.md)
>* [Saving a task (Save as Draft)](../../forms/using/save-as-draft.md)