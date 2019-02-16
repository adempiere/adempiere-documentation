---
description: >-
  How to define the physical locations used to store inventory and the logistic
  processes used to replenish that inventory.
---

# Warehouse & Locators

The model of logistics in ADempiere is based on a large company with a hierarchy of storage and replenishment warehouses where goods are received from suppliers at some of the warehouses and moved between warehouses to replenish those that do not receive goods directly. 

Each warehouse has a physical location with an address. 

Where the warehouses are located far from each other, there can be a significant period of time where the inventory is in transit from one location to another. In-transit warehouse locations can be defined that keep track of this inventory that has been shipped but not received. The products are recorded in the in-transit warehouse until the receipts have been confirmed.

Inside the warehouse, products are stored in locations called **Locators** defined by Aisle, Bin and Level, a sort of XYZ coordinate system. A single Locator can hold many different products.

Every warehouse needs at least one Locator and one of the Locators should be flagged as the "Default".  This is the locator that will be the default used on documents where a locator is required.   Typically, it would be the location of shipping/receiving in the warehouse.

For a very simple organization with small or no inventory, the minimum requirement is a single warehouse and single locator. Nothing else needs be configured.

For very complex companies, there is a full Warehouse Management System included with ADempiere that will support complex logistical processes. The Warehouse Management System provides ways to create areas and sections in the warehouse data to organize the locators more effectively and processes to manage the flow of material between warehouses.

### Setup and Definition

To setup the basic warehouses, go to **Material Management » Material Management Rules** and open the [**Warehouse & Locators Window**](http://wiki.adempiere.net/ManPageW_WarehouseLocators).

For more complex implementations, see **Warehouse Management** and **Distribution Management**.

### Replenishment Rules

Replenishment Rules help keep the necessary but minimum level of inventory in the warehouse to keep the costs low while also ensuring adequate availability of the products. The rules can be used with a regular process of replenishment planning to reduce the workload of procurement - the answer of the question "What do I need to buy today?".

Within each warehouse, replenishment rules can be established for each product. There are a number of replenishment types included:

* Maintain Maximum Level - Replenishment quantities will be ordered if the inventory level is below the maximum level.
* Reorder Below Minimum Level - Replenishment quantities will be ordered if the inventory level is below the minimum level.
* Replenish Plan Calculated - A Replenishment Plan is used to calculate when and how much material to order.
* Custom - It is possible to define a custom rule in software to calculate the replenishment quantities. The software class is defined in the **Warehouse** window.

### Replenishment Process

The replenishment rules are tested when the [**Replenish Report**](http://wiki.adempiere.net/ManPageR_ReplenishReport) ****is generated. The software that generates the report can also automatically generate the associated documents based on the replenishment rules assigned to the products in the warehouse including Distribution Orders, Inventory Moves, Purchase Orders, or Requisitions.

Where replenishment occurs from a source warehouse rather than procurement, the default source warehouse for the replenishment can be identified in the **Warehouse** window. This can be overridden for each product on the **Replenishment** tab.

### Warehouse Accounting

Each warehouse requires a set of accounts for

* Inventory Adjustment - This account is used to post Inventory value adjustments. 
* Warehouse Differences - The Warehouse Differences Account indicates the account used to record differences identified during inventory counts.
* Inventory Revaluation - The Inventory Revaluation Account identifies the account used to record changes in inventory value due to currency revaluation.

The value of inventory is recorded in the Product Asset account associated with each product.

### 

