---
description: >-
  Each window, form and process uses fields and buttons to display and gather
  data.  This page describes how to use the various types.
---

# Entering Data - Fields and Buttons

Each window that you open in ADempiere will likely provide you with the opportunity to enter data. This article describes the types of fields, buttons and controls that you will come across, the type of data that they will accept and how each of them functions. All the controls are listed below. The most common ones are [String](./#string), [Number](./#number), [Date](./#date) and [Search](./#search).

Several of the fields have helper functions, indicated by an icon/button at the right side of the field. The helper functions can be opened by clicking this icon. They may also open if the entered data is not clear or complete. The helper functions include the Calendar Tool, Calculator Tool, Search and Info windows \(See the Functionality list\), and others.

Unless noted in the field notes, most fields will accept and lose the focus as the &lt;Tab&gt; key is typed on the keyboard. When buttons have the focus, the buttons can be activated by typing the &lt;Space&gt; key. Each field also controls the pop-up menu that appears when the mouse is right-clicked over the field.

Data entered into a field is not processed until the field loses focus or, unless noted in the field notes, the &lt;Enter&gt; key s typed.

The fields and buttons are similar between the Web Application and the Java Client.

## Color

A Color element provides a way to set a color in the database. The Color control appears as a button. Clicking the button will open a color dialog where the color properties can be set. Colors can be selected using the java swing JColorChooser tool.

## Date [![Image:Icon\_Calendar24.png](http://wiki.adempiere.net/images/5/52/Icon_Calendar24.png)](http://wiki.adempiere.net/File:Icon_Calendar24.png)

The Date control maintains data as a time stamp in a format consistent with the locale and language of the user's system. The format definitions follow the Java class [SimpleDateFormat](http://download-llnw.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html). If no default format is found, the JDBC standard will be used "yyyy-MM-dd". Local formats will be converted to contain at least "dd" and "MM" numbers in the format code. Year codes will be increased to at least four digits.

The Date control operates like a text field where data can be input by keyboard entry. The digit being entered is enclosed in blue square brackets and format characters are ignored - just type the numbers.

Alternatively, the [Calendar Tool](http://wiki.adempiere.net/Calendar_Tool) can be opened and used to enter a date.

The pop-up menu displays the following options:

* [![Image:Icon\_VPreference24.png](http://wiki.adempiere.net/images/b/b0/Icon_VPreference24.png)](http://wiki.adempiere.net/File:Icon_VPreference24.png) [Value Preference](http://wiki.adempiere.net/Value_Preference_Dialog)
* [![Image:Icon\_ChangeLog24.png](http://wiki.adempiere.net/images/e/e1/Icon_ChangeLog24.png)](http://wiki.adempiere.net/File:Icon_ChangeLog24.png) [Change Log](http://wiki.adempiere.net/Change_Log)

## Date+Time [![Image:Icon\_Calendar24.png](http://wiki.adempiere.net/images/5/52/Icon_Calendar24.png)](http://wiki.adempiere.net/File:Icon_Calendar24.png)

Date with time control is similar to the [Date](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Date) control but includes the time component with the full timestamp format of yyyy-MM-dd HH:mm:ss. The text field can't be edited directly so you have to click the button to open the [Calendar Tool](http://wiki.adempiere.net/Calendar_Tool) to enter the values.

See [Date](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Date) above for more information.

## FileName [![Image:Icon\_Open24.png](http://wiki.adempiere.net/images/2/2e/Icon_Open24.png)](http://wiki.adempiere.net/File:Icon_Open24.png)

The FileName control is intended to hold a file name that can be found in the local default directories. Clicking the button will open the File Chooser dialog where you can select the file of interest. You can also enter the file name in the text field directly.

## FilePath [![Image:Icon\_Open24.png](http://wiki.adempiere.net/images/2/2e/Icon_Open24.png)](http://wiki.adempiere.net/File:Icon_Open24.png)

Local File Path control is similar to the FileName control but is restricted to a directory path only - no file names. Clicking the button will open the File Chooser dialog where you can select the directory of interest. You can also enter the file path in the text field directly.

## ID [![Image:Icon\_Reset24.png](http://wiki.adempiere.net/images/a/a5/Icon_Reset24.png)](http://wiki.adempiere.net/File:Icon_Reset24.png)

The ID control identifies a specific record in a table using the \*\_ID field. The control uses a [lookup/search](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Search) to identify the record. What appears in the ID control is determined by the Identifier field selection in the [**Column Tab**](http://wiki.adempiere.net/ManPageW_TableandColumn#Tab:_Column) of the [**Table And Column Window**](http://wiki.adempiere.net/ManPageW_TableandColumn) where the \*\_ID field is the key. For example, the Value can be Identifier 1 and Name Identifier 2, appearing as Value\_Name. References \(see the [**Reference Window**](http://wiki.adempiere.net/ManPageW_Reference)\) can also be used to control what is displayed in particular windows/fields.

For most ID columns, the ID control will present a combo box with a list of available values. As you type text in the control, the combo box will drop down and the most likely choice will be selected. Typing &lt;Enter&gt; of selecting the entry with a mouse click will save the data in the field.

If there is an Info window associated with the target table, the icon in the button will change to \([![Image:Icon\_Reset24.png](http://wiki.adempiere.net/images/a/a5/Icon_Reset24.png)](http://wiki.adempiere.net/File:Icon_Reset24.png)\). Text entered in the field will be compared with common columns in the table to find a match. If no match is found, more than one match is found or the button is clicked, the associated Info window will appear. Selecting and confirming a record in the info window will cause the ID field to be filled with the associated ID. Canceling the Info window will clear the ID field. Closing the Info window will have no effect. See [Functionality](http://wiki.adempiere.net/Functionality) for a list that includes the info windows.

The following ID fields behave slightly differently:

* Product ID \([![Image:Icon\_InfoProduct24.png](http://wiki.adempiere.net/images/e/eb/Icon_InfoProduct24.png)](http://wiki.adempiere.net/File:Icon_InfoProduct24.png)\): text typed into the field will be matched with the Name, Value or Search Key and SKU. If a single match is found, the ID field will be filled with that Product ID. If more than one match is found, no matches are found or the text is a wild card "%", then the [Product Info](http://wiki.adempiere.net/Product_Info) dialog will be opened. The ID field will be filled by the selected and confirmed value in the Product Info dialog. Canceling the Product Info dialog will clear the ID field. See [Product Info](http://wiki.adempiere.net/Product_Info) for more information.

The pop-up menu in a Product ID field will display the following entries:

* [![Image:Icon\_Zoom24.png](http://wiki.adempiere.net/images/7/7c/Icon_Zoom24.png)](http://wiki.adempiere.net/File:Icon_Zoom24.png) [Zoom](http://wiki.adempiere.net/Zoom)
* [![Image:Icon\_Refresh24.png](http://wiki.adempiere.net/images/2/2a/Icon_Refresh24.png)](http://wiki.adempiere.net/File:Icon_Refresh24.png) Requery
* [![Image:Icon\_ChangeLog24.png](http://wiki.adempiere.net/images/e/e1/Icon_ChangeLog24.png)](http://wiki.adempiere.net/File:Icon_ChangeLog24.png) [Change Log](http://wiki.adempiere.net/Change_Log)
* [![Image:Icon\_VPreference24.png](http://wiki.adempiere.net/images/b/b0/Icon_VPreference24.png)](http://wiki.adempiere.net/File:Icon_VPreference24.png) [Value Preference](http://wiki.adempiere.net/Value_Preference_Dialog)
* Business Partner ID \([![Image:Icon\_BPartner24.png](http://wiki.adempiere.net/images/a/a1/Icon_BPartner24.png)](http://wiki.adempiere.net/File:Icon_BPartner24.png)\): text typed into the field will be matched with the Name, Value or Search Key. The search will be limited to customers or vendors depending on the nature of the transaction \(IsSOTrx?\) of window on which the ID is found. If a single match is found, the ID field will be filled with that Business Partner ID. If more than one match is found, no matches are found or the text is a wild card "%", then the [Business Partner Info](http://wiki.adempiere.net/Business_Partner_Info) dialog will be opened. The ID field will be filled by the selected and confirmed value in the Business Partner Info dialog. Canceling the Business Partner Info dialog will clear the ID field. See [Business Partner Info](http://wiki.adempiere.net/Business_Partner_Info) for more information.

The pop-up menu in a Business Partner ID field will display the following entries:

* [![Image:Icon\_Zoom24.png](http://wiki.adempiere.net/images/7/7c/Icon_Zoom24.png)](http://wiki.adempiere.net/File:Icon_Zoom24.png) [Zoom](http://wiki.adempiere.net/Zoom)
* [![Image:Icon\_Refresh24.png](http://wiki.adempiere.net/images/2/2a/Icon_Refresh24.png)](http://wiki.adempiere.net/File:Icon_Refresh24.png) Requery
* [![Image:Icon\_InfoBPartner24.png](http://wiki.adempiere.net/images/7/76/Icon_InfoBPartner24.png)](http://wiki.adempiere.net/File:Icon_InfoBPartner24.png) [New Record](http://wiki.adempiere.net/Business_Partner_Dialog)
* [![Image:Icon\_InfoBPartner24.png](http://wiki.adempiere.net/images/7/76/Icon_InfoBPartner24.png)](http://wiki.adempiere.net/File:Icon_InfoBPartner24.png) [Update Record](http://wiki.adempiere.net/Business_Partner_Dialog)
* [![Image:Icon\_ChangeLog24.png](http://wiki.adempiere.net/images/e/e1/Icon_ChangeLog24.png)](http://wiki.adempiere.net/File:Icon_ChangeLog24.png) [Change Log](http://wiki.adempiere.net/Change_Log)
* [![Image:Icon\_VPreference24.png](http://wiki.adempiere.net/images/b/b0/Icon_VPreference24.png)](http://wiki.adempiere.net/File:Icon_VPreference24.png) [Value Preference](http://wiki.adempiere.net/Value_Preference_Dialog)

See [Search](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Search) for more information.

## Image

Image fields can be used to display images that are stored in the database as binary data or linked to a URL. When the Image field is initially displayed, it will appear as a button with the text "-" displayed. Clicking on this button will open an Image dialog which appears as a small window as shown below.

[![](http://wiki.adempiere.net/images/2/2c/ImageDialog.png)](http://wiki.adempiere.net/File:ImageDialog.png)

The dialog has three buttons: the standard Cancel and Confirm, and a small button "-" labeled Select File. Clicking this last button will open a file chooser where you can select an image from the file system. When the image is selected and opened, it will appear in the Image dialog and the button will hold the file name. Clicking Confirm will save the image to the database. Clicking Cancel will delete any image saved in the database and close the window. Closing the window will have no effect.

Once an image is saved in the database, it will appear in the window/tab in place of the button. The image will be sized to fit within a box defined by the column width set for that column in that tab.

Clicking the image again will re-open the Image dialog with the image loaded. To delete the image, click the Cancel button. Clicking the button with the file path/name will open the file chooser where you can select another image. Click Confirm to save that image to the database.

## Integer

The Integer field is a numeric field with no fractional part and a maximum of 10 digits. See [Number](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Number) for more information.

## List

A List appears as a combo box pre-filled with values that you can select. As you type in the box, the combo box will expand to show the best choice based on what you have typed. Type &lt;Enter&gt; to select it, or use the mouse to select the list entry. To set the List field to null, select the blank entry in the list.

See also

* [Search](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Search)

## Location \(Address\) [![Image:Icon\_Location24.png](http://wiki.adempiere.net/images/8/85/Icon_Location24.png)](http://wiki.adempiere.net/File:Icon_Location24.png)

The Location control provides a way to attach an address to a record. The Location control does not accept text directly but the button can receive the focus and can be activated from the keyboard by typing &lt;Space&gt;. You can also click on the button \([![Image:Icon\_Location24.png](http://wiki.adempiere.net/images/8/85/Icon_Location24.png)](http://wiki.adempiere.net/File:Icon_Location24.png)\). This will open the Location Dialog where you can specify the full address.

[![](http://wiki.adempiere.net/images/2/29/LocationAddress.gif)](http://wiki.adempiere.net/File:LocationAddress.gif)

When the Location Dialog is closed, the Location control will display a summary of the address information entered.

There is no way to fully clear the Location control once data has been entered. The pop-up menu item Delete will delete the record by clearing the entry and will open the Location Dialog. Canceling the dialog will only clear some of the information, leaving defaults in place.

The pop-up menu \(right-click\) provides options to:

* [![Image:Icon\_Delete24.png](http://wiki.adempiere.net/images/a/af/Icon_Delete24.png)](http://wiki.adempiere.net/File:Icon_Delete24.png) Delete
* [![Image:Icon\_ChangeLog24.png](http://wiki.adempiere.net/images/e/e1/Icon_ChangeLog24.png)](http://wiki.adempiere.net/File:Icon_ChangeLog24.png) [Change Log](http://wiki.adempiere.net/Change_Log)

## Locator \(WH\) [![Image:Icon\_Locator24.png](http://wiki.adempiere.net/images/a/a1/Icon_Locator24.png)](http://wiki.adempiere.net/File:Icon_Locator24.png)

The Warehouse Locator field displays the key field of a warehouse location. Both the field and the button will accept the focus.

Text typed into the Locator field will be compared to valid locations already defined. If the window already references a warehouse or a product, the locator entries will be limited to valid values for these references. If a single match is found, it will be used. If the text consists of a single percent symbol \(wildcard %\), no results are returned or more than one result is found, then the Locator Dialog is opened as shown below.

[![](http://wiki.adempiere.net/images/c/c1/LocatorDialog.png)](http://wiki.adempiere.net/File:LocatorDialog.png)

The Locator Dialog can be used to select an existing Locator reference or define a new one. If a new entry is defined, the Key value will be used to identify it in the Locator field.

The pop-up menu \(right-click\) provides options to:

* [![Image:Icon\_Zoom24.png](http://wiki.adempiere.net/images/7/7c/Icon_Zoom24.png)](http://wiki.adempiere.net/File:Icon_Zoom24.png) [Zoom](http://wiki.adempiere.net/Zoom) to the [**Warehouse & Locators Window**](http://wiki.adempiere.net/ManPageW_WarehouseLocators)
* [![Image:Icon\_Refresh24.png](http://wiki.adempiere.net/images/2/2a/Icon_Refresh24.png)](http://wiki.adempiere.net/File:Icon_Refresh24.png) Requery the field
* [![Image:Icon\_ChangeLog24.png](http://wiki.adempiere.net/images/e/e1/Icon_ChangeLog24.png)](http://wiki.adempiere.net/File:Icon_ChangeLog24.png) View the [Change Log](http://wiki.adempiere.net/Change_Log)

## Memo

The Memo field will accept character strings up to 2000 characters. It is similar to the [Text](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Text) and [String](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#String) fields with the exception that it uses a text area with 80 columns width and a height of 50 rows and can't be encrypted. If the text in the field exceeds the size of the text area on the screen, scroll bars will appear.

The memo field will accept the focus but &lt;Tab&gt; characters will be entered as text. Use &lt;Ctrl&gt;&lt;Tab&gt; or &lt;Ctrl&gt;&lt;Shift&gt;&lt;Tab&gt; to change the focus.

Typing &lt;Escape&gt; will reset the text to its previous value.

The pop-up menu includes a single entry. If the Column name is "Script", the pop-up will point to the [Script](http://wiki.adempiere.net/Script_Editor_Tool) editor. Otherwise, it will point to the text [Editor](http://wiki.adempiere.net/Text_Editor_Tool).

## Printer Name

The Printer Name field is a [String](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#String) field. See [String](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#String) for more information.

## Product Attribute [![Image:Icon\_PAttribute24.png](http://wiki.adempiere.net/images/c/ca/Icon_PAttribute24.png)](http://wiki.adempiere.net/File:Icon_PAttribute24.png)

The Product Attribute field or Product Attribute Instance is a field dedicated to selecting or displaying a specific instance of [Product Attributes](http://wiki.adempiere.net/Product_Attributes). It appears as a text field with an icon/button \([![Image:Icon\_PAttribute24.png](http://wiki.adempiere.net/images/c/ca/Icon_PAttribute24.png)](http://wiki.adempiere.net/File:Icon_PAttribute24.png)\). The text field will not accept the focus but the button will. You can double click the field or click the button to activate the helper function and open the [Product Attribute Dialog](http://wiki.adempiere.net/Product_Attribute_Dialog).

[![](http://wiki.adempiere.net/images/a/a5/PAttributeDialog.png)](http://wiki.adempiere.net/File:PAttributeDialog.png)

The dialog displays the details of the product attribute instance. There are two controls:

* New Record \(or Edit Record\) - New is used when adding items to inventory. Edit is used to modify attributes on an order.
* Select an Existing Record - Used to select an existing attribute instance from inventory.

The other fields that appear depend entirely on how the [Product Attributes](http://wiki.adempiere.net/Product_Attributes) are defined.

The pop-up menu for the field will have entries to

* [![Image:Icon\_Zoom24.png](http://wiki.adempiere.net/images/7/7c/Icon_Zoom24.png)](http://wiki.adempiere.net/File:Icon_Zoom24.png) [Zoom](http://wiki.adempiere.net/Zoom)
* [![Image:Icon\_ChangeLog24.png](http://wiki.adempiere.net/images/e/e1/Icon_ChangeLog24.png)](http://wiki.adempiere.net/File:Icon_ChangeLog24.png) [Change Log](http://wiki.adempiere.net/Change_Log)

See [Product Attributes](http://wiki.adempiere.net/Product_Attributes) for more information.

## Quantity [![Image:Icon\_Calculator24.png](http://wiki.adempiere.net/images/d/db/Icon_Calculator24.png)](http://wiki.adempiere.net/File:Icon_Calculator24.png)

The Quantity field is a numeric field with a maximum of 12 digits in the fractional part and 28 digits in the integer part. See [Number](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Number) for more information.

## RowID

The Row ID Data Type is currently not active in the database.

## Search [![Image:Icon\_Reset24.png](http://wiki.adempiere.net/images/a/a5/Icon_Reset24.png)](http://wiki.adempiere.net/File:Icon_Reset24.png)

A Search Field is used to look up data. The Search field appears as a combo box with a list of available values. The text field will accept the focus but the button can only be operated by the mouse.

As you type text in the control, the combo box will drop down and the most likely choice will be selected. Typing &lt;Enter&gt; of selecting the entry with a mouse click will save the data in the field.

Text entered in the field will be compared with common columns in the table to find a match. If no match is found, more than one match is found or the button is clicked, the associated Info window will appear. Selecting and confirming a record in the info window will cause the ID field to be filled with the associated ID. Canceling the Info window will clear the ID field. Closing the Info window will have no effect.

There are a few special cases:

* If the column name ends in "\_ID", it is treated as an [ID Field](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#ID). There are special cases for these as well. See the [ID](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#ID) field for more info.
* If there is an Info window associated with the column name, that info window will be used to perform the search. See [Functionality](http://wiki.adempiere.net/Functionality) for a list that includes the info windows.
* If none of the above, a generic [Lookup](http://wiki.adempiere.net/Lookup) form will be used.

The pop-up menu \(mouse right-click\) will have the following options:

* [![Image:Icon\_Zoom24.png](http://wiki.adempiere.net/images/7/7c/Icon_Zoom24.png)](http://wiki.adempiere.net/File:Icon_Zoom24.png)[Zoom](http://wiki.adempiere.net/Zoom)
* [![Image:Icon\_Refresh24.png](http://wiki.adempiere.net/images/2/2a/Icon_Refresh24.png)](http://wiki.adempiere.net/File:Icon_Refresh24.png) Requery
* [![Image:Icon\_VPreference24.png](http://wiki.adempiere.net/images/b/b0/Icon_VPreference24.png)](http://wiki.adempiere.net/File:Icon_VPreference24.png) [Value Preference](http://wiki.adempiere.net/Value_Preference_Dialog)
* [![Image:Icon\_ChangeLog24.png](http://wiki.adempiere.net/images/e/e1/Icon_ChangeLog24.png)](http://wiki.adempiere.net/File:Icon_ChangeLog24.png) [Change Log](http://wiki.adempiere.net/Change_Log)

See also

* [List](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#List)
* [ID](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#ID)
* [Table](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Table)
* [Table Direct](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Table_Direct)
* [Lookup](http://wiki.adempiere.net/Lookup)

## String

String fields are one of the most common types of fields in the database. A String is simply a sequence of up to 2000 characters but it is intended for shorter amounts of information.

The String field appears as a simple text field. It can accept and lose the focus with the &lt;Tab&gt; key. The &lt;Escape&gt; key will reset the value. It can be encrypted, like a password, if necessary and can have an "auto complete" feature enabled. It can also have special formatting applied.

The pop-up menu \(right-click\) provides options to:

* [![Image:Icon\_Edit24.png](http://wiki.adempiere.net/images/8/87/Icon_Edit24.png)](http://wiki.adempiere.net/File:Icon_Edit24.png) [Editor](http://wiki.adempiere.net/Text_Editor_Tool) \(Launches a text editor. Appears if the string length is greater than the displayed length.\)
* [![Image:Icon\_VPreference24.png](http://wiki.adempiere.net/images/b/b0/Icon_VPreference24.png)](http://wiki.adempiere.net/File:Icon_VPreference24.png) [Value Preference](http://wiki.adempiere.net/Value_Preference_Dialog)
* [![Image:Icon\_ChangeLog24.png](http://wiki.adempiere.net/images/e/e1/Icon_ChangeLog24.png)](http://wiki.adempiere.net/File:Icon_ChangeLog24.png) [Change Log](http://wiki.adempiere.net/Change_Log)

## Table

The Table data field uses a reference to look up data in a table. It behaves like the [ID](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#ID) and [Search](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Search) fields. See [Search](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Search) for more information.

## Table Direct

The Table Direct data field uses a default reference to look up data in a table. It works best for tables that have defined Info windows. It behaves like the [ID](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#ID) and [Search](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Search) fields. See [Search](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Search) for more information.

## Text

The Text data field is used for character strings up to 2000 characters long. It appears as a text area. It will be 2 rows high if the field length is less than 300 and three rows high otherwise. It is very similar to the [Memo](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Memo) field.

The pop-up menu includes the following options:

* [![Image:Icon\_Edit24.png](http://wiki.adempiere.net/images/8/87/Icon_Edit24.png)](http://wiki.adempiere.net/File:Icon_Edit24.png) Script Editor - if the column name is "Script" or ends with "\_Script". This will open the [Script Editor Tool](http://wiki.adempiere.net/Script_Editor_Tool)
* [![Image:Icon\_Edit24.png](http://wiki.adempiere.net/images/8/87/Icon_Edit24.png)](http://wiki.adempiere.net/File:Icon_Edit24.png) Editor - if not a Script. This will open the [Text Editor Tool](http://wiki.adempiere.net/Text_Editor_Tool)

See also

* [Memo](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Memo)
* [String](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#String)
* [Script Editor Tool](http://wiki.adempiere.net/Script_Editor_Tool)
* [Text Editor Tool](http://wiki.adempiere.net/Text_Editor_Tool)

## Text Long

The Text \(Long\) field is intended for Text &gt; 2000 characters in length. It is interpreted and presented as HTML text.

The pop-up control includes the following items:

* [![Image:Icon\_Edit24.png](http://wiki.adempiere.net/images/8/87/Icon_Edit24.png)](http://wiki.adempiere.net/File:Icon_Edit24.png) Editor - which brings up a rudimentary [HTML Editor Tool](http://wiki.adempiere.net/HTML_Editor_Tool)
* [![Image:Icon\_ChangeLog24.png](http://wiki.adempiere.net/images/e/e1/Icon_ChangeLog24.png)](http://wiki.adempiere.net/File:Icon_ChangeLog24.png) [Change Log](http://wiki.adempiere.net/Change_Log)

See also:

* [Memo](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Memo)
* [String](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#String)
* [Text](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Text)

## Time [![Image:Icon\_Calendar24.png](http://wiki.adempiere.net/images/5/52/Icon_Calendar24.png)](http://wiki.adempiere.net/File:Icon_Calendar24.png)

The Time control is similar to the [Date](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Date) control but only shows the time component in the local format similar to h:mm:ss z or HH:mm:ss z. The text field can't be edited directly so you have to click the button to open the [Calendar Tool](http://wiki.adempiere.net/Calendar_Tool) to enter the values.

See [Date](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Date) above for more information.

## URL [![Image:Icon\_Online24.png](http://wiki.adempiere.net/images/0/0a/Icon_Online24.png)](http://wiki.adempiere.net/File:Icon_Online24.png)

The URL behaves like a [Text](http://wiki.adempiere.net/Entering_Data_-_Fields_and_Buttons#Text) field with an added helper function \([![Image:Icon\_Online24.png](http://wiki.adempiere.net/images/0/0a/Icon_Online24.png)](http://wiki.adempiere.net/File:Icon_Online24.png)\). When you click the button, the software will attempt to open the text as a URL using the default browser on the system.

The pop-up menu \(right-click\) provides options to access:

* [![Image:Icon\_Edit24.png](http://wiki.adempiere.net/images/8/87/Icon_Edit24.png)](http://wiki.adempiere.net/File:Icon_Edit24.png) [Editor](http://wiki.adempiere.net/Text_Editor_Tool)
* [![Image:Icon\_VPreference24.png](http://wiki.adempiere.net/images/b/b0/Icon_VPreference24.png)](http://wiki.adempiere.net/File:Icon_VPreference24.png) [Value Preference](http://wiki.adempiere.net/Value_Preference_Dialog)
* [![Image:Icon\_ChangeLog24.png](http://wiki.adempiere.net/images/e/e1/Icon_ChangeLog24.png)](http://wiki.adempiere.net/File:Icon_ChangeLog24.png) [Change Log](http://wiki.adempiere.net/Change_Log)

## Yes-No

The Yes-No control appears as a Check Box.[![](http://wiki.adempiere.net/images/e/ef/Yes-no.png)](http://wiki.adempiere.net/File:Yes-no.png)

Checking the box is equivalent to Yes. Deselecting the box is equivalent to No. The data is saved in the database as the corresponding letter "Y" or "N".

The pop-up menu \(right-click\) provides options to access:

* [![Image:Icon\_ChangeLog24.png](http://wiki.adempiere.net/images/e/e1/Icon_ChangeLog24.png)](http://wiki.adempiere.net/File:Icon_ChangeLog24.png) [Change Log](http://wiki.adempiere.net/Change_Log)

