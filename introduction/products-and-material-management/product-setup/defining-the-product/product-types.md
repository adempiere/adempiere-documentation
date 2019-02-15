---
description: Describe the Product Types available when defining products
---

# Product Types

A product may be physical, like an apple, or intangible, like a fee for a service. They can be very simple in concept or a complex assembly of sub-components.  ADempiere uses the product type to determine how the product information should be treated.  Product Types are entered in the Product Window. There are four Product Types available**:**

| **Product Type** | Description |
| :--- | :--- |
| **Expense Type** | A product that may or may not be physical. It may require material handling but it is not tracked in inventory. The purchase of the product creates an expense rather than an increase in inventory value. The Expense Type is used where inventory tracking is not required, for example, in products with low volume, low cost and rapid turnover such as office stationary but where more granularity is required in the financial information than, say, the total cost of Office Supplies.  Expense Type products are usually purchased, rather than sold.  Expense Type products are created in the Expense Type window. |
| **Item** | A physical good, an Item is something that is manufactured, bought, or sold and may be held in inventory \(stocked\).  Items can typically be measured by some physical unit of measure and may have a size and weight. Material handling processes are important and the location of the item in inventory can be tracked.  Costs associated with the item can also be tracked using specific cost methods.  Unlike the other Product Types, which affect the income statement accounts, the Item product type cost affects the balance sheet Inventory \(or Product Asset account\). |
| **Resource** | A Resource is a type of product that is typically limited in availability and controlled with a calendar and schedule.  Resource products are not tracked in inventory.  A consultant, hotel room or a piece of manufacturing equipment would be examples. Resource products are usually sold, not purchased.  Resource products are created in the Resource window.   |
| **Service** | A service product is not tracked in inventory. It can be considered as a fee such as consulting fees or utility costs.  Services are most often expensed but may be included in costs related to work in progress. They can be sold or purchased. |

