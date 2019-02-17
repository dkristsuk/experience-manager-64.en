---
title: Tables in adaptive forms
seo-title: Tables in adaptive forms
description: The Table component in AEM Forms lets you create tables in adaptive forms that are responsive to mobile layouts, and also allows using XDP table components. 
seo-description: The Table component in AEM Forms lets you create tables in adaptive forms that are responsive to mobile layouts, and also allows using XDP table components. 
uuid: 40cb2055-6f91-4d56-9050-c26d0f2e5e03
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: ef0cd166-22aa-4572-beab-98c343a80577
index: y
internal: n
snippet: y
---

# Tables in adaptive forms{#tables-in-adaptive-forms}

Using tables is an effective, simplified, and organized way of presenting complex data. It helps users in identifying information easily and providing inputs in an ordered arrangement of rows and columns. Most forms from financial services and government organizations require large data tables to put numbers and perform calculations.

AEM Forms provides a Table component in the components browser in sidebar that lets you create tables in adaptive forms. Some of the key capabilities it provides are:

* Responsive layout on mobile devices
* Configurable rows and columns
* Dynamic addition and deletion of rows at runtime  
* Combine or merge and split cells
* Accessible by screen readers
* Custom layout using CSS
* Compatible and mapped with XDP table component
* Support for adding rows or cells using XSD complex type elements  
* Merge data from an XML file

## Create a table {#create-a-table}

To create a table, drag-and-drop the Table component from the components browser in the sidekick on the adaptive form. By default, the table contains two columns and three rows, including the header row.

![Table component in AEM sidebar](assets/sidebar-tables.png) 

### About header and body cells {#about-header-and-body-cells}

The header cells are text fields. To change the label for a header, right-click the header cell and click **Edit**. In the Edit dialog, update the label in the **Value** field and click **OK**.

The body cells are text boxes, by default. You can replace a body cell with any other adaptive forms component available in the sidekick, such as a numeric box, date picker, or drop-down list.

For example, the first body row in the following table includes text box, date picker, and drop-down list components as cells.

![](assets/row-cell-types.png)

You can merge two or more body cells by selecting the cells you want to merge, right-click, and select **Merge**. Also, you can split a merged cell by right-clicking it and selecting **Split Cells**.

### Add, delete, move rows and columns {#add-delete-move-rows-and-columns}

You can add and delete a row or column, and move a row up and down in a table.

To add or delete a row or column or move a row, click any cell in the row or column. A drop-down menu appears at the top of the column and on the left of the row. The menu at the top provides options to add or delete the column, whereas the menu on the left allows you to add, delete, or move the row.

* The Add operation adds a row below or a column to the right of the selected row or column.
* The Delete operation deletes the selected row or column.
* The Move Up and Move Down operation moves the selected row up and down.

The drop-down menu for the row also provides the Edit operation to edit row properties, settings, and styling options.

![](assets/add-delete-move-row-column.png)

>[!NOTE]
>
>While you can add any number of rows in a table, the maximum number of columns you can add is six. Also, you cannot delete the header row from the table.

### Add table description {#add-table-description}

You can add a description of the table to explain how the information is organized that screen readers can interpret and read out. To add the description:

1. Select the table and tap ![](assets/cmppr.png) to see its properties in the sidebar.
1. Specify summary in the Accessibility tab.
1. Click **Done**.

## Configure table style {#configure}

You can define the style for a table by using the Style mode in the page toolbar. Perform the following steps to switch to style mode and edit the table styling

1. In the page toolbar, before Preview, tap ![](assets/canvas-drop-down.png) &gt; **Style**.

1. In the sidebar select table and tap the edit button ![](assets/edit-button.png).   
   You can see the styling properties in the sidebar.

![Styling properties of a table](assets/style-table.png) 

<!--
Comment Type: draft

<p>In the Styling tab, you can specify the following properties for a table:</p>
<p><strong>Width</strong>: Specifies the width of the table, in percentage, with respect to the total width available for the table in the parent container.</p>
<p><strong>Height</strong>: Specifies the maximum height, in pixels, for the table.</p>
<p><strong>CSS class</strong>: Specifies a CSS class to apply any custom style to a table.</p>
<p><strong>Mobile layout</strong>: Specifies how a table should appear on a mobile device. The available options are Headers on Left and Collapsible Columns. For more information, see <a href="#-mobile-layouts-for">Mobile layouts for tables</a>.</p>
<p><strong>Column width</strong>: Specifies proportionate width for each column in a table as a comma-separated list. For example, if you specify <strong>1,2,3,4</strong> as the column width for a four-column table, the total table width will be distributed as 1/10, 2/10, 3/10, and 4/10 among the first, second, third, and fourth columns, respectively.</p>
-->

>[!NOTE]
>
>You can change the color theme for header and body rows by changing the values of LESS variables. For more information, see [Themes in AEM Forms](../../forms/using/themes.md) [](../../forms/using/creating-custom-adaptive-form-themes.md).

<!--
Comment Type: draft

<h2>Change background color for table rows</h2>
-->

<!--
Comment Type: draft

<p>The color theme for the header and body rows are defined in the <span class="code">globalvariables.less</span> file. To change the color theme for the rows:</p>
<ol>
<li>In CRXDE Lite, navigate to the <span class="code">/etc/clientlibs/fd/af/guidetheme/common/less/</span> folder.</li>
<li>Double-click to open the <span class="code">globalvariables.less</span> file.</li>
<li>Look for the following less variables and updated their values as required:<br />
<ul>
<li><span class="code">@table-header-bg-color</span> - defines the color for the header row. The default value is #333.</li>
<li><span class="code">@table-odd-row-bg-color</span> - defines the color for the odd body row. The default value is <span class="code">rgb(255, 255, 255)</span>.</li>
<li><span class="code">@table-even-row-bg-color</span> - defines the color for the even body row, The default value is <span class="code">#eee</span>.</li>
</ul> </li>
<li>Save the file.</li>
</ol>
<p>The updated color theme will be applied to the tables in all adaptive forms.</p>
-->

## Add or delete a row dynamically {#add-or-delete-a-row-dynamically}

Tables provide out-of-the box support for dynamically adding or deleting rows at runtime.

1. Select a table row and tap ![](assets/cmppr.png).
1. In the Repeat settings tab, specify the minimum and maximum counts to limit the number of rows in the table.
1. Click **Done**.

At runtime, you will see **+** and *-* buttons to add or delete a row.

![](assets/add-delete-rows-dynamically.png)

>[!NOTE]
>
>Adding or deleting a row dynamically is not supported in Headers on left mobile layout of tables.

## Expressions in a table {#expressions-in-a-table}

Tables in adaptive forms allow you to write expressions in JavaScript to induce behaviors, such as show or hide a table or a row, add up all the numbers and show the total in a cell, enable or disable a cell, validate user input, and so on. These expressions use adaptive forms scripting model APIs.

While tables and rows support only visibility expressions to control their visibility based on the value returned by an expression, cells support the following expressions:

* **Initialization Script:** to perform an action on initialization of a field.
* **Value Commit Script:** to change the components of a form after the value of a field is changed.

>[!NOTE]
>
>If the XFA change/exit script is also applied to the same field, the XFA change/exit script executes before the Value Commit script.

* **Calculate expressions**: to auto-compute value of a field.
* **Validation expressions**: to validate a field.
* **Access expressions**: to enable/disable a field.
* **Visibility expression**: to control visibility of a field and panel.

The visibility expression for a table or a row can be defined in the Panel properties tab of their corresponding Edit component dialog. The expressions for a cell can be defined in the Script tab of its Edit component dialog.

For the complete list of adaptive forms classes, events, objects, and public APIs, see [JavaScript Library API reference for adaptive forms](http://helpx.adobe.com/aem-forms/6/javascript-api/index.html).

## Mobile layouts {#mobile-layouts}

Tables in adaptive forms provide unmatched experience mobile devices because of its fluid and responsive layouts. AEM Forms offers two types of mobile layouts for tables - Headers on left and Collapsible columns.

You can configure a mobile layout for a table from the Styling tab of the Edit component dialog for a table.

### Headers on left {#headers-on-left}

In the Headers on left layout, the header in the table are transposed on the left with only one cell appearing against a header. Each row in this layout appears as a distinct section. The following images compare a table on a desktop with that on a mobile device.

![](assets/desktopview.png)

Desktop view of a table with Header on left layout

![](assets/headersontheleft.png)

Mobile view of a table with Header on left layout

### Collapsible columns layout {#collapsible-columns-layout}

In the Collapsible column layout, the columns in the table collapse to show one or two columns, depending on the device size, while other columns are collapsed. You can click the collapse/expand icon to view other columns in the table.

***Note**: While Collapsible column layout is optimized for mobile devices, it will work on desktop as well, if the width available is not enough to show all the columns in a table. *

The following images compare how a table looks on a device with collapsed and expanded columns.

![](assets/collapsed-column.png)

Collapsed columns of a table with only two columns showing up on a mobile device

![](assets/collapsible_column.png)

Expanded column of a table on a mobile device

## Merge data in a table {#merge-data-in-a-table}

Tables in adaptive forms allow you to populate the table at runtime using data from an XML file. The data XML file can reside in the local file system of the machine where AEM Forms server is running or in the CRX repository.

Let’s take example of the following bank transaction summary table that we want to populate with data from an XML file.

![](assets/data-merge-table.png)

In this example, the Element name property for:

* the row is **Row1**
* the body cell under Transaction date is **tableItem1**
* the body cell under Description is **tableItem2**
* the body cell under Transaction type is **type**
* the body cell under Amount in USD is **tableItem3**

The XML file that contains data in the following format:

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
 <typeSelect>0</typeSelect>
 <Row1>
      <tableItem1>2015-01-08</tableItem1>
      <tableItem2>Purchase laptop</tableItem2>
      <type>0</type>
      <tableItem3>12000</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-05</tableItem1>
      <tableItem2>Transport expense</tableItem2>
      <type>0</type>
      <tableItem3>120</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2014-01-08</tableItem1>
      <tableItem2>Laser printer</tableItem2>
      <type>0</type>
      <tableItem3>500</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2014-12-08</tableItem1>
      <tableItem2>Credit card payment</tableItem2>
      <type>0</type>
      <tableItem3>300</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-06</tableItem1>
      <tableItem2>Interest earnings</tableItem2>
      <type>1</type>
      <tableItem3>12000</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-05</tableItem1>
      <tableItem2>Payment from a client</tableItem2>
      <type>1</type>
      <tableItem3>500</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-08</tableItem1>
      <tableItem2>Food expense</tableItem2>
      <type>0</type>
      <tableItem3>120</tableItem3>
 </Row1>
 </data>
  </afUnboundData>
  <afBoundData>
    <data/>
  </afBoundData>
  <afBoundData/>
</afData>

```

In the sample XML, the data for a row is defined by the <Row1> tags, which is the element name for the row in the table. Within the `<Row1>` tag, the data for each cell is defined within the tag for its element name, such as `<tableItem1>`, `<tableItem2>`, `<tableItem3>`, and `<type>`.

To merge this data with the table at runtime, we need to point the adaptive form containing the table to the absolute XML location with wcmmode disabled. For example, if the adaptive form is at *http://localhost:4502/myForms/bankTransaction.html* and the data XML file is saved at *C:/myTransactions/bankSummary.xml*, you can view the table with data at the following URL:

*http://localhost:4502/myForms/bankTransaction.html?dataRef=file:/// C:/myTransactions/bankSummary.xml&wcmmode=disabled* 

![](assets/data-merged-table.png) 

## Use XDP components and XSD complex types {#use-xdp-components-and-xsd-complex-types}

If you created an adaptive form based on an XFA form template, the XFA elements are available in the Data Model tab of AEM Content Finder. You can drag and drop these XFA elements, including tables, in the adaptive form.

The XFA table element is mapped to the Table component and works out-of-the-box in adaptive forms. All properties and functionalities of XDP table are preserved when moved into adaptive form, and you can perform any operation on it just as you do with native adaptive form table. For example, if a row in an XDP table is marked repeatable, it will be repeated when dropped in adaptive forms as well.

In addition, you can drag-drop XDP subform to add a new row in the table. However, note that dropping a nested subform does not work.

>[!NOTE]
>
>An XDP table without a header row will not be mapped to the adaptive form Table component. Instead, it will be mapped to the adaptive form Panel component with fluid layout. Also, when you add a nested table from an XDP to an adaptive form, the outer table gets converted to a panel while retaining the inner table.

In addition, you can drag-drop a group of XSD complex type elements to create a table row. A new row gets created just below the row on which you dropped the elements. The cells created using the XSD complex type elements maintain a binding reference to the XSD. You can also replace a body cell with an XSD complex type element by dropping the element onto the cell.

>[!NOTE]
>
>The number of elements in a XDP table component, a subform, or an XSD complex type cannot exceed the number of cells in a row. For example, you cannot drop four elements on a row that has only three cells. It will result in an error.
>
>If the number of elements is less than the number of cells in a row, the new row first adds cells based on the elements, and then the default cells are added to fill in the remaining cells in the row. For example, if you drop a group of three elements in a row that has four cells, the first three cells are based on the elements you dropped and the remaining one cell will be the default table cell.

## Key considerations {#key-considerations}

* If you move rows up and down while authoring an XSD-based table, some data loss from table rows is seen in the data XML generated on submitting the form.
* Each body cell in a default table has a predefined element name associated with it. If you add another table in the adaptive form, the default body cells in the new table will have the same element name as in the first table. In such scenario, the data generated on submitting the form will include data in the default body cells of only one of the tables. Therefore, ensure that you rename the element names for default body cells to keep them unique across tables and avoid data loss.  
  
  Note that this is applicable only to the default body cells. If you add more rows or columns to a table will autogenerate unique element names for non-default body cells.
