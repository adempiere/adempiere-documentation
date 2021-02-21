# Warehouse Management System

Usually the sales department creates Sales Orders _SO_ using alternative Delivery Rules:

| **Delivery Rule** |
| :--- |
| Full Line Delivery |
| Full Order Delivery |

## Distribution Plan

This report comes out of executing a standard process, basically shows current status of items to be delivered, it allows to consolidate commitments from previous orders in order to generate a delivery plan, this in turn allows to create Outbound Orders based on the items to be delivered.

![Input Parameters for Delivery Plan Report](../.gitbook/assets/image%20%284%29.png)

![Delivery Plan Report](../.gitbook/assets/image%20%285%29.png)

Important data is obtained from this report, such as delivery date, source warehouse, customer, quantity, among others.

## Generate Outbound Order

The user generates a picking list through an Outbound Order _OO_ using several criteria based on demand or open sales orders. It is important to mention the key parameters chosen here refer to common criteria that makes delivery possible, for example: Promised Date range, Document Type, Sales Region.

![Generate Outbound Order Selection Criteria](../.gitbook/assets/image%20%286%29.png)

![Record Selection Preview from Order Lines](../.gitbook/assets/image%20%283%29.png)

![Generated Outbound Order Example](../.gitbook/assets/image%20%2816%29.png)

![Outbound Order Line Detail](../.gitbook/assets/image%20%2819%29.png)

You may notice there are different sales order lines reference in an outbound order, This is because their focus is to ease deliveries across several criteria, for example a distribution route and/or fulfilling truck capacity.

![Release Outbound Order to Pick](../.gitbook/assets/image%20%2817%29.png)

As we reach one of the critical steps in this process, this is the Release Outbound Order to Pick that generates the pick tickets and indicates the picking list and the location of the items.

## Distribution Order

The pick tickets that were created on the previous steps will now show up as distribution orders

![Distribution Order from Pick Ticket](../.gitbook/assets/image%20%2818%29.png)





