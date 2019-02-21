---
description: Adding component products to a BOM
---

# BOM Components

After the BOM header is entered and saved, the next step is to add the product components to the BOM. The components are a single layer, meaning if there are sub-components, these will have to be entered as lines on a BOM for their parent products.

{% hint style="info" %}
If a BOM already exists that has the set of products identified or nearly, you can copy it easily by clicking the button _**Copy BOM Lines From**_ at the bottom of the form view.
{% endhint %}

When you create a new record, the following fields are mandatory:

* _**Line No**_ - should default to the next line number, counted by 10
* _**Product**_
* _**Issue Method**_ - see notes below.
* _**Valid From**_ - defaults to the current system date

The other fields will have the following default values:

* _**Component Type**_ - the _**Component Type**_ will default to _Component_
* **Critical Component** _-_ will default to _No_

The following describes the possible settings of the important BOM Component fields and the impacts.

## Product

Select the product component. There are no restrictions on the type of product - it can be any [Product Type](../product-types.md).

## Component Type

The Component Type defines what the component does in the BOM and how it should be treated. The following table outlines the choices and their meaning:

| Component Type | Description |
| :--- | :--- |
| Component | The default. A component is consumed or incorporated into the final product by the manufacturing process. The quantity entered is in UOM selected. |
| By-Product | A product produced as a result of the manufacturing process.  By-Products are treated differently when calculating the rolled-up cost of the BOM and are not included in the final Product costs nor do they absorb a portion of the cost of the production. By-Products are used in Material Resource Planning \(MRP\) to calculate supply. |
| Co-Product | A product that is produced along with the final Product and that will need to be received into inventory when a M**anufacturing Order** is completed.  The _**Quantity**_ consumed must be negative. The Costs of a Co-Product are calculated from a  percentage of the BOM cost using either the _**Cost Allocation Percent**_, mentioned below, or the ratio of the quantity of Co-Product produced versus the qty of final product.  Co-Products are used in Material Resource Planning \(MRP\) to calculate supply. |
| Phantom | A Component of this type, when added to a **Manufacturing Order**, will have its _**Quantity Required**_ amount set to zero and, if the Product has a [default BOM](./#search-key), all the default BOM Components will be added to the Order at the same level with the original _**Quantity Required**_.  This is useful for adding common material and process components to a large number of BOMs while keeping the BOMs rather simple. It also allows the Phantom BOM to be changed independently of all the BOMs that make use of it. |
| Packing | A Packing component quantity is assumed to be per batch when the component is entered on a Manufacturing Order. |
| Tools | A Tools component quantity is assumed to be quantity one per BOM quantity when the component is entered on a Manufacturing Order. |
| Option | A component that will be optionally added to an Order Line when the BOM is "dropped" onto an Order, Invoice or Project.  Option components are not allowed on Manufacturing Orders. |
| Variant | Similar to the _Option_ type but used as a choice of one from several variant Components within a group where the variants share a _**Feature**_. Variant components are not allowed on Manufacturing Orders. |

## UOM

Select the UOM for the component. This can be any valid UOM for the Component Product.

## Attribute Set Instance

This should default to the Product Attribute Set Instance value if one is defined. This represents a template that will be passed to a Manufacturing Order. It is not possible to add Instance values for Product BOM Components. See [Product Attributes, Attribute Sets and Instances](../../product-attributes-sets-and-instances/) for more info.

## Change Notice

Select the Change Notice that relates to this Component. This is a link to a change process describing what was changed and why.

## Valid From/To

The _**Valid From**_ and _**Valid To**_ fields are used to ensure the Component is or will be valid at the time of use. For example, in Manufacturing Orders the dates are tested against the scheduled start date of the manufacturing process before the Component is added to a Manufacturing Order.

## Is Critical Component

A flag that indicates that this component Is Critical. It is not currently used by the Application.

## Is Quantity Percentage

If selected, this indicates that the quantity of the Component will need to be calculated as a percentage of the Quantity Ordered on a Manufacturing Order. When this field is selected, the quantity is entered as a batch quantity percentage. If deselected, the quantity is a quantity per BOM UOM.

## Quantity

The quantity of the component required to create one BOM UOM. This field is shown if the _**Is Quantity Percentage**_ field is not selected.

## Quantity in %

The quantity as a percentage of the Batch Quantity on a Manufacturing Order. This field is shown if the _**Is Quantity Percentage**_ field is selected.

## Cost Allocation Percent

If the _**Component Type**_ is set to _Co-Product_**,** this field will appear. It is used to allocate a percentage of the cost of the BOM to the Co-Product. If the field is left blank, the Cost Allocation Percent is calculated based on the quantity of Co-Product produced.

## Scrap %

Indicates the percentage of the quantity that will become scrap as a result of the manufacturing process. The quantity of the Component to order to fulfill the BOM will be calculated as

$$
QtyToOrder = QtyRequired / (1 - Scrap/100)
$$

where _Scrap_ is the Scrap % value.

## Quantity Assay

A quantity of the component that will be consumed in tests or assay during the manufacturing process. The value is not currently used.

## Issue Method

There are three methods for issuing products to a Manufacturing Order:

| Issue Method | Description |
| :--- | :--- |
| Issue | Indicates that manual material handling processes will be followed to draw material form inventory and provide the component to the manufacturing process.  The component can be issued individually from other components and in partial quantities if necessary. |
| Backflush | The required quantity of the component will be automatically issued to the manufacturing process with no material handling involved.  Components using the Backflush Issue Method can be grouped using the _**Backflush Group**_ field.  This Issue Method is useful where the quantities of the component in stock are high and readily available to the manufacturing process. |
| Floor Stock | The Component will be drawn from Floor Stock with no material handling involved. Floor Stock is an expense account similar to the Product Asset or Inventory account but that represents material that will be consumed in production.  It is used for issue methods such as Kanban where the Kanban locations are filled from inventory and treated as an internal use expense when filled. This "fill" process would remove products from inventory, credit Inventory and debit Floor Stock as an expense.   The _Floor Stock_ Issue Method will allocate this expense to the cost of the BOM Product as debit Work-In-Progress, credit Floor Stock. |

## Backflush Group

This field appears if the _**Issue Method**_ is set to _Backflush._ It is not currently used.

## Lead Time Offset

An optional field, it is used to identify a Lead Time Offset before starting production. It is not currently used.

## Feature

A string field that appears when the _**Component Type**_ is set to _Option_ or _Variant_ and the _**BOM Type**_ is _Product Configure_. The field is used to group similar optional or variant components when performing a BOM Drop or Product Configuration.

## Forecast

A percent number representing the % contribution of this component or variant to planning for the BOM Product. The Forecast field is displayed if the _**BOM Use**_ is set to _Planning._

{% hint style="info" %}
The planning feature using this Forecast field has not been implemented yet.
{% endhint %}

For the purposes of the planning based on a forecast, the BOM Product represents a family of products and the BOM Components are members of that family. The Forecast % is the contribution of each member of the family to the overall demand. For example, if the product family is an automobile with four types based on color, the overall forecast of the demand for the automobile could be broken down as shown in the table below.

| Product | Forecast \(%\) |
| :--- | :--- |
| Automobile Green | 30 |
| Automobile Red | 15 |
| Automobile Blue | 10 |
| Automobile Silver | 45 |

The forecast for the Automobile family could be say, 10,000 vehicles. The Material Resource Planning process would generate demand, procurement and Manufacturing Orders for the four Automobile types and their components according to the Forecast percentage of each.

