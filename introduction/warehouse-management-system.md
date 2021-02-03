# Warehouse Management System

Usually the sales department creates Sales Orders _SO_ using alternative Delivery Rules:

| Delivery Rule |
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

![](../.gitbook/assets/image%20%286%29.png)

![](../.gitbook/assets/image%20%283%29.png)

![](../.gitbook/assets/image%20%288%29.png)



## Distribution Order

Commonly known as _DO_ it feeds from the commitments made out of the Sales Orders based on availability of the line items involved.



