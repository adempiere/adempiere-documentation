---
description: How to setup and use Product Attributes to extend the product definition.
---

# Product Attributes, Sets and Instances

## The Product Attribute Model

**Attributes** enrich the information about products and provide additional ways in which the products can be defined and managed. The attributes can be thought of as specifications of the product. A collection of attributes is called an **attribute set** and the attribute set is applied to specific products as required. The attribute set can include information on the lot, serial number, and guarantee date of the product.

Product attributes allow the product name and value, fields to be kept short, since the information about the nature of the product can be defined in the attributes.

The attributes can also be used in product searches based on the attribute values. For example, find all resistors in stock that have a rating of 100 kOhms and a rectangular two-terminal surface mount package \(0201\). An electronic manufacturer could easily have tens of different products in inventory that match this search.

Attributes can be defined for a variety of products, be specific to a group of products or specific to a single item. An example of a specific attribute is a serial number. Only one item in the entire inventory of that product will have that serial number attribute. The value of the attribute is called and **Attribute Instance** and the collection of Attribute Instances is an **Attribute Set Instance**.

Attributes and their instances can be defined at the product level as in a specification or at the inventory level. At the product level, these are **Product Attributes** and at the inventory level **Instance Attributes**.

Product attributes are defined by the attribute set applied to the [**Product Window**](http://wiki.adempiere.net/ManPageW_Product). The Attribute Set Instance in the product window sets product level attributes that will be common across all attribute set instances created for that product.

Instance attributes are typically defined at the time that product or item enters or leaves the control of the company, such as at production, material move, inventory counts, material receipts, or material shipments. Instance attributes are associated with items in storage and are tracked on documents that affect these items.

There are three elements of instance attributes that can be assigned to any attribute set:

* a lot number or code
* a serial number
* a guarantee date

Beyond these three, any attribute can be defined as an instance attribute.

Once an Attribute Set Instance is created, it can be searched and tracked through documents via the [**Attribute Set Instance Window**](http://wiki.adempiere.net/ManPageW_AttributeSetInstance).

The Attributes Set Instances can also appear on shipments or material receipts as well.

## Setup

{% hint style="info" %}
For an example of the attributes in use, see [Example - Using Product Attributes.](example-using-product-attributes.md)
{% endhint %}

Before you establish your attributes and attribute sets, you need to define the information that you will need to track for each product and why it is needed. Some examples of how attributes can be required:

* Vendor serial numbers which need to be tracked and used if items are returned
* Vendor shipping code which needs to be tracked
* A lot or product number which needs to be tracked in case of recall
* Manufactured sub-assemblies have serial numbers which are tracked during manufacture
* Final products are assigned serial numbers and these are listed on shipping documents when sent to customers.
* Product attributes are assigned to define product specifications. Products need to be searchable based on the individual attribute values and/or attribute sets. \(For an example of how complex this can get, see [Arrow Electronics Parametric Search](http://components.arrow.com/part/search/^6/11/863)\)
* Guarantee dates that need to be tracked. Items close to expiry need to be located in inventory and put on sale or disposed of.
* Warranty dates based on the date sold

Next, split the information into the product level and instance level information. The product level information will be similar for every instance associated with that product.

For each element of the information, define an attribute using the [**Attribute Window**](http://wiki.adempiere.net/ManPageW_Attribute). In this window you can define the attribute using a name, description and the type of value the attribute will hold. The available choices are:

* List
* String with a max length of 40 characters
* Numeric

If using the List type, you have to define the allowed attribute values on the [**Attribute Value Tab**](http://wiki.adempiere.net/ManPageW_Attribute#Tab:_AttributeValue).

The Attribute Window also has two check box fields:

* Mandatory - indicating the attribute must be set when an inventory transaction takes place. Failure to do so will cause an error/warning when trying to complete the document.
* Instance Attribute - if checked the attribute is an instance attribute which relates to specific instance information. If unchecked, that attribute is a product attribute that relates to product information common to all instances. The product attribute can be changed in the product window.

Once all the attributes are entered, combine them in Attribute Sets in the [**Attribute Set Window**](http://wiki.adempiere.net/ManPageW_AttributeSet). Here you can set the name, description of the attribute set and select the attributes associated with the set. You can also determine if the set contains a lot code, serial number of guarantee date and the parameters that control these. Finally, you can set the controls associated with the set so that its use is mandatory or not. The available options are:

* Always mandatory
* Not Mandatory
* When Shipping

A mandatory attribute set needs to be filled on every document where the product is referred to. If the mandatory type is set to When Shipping, the attribute set needs to be filled on any material shipment document but not on other transactions.

The [**Attribute Use Tab**](http://wiki.adempiere.net/ManPageW_AttributeSet#Tab:_AttributeUse) is used to determine the attributes that are part of the attribute set and the sequence of their appearance on the forms.

The [**Exclude Tab**](http://wiki.adempiere.net/ManPageW_AttributeSet#Tab:_Exclude) can be used to control the mandatory nature of the attribute set by excluding certain tables. This is helpful when attributes are required only on outbound shipping but not on the original purchase, for example.

### Lot Codes

Lot codes are essentially strings and can be manually entered or created and tracked in ADempiere in a way similar to document and sequence numbering.

To create Lot codes as a sequence of numbers, open the [**Lot Control Window**](http://wiki.adempiere.net/ManPageW_LotControl) in **Material Management→Product Attributes**. There you can establish:

* the control name;
* description;
* the starting number of the lot code;
* the increment to use when creating a new code; and
* the prefix and suffix for the codes created.

On the Lot Control window there is also an [**Exclude Tab**](http://wiki.adempiere.net/ManPageW_LotControl#Tab:_Exclude) tab. Identifying a table in this tab will prevent the lot control "New Record" button from appearing on the [Product Attribute Dialog](http://wiki.adempiere.net/Product_Attribute_Dialog) when creating a new attribute set instance.

In the [**Lot Window**](http://wiki.adempiere.net/ManPageW_Lot), you can manage the actual lot codes created using the Product Attribute Dialog and the Lot Control or you can create your own Lot codes and assign them to a product. Here you can add additional information to the lot code such as a description, comment and date-from and date-to limits for the lot. The string Name field is the actual Lot Code. Date From and Date To limits can be used to show only valid lot codes in the Product Attribute Dialog.

When an Attribute Set Instance is created or edited in the Product Attribute Dialog, there are two fields that reference the Lot: **Lot No** and **Lot**. The contents of the **Lot No** field are used in the description of the Attribute Set.

[![Image:ASI\_NewFromTemplate.png](http://wiki.adempiere.net/images/5/52/ASI_NewFromTemplate.png)](http://wiki.adempiere.net/File:ASI_NewFromTemplate.png)

The underlying model has a Lot ID \(M\_Lot\_ID\) which is associated with the lots in the [**Lot Window**](http://wiki.adempiere.net/ManPageW_Lot). This Lot ID is set by the **Lot** combo box. If the Lot Id is not set, the **Lot No** text field will be editable and you can enter the lot number manually. Otherwise, the Lot No field will be read-only and will contain the number/name of the lot selected in the Lot combo box.

{% hint style="info" %}
Text entered directly in the Lot No text field in the Product Attribute Dialog is just a text value in the Attribute Set Instance - it will not appear in the Lot Window.
{% endhint %}

The **Lot No** text field can be used if the Lot Control and Lot window are not required. This may be the case, for example, if tracking the lot numbers on incoming material. In such a case, you could setup the Lot Control to exclude the tables where the Attribute Instances may be set, which would prevent selection of a Lot and encourage or force entry of text in the Lot No field.

**Prefixes and Suffixes for Lot Codes**

The prefixes and suffixes in the Lot Control window can be used to distinguish the lots in the displays of the Attribute Set Instance. The strings in the Prefix and Suffix fields will be used in the lot codes. For example, if the Prefix is "Lot" and the Suffix "E", when creating a new Lot record, say 124, it will be recorded and will appear in the Lot combo box and the Lot No field as "Lot124E".

Further, in the [**Attribute Set Window**](http://wiki.adempiere.net/ManPageW_AttributeSet), there are two prefix and suffix delimiters for Lot identification:

* Lot Char Start Overwrite and
* Lot Char End Overwrite.

By default, these will be the "«" and "»" characters. These characters can be over-written in the description by a **single** character in the Lot Char Overwrite fields. Multiple characters or a single space \(" "\) will be ignored.

For example, if the Lot Char Start/End Overwrite fields are filled with "@" characters, and using the above example of the lot prefix and suffix codes, the display will appear as shown below.

[![Image:ASI\_ShowingPrefixSuffix.png](http://wiki.adempiere.net/images/2/2d/ASI_ShowingPrefixSuffix.png)](http://wiki.adempiere.net/File:ASI_ShowingPrefixSuffix.png)

### Serial Numbers

Serial numbers are the ultimate instance attribute as they should be unique in the life of a product.

Serial Number attributes are essentially similar to Lot numbers with the exception that the serial number only has a text entry option on the Product Attribute Dialog and no combo box to select existing serial numbers from.

To create serial numbers as a sequence of numbers, open the [**Serial No Control Window**](http://wiki.adempiere.net/ManPageW_SerialNoControl) in **Material Management→Product Attributes**. There you can establish:

* the control name;
* description;
* the starting number of the serial number;
* the increment to use when creating a new number; and
* the prefix and suffix for the codes created.

This window behaves identically to the Lot Control window. Note that there is also an [**Exclude Tab**](http://wiki.adempiere.net/ManPageW_SerialNoControl#Tab:_Exclude) tab. Identifying a table in this tab will prevent the serial number control "New Record" button from appearing on the [Product Attribute Dialog](http://wiki.adempiere.net/Product_Attribute_Dialog) when creating a new attribute set instance.

**Prefixes and Suffixes for Serial Numbers**

The prefixes and suffixes in the Serial No Control window can be used to distinguish the serial numbers in the displays of the Attribute Set Instance. The strings in the Prefix and Suffix fields will be used in the display of serial numbers. For example, if the Prefix is "ICX" and the Suffix "-01", when creating a new serial number record, say 104789, it will be recorded and will appear in the serial number field as "ICX104789-01".

Further, in the [**Attribute Set Window**](http://wiki.adempiere.net/ManPageW_AttributeSet), there are two prefix and suffix delimiters for serial number identification:

* Serial Char Start Overwrite and
* Serial Char End Overwrite.

By default, these will be the "\#" and "" characters respectively. These characters can be over-written in the description by a **single** character in the Serial Char Overwrite fields. Multiple characters or a single space \(" "\) will be ignored.

**Assigning Serial Numbers to Product Instances**

In planning the use of serial numbers, consider how the serial numbers are determined for and found on your products.

* Are they defined by the vendors of those product?
* Are they defined in the production process?
* Are they determined by the number on a sticker applied to the product at the time of final assembly?
* Are they chosen at the time from a list of available numbers on a spreadsheet perhaps?
* Is there a bar code associated with the serial number?

Answers to these questions will help in defining when and how the attribute set instances should be defined for the products.

For example, suppose the serial numbers are defined by stickers applied to the products as one of the final steps in the manufacturing process. The serial number control is maintained by the printer of the stickers so it is not required in ADempiere. The stickers come in large sheets. Each assembly station has several sheets and the stickers are applied as part of the product BOM and assembly process. Keeping track of the stickers is not important. Finished goods are placed on a shelf for testing. When moving the products from the assembly area to the testing area, the attribute set instance information is captured on an Inventory Move document generated by the [**Inventory Move Window**](http://wiki.adempiere.net/ManPageW_InventoryMove). An Inventory Move line is created for each \(Qty 1\) product and the Attribute Set Instance To field is filled using the serial number on the sticker. This is accomplished with a bar code scanner which is programmed to read the serial number and add the short-cut codes \(tab, space bar, enter key, F2 and F4\) as required to save the attribute set instance, save the inventory move line record, copy the line and then open the Attribute Set Instance To field again.

### Guarantee Date

The **Guarantee Date**, like the Lot Number, is another instance attribute that applies to a set of instances of a product. Guarantee Dates provide a date that can be calculated when the attribute set instance is created and which can be interpreted in a variety of ways depending on the product. For example, it could be the Best Before date on food products or it could be used to indicate the beginning of a performance guarantee or the end of a trial period.

Guarantee Dates are defined on the [**Attribute Set Window**](http://wiki.adempiere.net/ManPageW_AttributeSet) by selecting the **Guarantee Date** check box. The Guarantee Date can be made mandatory by selecting the **Is Mandatory** check box. If a new attribute set instance is created and a new guarantee date record created, the date will be defined by the **Guarantee Days** field. When the new record is created the resulting date will be Guarantee Days from the current system time.

Guarantee Dates are set in the [**Attribute Set Instance Window**](http://wiki.adempiere.net/ManPageW_AttributeSetInstance) by clicking on the **New Record** button or entering a date in the **Guarantee Date** field.

When the record is saved, the date will appear in the attribute set instance description as a date formatted according to the local language settings. For example: \#101\_«125»\_07/12/2013.

## Assigning Attribute Sets to Products

Attribute Sets are assigned to Products in the [**Product Window**](http://wiki.adempiere.net/ManPageW_Product). By defining an attribute set in the **Attribute Set** field, and attribute set instance can be created in documents that deal with product transactions.

### Setting Product Attribute values

If you need to define product attribute values - attribute instance information common to all items of that product - such as specifications, use the **Attribute Set Instance** field in the Product window and click on the button in the field. This will open the [Product Attribute Dialog](http://wiki.adempiere.net/Product_Attribute_Dialog) where you can set the product attributes that will be used in all instances of that product. This special instance becomes a template that is copied to other instances when the those instances are created. Note that the Product Attribute Dialog will only show the Product Attributes and not the Instance Attributes defined in the attribute set.

The Product Attributes can only be edited in the Product window. When the template is used to create a new instance in a document, the Product Attribute Dialog will show the Product Attributes as read only.

## Setting Instance Attribute Information

Attribute Set Instances are created on documents that deal with product transactions. When a product that has an attribute set defined is entered on a line these documents, the **Attribute Set Instance** field is activated and can be used to create, edit or delete the Attribute Set Instance information.

Clicking the button in the Attribute Set Instance field will open the Product Attribute Dialog which will show the Attribute Instance Values. Here the values can be created as a new record if the **New Record** is selected at the top right.

If the Instance has been created from a Product Attribute Set template, the top right check box will show **Edit Record** instead.

An alternative is to select the Attribute Set Instance from the list of previously created Attribute Set Instances by clicking on the **Select existing record** button. This can be useful if, for example, a number of production runs produce products that all have the same lot and guarantee dates.

If an Attribute Set Instance has been defined, it can be deleted from that field by opening the Product Attribute Dialog and clicking the Cancel button.

### Automatic Selection of Attribute Set Instances

ADempiere uses Attribute Set Instance information to track products in inventory and tries to do so intelligently. For example, if no attribute set instance information is specified on a customer shipment lines, in completing the document, the system will select from the available Attribute Set Instances in inventory and attach this information to the shipping record in the [**Attributes Tab**](http://wiki.adempiere.net/ManPageW_Shipment%28Customer%29#Tab:_Attributes).

If you are going to allow the system to select the attributes in this fashion, be sure to test that the selection matches the process used in handling the inventory.

{% hint style="warning" %}
Certain documents, like the POS Order, will create new instances of attributes regardless of what is in inventory. This may create problems with inventory tracking where products with attribute set instances are sold using a POS. This may be a bug.
{% endhint %}

## Displaying Attribute Set Instance Info on Documents

## Searching Attribute Information

### Attribute Search

### Attribute Instances

### Product Info Window

