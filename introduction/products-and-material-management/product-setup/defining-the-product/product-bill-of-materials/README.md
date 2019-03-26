---
description: Describes the creation and maintenance of a Product Bill of Materials (BOM)
---

# Product Bill of Materials

A Bill of Materials or BOM is a list of raw materials, processes, sub-components and assemblies that describe the product. A BOM is required to manufacture a product. The Product BOM is comprised of a header record with information about the BOM and a number of subordinate lines representing the components used or required. A BOM can range from a simple list to a complex tree of components and processes that turn raw material into the final product.

The BOM has a number of possible uses:

* It can be used to breakdown a product on Orders \(referred to as "exploding" the BOM\).  The Order would be created using one line for the master product but the printed Order and Shipping documents would show the BOM components. In this case, the product would function as a summary product for its components, making it easy to add a number of lines to an order with a single entry.  \(See the note in the [Stocked field in Basic Product Setup ](../basic-product-setup.md#stocked)for more info.\)
* The BOM can be "Dropped" onto an Order, Invoice or Project which has the effect of entering the BOM components as lines on the document.  During this process, options and product configuration are possible.
* In manufacturing, the BOM provides the processes and materials necessary to create the master product.  Manufacturing planning relies on this data to create effective and efficient plans of what needs to be built when to fulfill customer orders.
* For procurement, the BOM converts demand for the master product into demand for its components allowing procurement planning to purchase required material in a timely manner.
* For Engineering, the BOM provides a way to manage the configuration of the product during development prior to manufacturing.
* The BOM also provides cost information and allows costs to be "rolled up" to the parent product.

## Defining a BOM

The BOM is defined in the **Product** window, **BOM** tab. It can also be defined in the **Bill of Materials & Formula** window, which is essentially a copy of the **BOM** tab.

Start by creating a new record. If in the **Product** window, creating the new record will fill in the _**Product**_ field with the parent Product. In the **Bill of Materials & Formula** window, you will need to start by selecting the parent or final Product.

{% hint style="info" %}
If the manufacturing process using this BOM creates other final products, these can be identified in the **BOM Components** by selected _Co-Product as the **Component Type**_ and setting the _**Quantity Required**_ to a negative amount.
{% endhint %}

The system will then fill the following fields with default values taken from the parent Product or set as described:

* _**Attribute Set Instance**_ - the template value from the Product will be used.
* _**Search Key**_ 
* _**Name**_
* _**Description**_
* _**Comment/Help**_
* _**Unit of Measure**_
* _**Valid from**_  - the date will default to the current system date.
* _**BOM Type**_ - will default to _Currently Active_
* _**BOM Use**_ - will default to _Manufacturing_

Additional information about the non-standard fields or special conditions follows.

## Search Key

If you have more than one BOM for this Product, the Search Key will have to be unique for each BOM.

{% hint style="warning" %}

### Default BOM

The BOM where the _**Search Key**_ matches the **Product** _**Search Key**_ will be considered the default BOM for the Product regardless of its _**BOM Type**_ or _**BOM Use**_ settings. This connection with the Search Key is used:

* When the Product appears as a BOM Component on another BOM with _**Component Type**_ set to _Phantom_,  then this BOM is used as the Phantom BOM and is exploded on Manufacturing Orders.
* When doing Product Planning, the Default BOM is used if a specific BOM was not specified for the Product.
* When calculating the costs a Bill of Materials, the default is used if there is no Product Planning record for the product or no BOM specified on that record.
* When automatically creating a Manufacturing Order as part of the resupply process for a Warehouse or from a Project
* When adding a product to a Manufacturing Order where there is no Product Planning record for the matching Organization, Product, Warehouse, Resource on the Order.
* When preparing Distribution Orders.

## Attribute Set Instance

The template of the Product Attribute Set Instance, if one exists, can be changed from this field. It is not possible to set Instance values in the Product BOM. The template applied here will be applied to the resulting products of the BOM. See [Product Attributes, Sets and Instances](../../product-attributes-sets-and-instances/) for more information.

## UOM

The BOM can use any UOM \(Unit of Measure\) valid for the Product - meaning where a Product UOM conversion exists. This is helpful where the units of measure for manufacturing or procurement are different than the units of measure used in sales. See [Units of Measure](../../units-of-measure.md) for more info.

## Change Notice

The _**Change Notice**_ \__\*\*_\_field is used to record the Change Notice that is/was being applied to the BOM. A Change Notice is a way to inform people that need to know about the change as to the reasons and nature of the change.

The Change Notice information is passed to the Manufacturing Order when it is created.

Management of change can be complex. See [Engineering Change Management](../../../../manufacturing/engineering-change-management.md) \(ECM\) for more information. In summary, the need to make a change is identified on Change Request and this change may affect one or more BOMs for the product and its components. The actual change is specified in a Change Notice. The affected BOM is copied to a new record, the new record is modified according to the change, and the Change Notice provides a reference on the new BOM as to what changed, why and who approved it.

## Revision

The _**Revision**_ field provides a reference for revision information. The revision information is passed to the Manufacturing Order when it is created.

## Valid From, Valid To

The _**Valid From**_ and _**Valid To**_ fields are used to ensure the BOM is or will be valid at the time of use. For example, in Manufacturing Orders the dates are tested against the scheduled start date of the manufacturing process.

{% hint style="warning" %}
Valid From/To dates are not used when selecting the "default" BOM. The BOM with the _**Search Key**_ field matching the **Product** _**Search Key**_ is considered the default. If the default BOM is not valid, you may receive errors in some operations, even if a valid BOM exists. See issue [2303 ](https://github.com/adempiere/adempiere/issues/2303)and [2304](https://github.com/adempiere/adempiere/issues/2304).
{% endhint %}

## BOM Type

The _**BOM Type**_ **can be used to describe the purpose of the BOM. There can be typically no more than one** _**BOM Type**_ for each _**BOM Use**_ value and should be only one _Make-To-Order or_ _Make-To-Kit_ type per Product. Allowable values and the uses follow:

| BOM Type | Impacts |
| :--- | :--- |
| Current Active | Indicates that this BOM is the currently active BOM for the _**BOM Use**_ selected. |
| Maintenance | A Maintenance Order will be created for this BOM Type instead of a Manufacturing Order |
| Make To Kit | If it exists with a _**BOM Use**_ of _Manufacturing_, a **Manufacturing Order** will be created, processed and closed when the parent product is added to a **Sales Order**.  See the notes below. |
| Make To Order | Similar to Make To Kit but the created Manufacturing Order will be left at the prepared state and will need to be completed, and processed. See the notes below. |
| Product Configure | The BOM used to configure a product where there are options. For more information, see Product Configuration |
| Repair | Not currently used by the system. |
| &lt;Blank&gt; | Use if the BOM Type is not known. |

## BOM Use

There are five possible settings for the _**BOM Use**_ field.

| BOM Use | Description |
| :--- | :--- |
| Master | The BOM that is the basis for the other copies.  For _**BOM Type**_ _Product Configure,_ it is the BOM displayed in the **Product Configuration BOM** or **BOM Drop** window. |
| Engineering | Can be used to track engineering version and copies of the BOM during development. |
| Manufacturing | Used when the product is manufactured. When associated with _**BOM Type**_ _Make To Kit_ or _Make To Order_, this BOM will be used to create a **Manufacturing Order**. |
| Planning | Not currently used. |
| Quality | Not currently used. |

{% hint style="info" %}
## _Make To Order and Make To Kit_

When an Order is completed, if any product on the order has a BOM with _**BOM Type**_ set to _Make To Kit_ or _Make To Order_, and the _**BOM Use**_ set to _Manufacturing_, then a **Manufacturing Order** will be created automatically to build the products. This applies for all Sales Orders with document types _Standard, Warehouse, On Credit or POS._ The Product must not be [_**Purchased**_](../basic-product-setup.md#purchased-sold).

For **BOM Type** _Make To Kit_, the Manufacturing order will automatically have material issued to it and the final product will be received into inventory. This is useful where the manufacturing process is simple and there is no need for pick lists and other material handling processes.

For **BOM Type** _Make To Order_, the Manufacturing Order created will be prepared \(materials reserved\) but not completed and will need to processed according to the manufacturing workflow.
{% endhint %}

## \_\_

