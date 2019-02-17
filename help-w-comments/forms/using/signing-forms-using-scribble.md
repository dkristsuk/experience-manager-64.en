---
title: Apply electronic signatures to a form using scribble signatures
seo-title: Apply electronic signatures to a form using scribble signatures
description: Signing forms using scribble
seo-description: Signing forms using scribble
uuid: 81152eee-536c-462b-92a0-60ee4edc95c0
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: 23875ee5-a237-4962-8ddf-ef6ee07492ab
index: y
internal: n
snippet: y
---

# Apply electronic signatures to a form using scribble signatures{#apply-electronic-signatures-to-a-form-using-scribble-signatures}

You can use the **Scribble Signature **component and **Signature Step **component to draw(Scribble) signature on an adaptive form. The Signature step component displays a PDF version of the adaptive form. You require a Document of Record option enabled or form template based adaptive forms to use the Signature step component.

Both the components provide a window, as displayed below, to sign a form. You can also click the geolocation icon ![](assets/aem_6_3_geolocation.png) to add geolocation to the signature.

![Scribble sign dialog](assets/scribble-signature.png) 

## Configure an adaptive form to use Scribble Signature {#configure-an-adaptive-form-to-use-scribble-signature}

1. Create a Document of Record option enabled or form template based adaptive form. For step-by-step information, see [Creating an adaptive form](../../forms/using/creating-adaptive-form.md).
1. Drag-and-drop the **Scribble Signature** component from component browser to the adaptive form.
1. Tap the **Configure ** ![](assets/configure.png) icon. It opens properties browser and displays properties of the Scribble Signature component. Configure properties of the Scribble Signature component. 
1. Drag-and-drop the Signature Step component from component browser to the adaptive form.

   >[!NOTE]
   >
   >The Signature Step component takes up full width available for the form. It is recommended to not have any other component on the section containing the Signature Step component.

1. In the Content browser, tap **Form Container**, and tap the **Configure ** ![](https://chl-author-preview.corp.adobe.com/content/dam/help/icons/Configure.png) icon. It opens properties browser and displays Adaptive Form container properties. Navigate to **Adaptive Form Container** &gt; **Electronic Signature** and deselect the **Enable Adobe Sign** option. Tap the Done ![](assets/aem_6_3_forms_save.png) icon to save the changes.

   >[!NOTE]
   >
   >When you add a Signature Step component to an adaptive form, the Enable Adobe Sign option is selected automatically.

1. Tap the **Configure ** ![](assets/configure.png) icon. It opens properties browser and displays Signature step properties. Configure the following properties:

    * **Element Name**: Specify name of the component.  
    
    * **Title:** Specify unique title of the component.
    * **Template message:** Specify the message to be displayed while the signature PDF is being loaded. Adobe Sign services take some time to prepare and load signature PDF.
    * **Signing Service:** Select the **Scribble Signature** option.  
    
    * **CSS Class**: Specify CSS class of the client library, if any. It is recommended to use [themes](../../forms/using/themes.md) and [in-line styles](../../forms/using/inline-style-adaptive-forms.md) instead of CSS Class.

   Tap the Done ![](assets/aem_6_3_forms_save.png) icon to save the changes. The Signature is configured sucessfully.

   Now, when you fill a form, a PDF version of adaptive form is displayed and options to sign the PDF document are provided. For detailed information, see [Sign an adaptive form using Scribble Signature](../../forms/using/signing-forms-using-scribble.md#main-pars-header-134183786).

## Sign an adaptive form using Scribble Signature {#sign-an-adaptive-form-using-scribble-signature}

1. After you fill an adaptive form and reach the Signature Step page, the signature screen is displayed.

   ![Signature screen for EchoSign page](assets/esignscribblesign.jpg)

1. Click **[!UICONTROL Sign]**. The scribble sign dialog appears. Sign the form and click the Done ![](assets/aem_6_3_forms_save.png) icon to save the signature.

   ![Scribble sign dialog](assets/scribblewidget.jpg)

1. Click complete to finish the signing process. 

   ![Complete the signing process](assets/scribblecomplete.jpg)

The signatures are added to the form and the form control moves to the next panel.

>[!MORE_LIKE_THIS]
>
>* [Integrate Adobe Sign with AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
>* [Using Adobe Sign in an adaptive form](../../forms/using/working-with-adobe-sign.md)