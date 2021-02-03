---
description: How to define Asset Groups and link them to the Product Categories
---

# Asset Groups

ADempiere provides an Asset Management capability that allows users to manage capital assets using standard documents rather than GL Accounting. If you are not going to use the Asset Management module, you can skip this section. For more information, see the section on the [Assets & Asset Management](../../assets-and-asset-management.md).

If you are going to use the Asset Management module, you will need to link Product Categories to the Asset Groups. The Product Category and Asset Group are linked on the Product Category page, so its easier if the Asset Groups exist before the Product Categories are created. The Product Category Accounts referred to here are described in more detail in the [Product Categories](product-categories.md) section.

The **Assets** [**Asset Groups Window**](http://wiki.adempiere.net/index.php?title=ManPageW_Asset_Groups&action=edit&redlink=1) is the first window to use when defining assets. Each Asset Group defines specific accounting elements to use so the groups should be set up according to the asset reporting structure in the corporate financial statements. For example, in the GardenWorld demo, the financial statements report on the assets using the following categories:

* 16 Land and Building
  * 16100 Land
  * 16200 Building
  * 16300 Land Improvements
  * 16400 Building Improvements
  * 16500 Leasehold Improvements
* 17 Furniture, Fixtures & Equipment
  * 17100 Furniture
  * 17200 Fixtures
  * 17300 Equipment
  * 17400 Vehicles
  * 17500 Data Processing Equipment
  * 17600 Software

The Asset Groups are set up in a similar way:

* Buildings
* Furniture
* Fixtures
* Equipment
* Vehicles
* Data Processing Equipment
* Software

Each group relates to a specific set of accounts that are used for the asset accounting for any asset that is part of that group. Again, in the Garden World demo, the accounts for the Buildings Asset Group are:

* Asset Acct HQ-16200-\_-\_-\_-\_
* Accumulated Depreciation Account HQ-18120-\_-\_-\_-\_
* Depreciation Account HQ-67120-\_-\_-\_-\_
* Disposal Revenue Acct HQ-79200-\_-\_-\_-\_
* Disposal Gain Acct HQ-80800-\_-\_-\_-\_
* Disposal Loss Acct HQ-82800-\_-\_-\_-\_

These accounts should be straight forward for most people familiar with a balance sheet with the exception of the Disposal Revenue Account. This account is debited with the proceeds of the disposal of the asset which would normally be a cash account. However, as the sale of the asset will likely involve invoicing and accounts receivable, the Disposal Revenue account should point at a clearing account that will be balanced by the invoice Product Revenue account. For this reason, the Asset Group Disposal Revenue account and Product Category Product Revenue account should be the same clearing account.

The Asset Group also defines the type of depreciation processing to use and the life of assets that are part of the Group. The Building Asset Group defines the depreciation function as [Straight Line](http://wiki.adempiere.net/Accounting_of_Assets#Straight_Line_Method) and the Usable Life as 10 years or 120 periods/months. This means that 10% of the depreciable value of the asset will be expensed as depreciation in each year.

There are a number of possible depreciation functions to choose from that match the most common depreciation schemes in use around the world.

The other key element that can be set in the Asset Group is the Accounting Schema. This allows the accounts and depreciation methods to change from one Schema to another where multiple schema are in use. For example, an accelerated depreciation scheme could be used in one Schema for tax purposes and a basic straight line scheme in another for regulatory reporting.

## Product Categories for Asset Products

After defining Asset Groups, the Asset Groups need to be matched to Product Categories. The next page provides details on setting up Product Categories for non-asset products. Here, the connection between Asset Groups and Product Category accounts are examined in detail.

When an asset is defined, it is defined using a Product and Asset Group. The Product Category used in the definition of the Product has to be linked to the Asset Group or it won't be possible to save the Asset record.

{% hint style="info" %}
Create a summary Product Category for all assets and use this as the Parent Product Category for the asset related Product Categories. Then in the Product Info window, you will be able to search for all asset related products using the summary category or for specific product assets using the detail categories.
{% endhint %}

The **Material Management&gt;Material Management Rules** [**Product Category Window**](http://wiki.adempiere.net/ManPageW_ProductCategory) performs the same function as the Asset Group in that it defines the accounting for product transactions. The key items here are:

* The Parent Product Category - point to the summary category if following that approach.
* The Asset Group - select the matching asset group.

When setting the accounts on the Product Category Accounting tab, there are a few hints.

**It is recommended that the Product Revenue, Product Expense, Product Inventory Clearing, Cost of Goods Sold and Product Asset accounts be pointed at the same account which will function as a clearing account.**

The Product Asset account is used when the asset is first added to the books using the [Asset Addition](../../assets-and-asset-management.md#adding-assets) process via a Vendor Invoice. This account will be credited the equivalent of the net book value of the asset. When the asset is received, the Product Asset account will be debited by the Material Receipt with the same value.

If moving from asset accounting using a GL, the product expense account could be pointed at a clearing account and a final GL entry could be made to remove the original assets and accumulated depreciation values to balance the clearing account after the asset has been added using the Asset Addition process.

Ignoring tax and other adjustments, the relevant postings that occur for the addition of an asset related product appear as follows. If the Asset Product is stocked, the Inventory Clearing account will be used. Otherwise, the Product Expense account. The Product Category accounts are in bold italics. The Asset Addition document is created and completed automatically by the Match Invoice document via the asset model validator.

| Document | Debit Account | Credit Account |
| :--- | :--- | :--- |
| Vendor Invoice | _**Product Expense**_ or _**Inventory Clearing**_ | Accounts Payable |
| Material Receipt | _**Product Asset**_ | Not Invoiced Receipts |
| Match Invoice | Not Invoiced Receipts | _**Product Expense**_ or _**Inventory Clearing**_ |
| Asset Addition | Asset | _**Product Asset**_ |

The end result of these four documents is a capital asset and an equivalent accounts payable.

The Product Revenue account will be credited on the sale of the asset, assuming an AR invoice is used to make the sale. The invoice line net amount will be considered as the proceeds of the sale. The documents and the relevant accounts affected are shown below.

| Document | Debit Account | Credit Account |
| :--- | :--- | :--- |


| Customer Invoice | Accounts Receivable | _**Product Revenue**_ |
| :--- | :--- | :--- |


| Shipment | _**Cost of Goods Sold**_ | _**Product Asset**_ |
| :--- | :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left">Asset Disposal</th>
      <th style="text-align:left">
        <p><em><b>Product Revenue</b></em>,
          <br />Accumulated Depreciation,</p>
        <p>Disposal Loss or Disposal Revenue</p>
      </th>
      <th style="text-align:left">Asset</th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

