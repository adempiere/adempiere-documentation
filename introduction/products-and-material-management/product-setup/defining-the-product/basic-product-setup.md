---
description: How to configure a basic product.
---

# Basic Product Setup

For details on the various fields, see the Manual for the Product Window. This page won't go into all of them, just the ones that are not standard.

## Product Fields

### The Key Identifiers: Value, Name, UPC and SKU

A Product appears in windows and forms using a lookup editor that displays the identifier for the Product, usually its value and name together. When you need to enter a product in the editor, the editor tries to match the data entered with one of the four key identifiers: the Value, Name, Universal Product Code \(UPC\) or Stock Keeping Unit \(SKU\). For users who are familiar with the products and can memorize one of these, its a simple matter to enter the data.

A laser scanner can also be used to populate the editor from a label on the product using one of these fields. If you are using a laser scanner, setup one of these fields to match the output of the scanner.

The goal should be to enable users and scanners to uniquely identify the product with a simple entry. If the entry is ambiguous and relates to more than one product, the Product Info window will appear. While helpful, this takes time and can quickly become annoying if entering large amounts of data.

### Version Number

A reference field, the version number of the Product is used when assets are delivered. The Version Number is copied to the Asset.

### Groups, Classes, Classifications and Categories

These fields are helpful for summarizing reports. See [Product Categories](../product-categories.md) and [Product Classifications, Classes and Groups](../product-classifications-classes-and-groups.md) for more info. The Product Category is mandatory.

### Summary Level

The Summary Level field is intended to allow a tree of products to be defined and used in reporting. Where the summary level product is identified in a report, the results will be based on the child products. The Summary Level field can be set in the Product window but the selection of child products is done in the Tree Maintenance window. See [Trees and Tree Maintenance](../../../system-administration/general-rules/system-settings.md#trees-and-tree-maintenance) for more info.

### Tax Category

Select the appropriate Tax Category. See the description of [Taxes Setup](../../../accounting-and-performance-analysis/tax-setup.md) for more information about the Tax Category.

### Tax Type

Part of the Global Tax Management menu, the Tax Type field is not used in the core system but is available if you need to develop a Global Tax Management system to treat complex tax cases. Some Localizations may use this field.

### Revenue Recognition

Select the appropriate Revenue Recognition type. This field only appears if the Product is sold. The field is currently for reference only. See [Revenue Recognition](../../../revenue-recognition.md) for more info.

### UOM

Enter the UOM in which the product will be stored. This needs to be the smallest UOM that will be used for the Product. See [Units of Measure](../units-of-measure.md) for more information about using UOMs and the conversion from one to the this "Product" UOM.

### Company Agent

The sales rep or User responsible for this product. Used for reference only.

### Product Type

Select the appropriate product type. See [Product Types](product-types.md) for more information about the possible choices.

### Mail Template

The mail template is used when this Product relates to an Asset or Item that can be delivered by e-mail as a URL to a download location. The mail template can be used to provide information about the product or to asset. The Mail Template is used in the Asset Delivery process to deliver customer assets electronically.

### Weight

Enter the weight of the product. This field only appears if the Product Type is "Item". The weight is used in calculating the total weight of an order or shipment, in estimating the cost of shipping or applying landed costs. There are no units for the Weight so you will need to have a system wide definition for which unit to use.

### Volume

Enter the volume of the product. This field only appears if the Product Type is "Item". The volume is used in calculating the total volume of an order or shipment, in estimating the cost of shipping or applying landed costs. There are no units for the Volume so you will need to have a system wide definition for which unit to use.

### Freight Category

Select the appropriate Freight Category. The Product Freight Category is used in the order and shipping documents to determine which Shipper to use and the estimated costs of the shipment based on the product weight. Freight Categories are defined in the Freight Category window and Shippers in the Shipper window. Each Shipper can be associated with a number of Freight Categories. The actual Shipper used and the final Freight Category are set on the Shipping document.

### Drop Shipment

Select this field if the product can be drop shipped \(sent direct from the vendor to the customer.\) For reference only.

### Stocked

Select if the product is to be held and tracked in inventory. This field will only appear if the Product Type is "Item".

{% hint style="info" %}
On an Invoice or Order, non-stocked products that have a BOM will have the BOM tree "exploded" - meaning expanded - when the document is prepared. In this case the BOM line products will be added to the document as if they were additional products. The BOM _**Valid From**_ and _**Valid To**_ dates must agree with the document date, _**Date Promised**_ for orders and _**Date Invoiced**_ for invoices, and the BOM _**Search Key**_ field needs to match the Product _**Search Key**_ field. See [Product Bill of Materials](product-bill-of-materials/) for more information.
{% endhint %}

### Locator

The default location for the product in storage. This field will only appear if the item is Stocked. This is the Locator that will be used when the product is first added to a Material Receipt Line IF the Locator Warehouse and the Warehouse identified on the Material Receipt are the same. If they Warehouses are different, the default Locator for the Warehouse will be used.

For Production Light, if the Production header is created from an Order Line, the Product Locator will be used. When the Production BOM is created, the BOM line products will also use the Product Locator.

Other than setting default values in a few documents, this field does not control the location in storage at all.

{% hint style="info" %}
Note that the Locator used for reservations and orders will always be the default locator for the warehouse.
{% endhint %}

### Shelf Width, Shelf Height, Shelf Depth, Units Per Pallet

These fields provide information about how the Product fits into inventory locations. The fields are not used other than for information and reference.

### Bill of Materials, Verify BOM, Verified

If a Bill of Materials \(BOM\) is defined on the BOM tab of the Product Window, the Bill of Materials checkbox will be selected and the Verify BOM button and Verified checkbox will be visible. After the BOM is entered, you can click the Verify BOM button and the system will check the BOM products and processes making sure there are no recursive products in the BOM tree. Once the BOM has been verified, the Verified checkbox will be selected.

{% hint style="warning" %}
Any BOM defined for the product will not be available to use unless the Verify BOM process is completed and the Verified checkbox is selected.
{% endhint %}

### **Print detail records on invoice**

This field appears if the Product has a BOM. If selected, the contents of the BOM will be added to the Invoice print out, not as new line items but as details of the master product. This does not affect the invoice document - no lines are added. It only affects the invoice Print or Print Preview output.

{% hint style="warning" %}
If the product has multiple BOMs, all of the BOM lines will be printed on the Invoice, even the inactive ones. See issue [2305](https://github.com/adempiere/adempiere/issues/2305).
{% endhint %}

### **Print detail records on pick list**

This field appears if the Product has a BOM. If selected, the BOM details will be added to the Pick List for the Product. This does not affect the shipment document - no lines are added. It only affects the Pick List Print and Print Preview output.

The same caution as for _**Print detail records on invoice**_ applies.

### Purchased, Sold

These fields indicate if the Product is purchased or sold or both. As a rule of thumb, if the product is not purchased but is sold, it must be manufactured and will usually have a BOM associated with it. On the other hand, if the product is purchased but not sold, it will usually be consumed somehow, typically as a component in another product.

The Purchased flag is used when calculating replenishment plans. Requisitions are created for purchased products.

{% hint style="warning" %}
If the Product is purchased and also has a BOM, the behavior is not consistent across all replenishment processes. In some cases a requisition will be generated instead of a manufacturing order. In others, the manufacturing order will come first. See [issue 2286](https://github.com/adempiere/adempiere/issues/2286).
{% endhint %}

The Sold field is not used much. It is used to limit the display of products in the Point of Sale \(POS\) and web store. Otherwise, it is for reference only.

{% hint style="info" %}
The real control on whether a product is purchased or sold is the Price List. If the Price List has "Sales Price List" selected, then products on the list can be sold. If not, the products on the price list can be purchased. Sales orders only use sales price lists and purchase orders don't. Any product, regardless of the settings of "Purchased" or "Sold" can be added to any price list.
{% endhint %}

{% hint style="info" %}
The rules of Purchased/Sold do not apply to Counter Docs - documents that are automatically created to balance processes. For example, inter-organizational invoices where one organization purchases a product from another organization within the same client.
{% endhint %}

### Discontinued

The Discontinued field shows if the product will no longer be produced or purchased. When a product is discontinued, it will not appear in the POS. When the field is selected, the User who made the change is recorded.

### Expense Type

If the Product Type is set to "Expense type", the Expense Type field will appear and will contain the related Expense Type. Expense Type products are not created in the Product Window but can be viewed. They are created in the Expense Type window.

### Resource

If the Product Type is set to "Resource", the Resource field will appear and will contain the related Resource. Resource products are not created in the Product Window but can be viewed. They are created in the Resource window.

### Subscription Type

Enter the Subscription Type. Subscription Types are created and managed in the Subscription Type window. The value is for reference only. Subscription management has not been implemented. See [issue 411](https://github.com/adempiere/adempiere/issues/411).

### Exclude Auto Delivery

Select to exclude this product from Auto Delivery via a process. Auto delivery can occur if the Customer \(Business Partner\) has a Delivery Rule other than "Manual". Selecting Exclude Auto Delivery on the Product window will prevent automatic delivery of this product. This is useful where the product is sensitive, potentially dangerous or stock levels are likely to be insufficient. A product that should be excluded from air freight would be a good example.

The Exclude Auto Delivery flag is ignored if the Business Partner Delivery Rule is "Force" or if the Order is one of the following document types, all of which over-write the Delivery Rule with "Force":

* On Credit Order,
* Warehouse Order,
* POS Order, or
* Prepay Order.

### Image URL and Description URL

The Image URL and Description URL are used in the Web Store. The Image URL is used to display the image of the product and the Description URL is used as a link for the Product Name.

### Guarantee Days and Min Guarantee Days

These numbers are used to calculate the Good For Days, Shelf Life Days and Shelf Life Remaining values shown in the Attribute Instance dialog.

The Good For Days \(GFD\) is calculates as

$$
GFD = DaysBetween(ASI.GuaranteeDate, SysDate) - MGD
$$

where ASI.GuaranteeDate is the Guarantee Date of a particular Attribute Set Instance of this Product, SysDate is the current system date and MGD is the Product Min Guarantee Days.

The Shelf Life Days \(SLD\) is simply

$$
SLD = DaysBetween(ASI.GaranteeDate, SysDate)
$$

and Shelf Life Remaining Percent \(SLRP\) is

$$
SLRP = 100*DaysBetween(ASI.GuaranteeDate, SysDate)/GD
$$

where GD is the Product Guarantee Days and GD &gt; 0. If GD &lt;= 0 the SLRP is shown as 0.

### Attribute Set and Attribute Set Instance

Enter the Attribute set used by the product and the template Attribute Set Instance. The Attribute Set Instance field will not be enabled until the Attribute Set field has a suitable value.

For more information about these fields, see [Product Attributes, Sets and Instances.](../product-attributes-sets-and-instances/)

### Featured in Web Store

This field should be selected if the product will be shown in the Web Store by default. The product must also have the Is Self-Service field selected and meet the requirements of that field. Products that are not selected as part of the Web Store but that are on the same price list and that have the Is Self-Service field selected can be shown in the Web Store Shopping Basket.

### Self-Service

Selecting the field is required to display the product in the Web Store, by default if the field Featured in Web Store is also selected. The product must also be Active, Sold and be on a suitable price list with a Standard Price greater than zero.

## Copying a Product

After the basic product fields are generated here, if the product is similar to another product, the Copy From Product button at the bottom of the form can be used to copy a number of the subordinate tab data from that product to this one.

The current Product record needs to be saved. When you click the Copy From Button, a dialog will appear where you can select the source product. Click the Confirm button and the following data will be copied from the selected product:

* Product Prices
* Substitutes
* Related Products
* Warehouse Replenishment Rules
* Product Business Partner Info
* Product Download Info

{% hint style="info" %}
Note that the Copy From Product process does not fill in any of the Product Tab fields and doesn't change the Accounting
{% endhint %}

