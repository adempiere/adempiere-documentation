---
description: >-
  This section is an overview of the Asset Management within ADempiere. For
  background on the terms used, please see Accounting of Assets.
---

# Assets and Asset Management

## Overview

This section is an overview of the Asset Management within ADempiere. For background on the terms used, please see [Accounting of Assets](http://wiki.adempiere.net/Accounting_of_Assets).

The basic approach to assets in ADempiere is that they are specialized products which are amortized over time using a monthly or period process which performs all the necessary calculations. This ensures that all assets are depreciated properly and consistently and takes much of the effort out of depreciation calculations.

### Defining Assets

Essentially, assets are products and are treated like products in every sense. 

Asset related products are bought and sold just like the services or other items but the accounting is managed differently so that the cost of the asset product is capitalized rather then expensed. The accounting of the assets is controlled by the Asset Group for the capital portion and by the Product Category for the product expenses and revenue. These two windows are the starting point for managing assets in ADempiere.

#### Asset Groups

The Product Category and Asset Group are linked on the Product Category page, so the **Assets** [**Asset Groups Window**](http://wiki.adempiere.net/index.php?title=ManPageW_Asset_Groups&action=edit&redlink=1) is the first window to use when defining assets. Each Asset Group defines specific accounting elements to use so the groups should be set up according to the asset reporting structure in the corporate financial statements. For example, in the GardenWorld demo, the financial statements report on the assets using the following categories:

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

The Asset Group also defines the type for depreciation processing to use and the life of assets that are part of the Group. The Building Asset Group defines the depreciation function as [Straight Line](http://wiki.adempiere.net/Accounting_of_Assets#Straight_Line_Method) and the Usable Life as 10 years or 120 periods/months. This means that 10% of the depreciable value of the asset will be expensed as depreciation in each year.

There are a number of possible depreciation functions to choose from that match the most common depreciation schemes in use around the world.

The other key element that can be set in the Asset Group is the Accounting Schema. This allows the accounts and depreciation methods to change from one Schema to another where multiple schema are in use. For example, an accelerated depreciation scheme could be used in one Schema for tax purposes and a basic straight line scheme in another for regulatory reporting.

#### Product Categories

After defining Asset Groups, the Asset Groups need to be matched to Product Categories. When an asset is defined, it is defined using a product and Asset Group. The Product Category used in the definition of the product has to be linked to the Asset Group or it won't be possible to save the Asset record.

> <table>
>   <thead>
>     <tr>
>       <th style="text-align:left"><a href="http://wiki.adempiere.net/File:Note.gif"><img src="http://wiki.adempiere.net/images/6/62/Note.gif" alt="Image:Note.gif"/></a>
>       </th>
>       <th style="text-align:left">
>         <p><b>Note:</b>
>         </p>
>         <p>Create a summary product category for all assets and use this as the parent
>           product category for the asset related product categories. Then in the
>           Product Info window, you will be able to search for all asset related products
>           using the summary category or for specific product assets using the detail
>           categories.</p>
>       </th>
>     </tr>
>   </thead>
>   <tbody></tbody>
> </table>

The **Material Management&gt;Material Management Rules** [**Product Category Window**](http://wiki.adempiere.net/ManPageW_ProductCategory) performs the same function as the Asset Group in that it defines the accounting for product transactions. The key items here are:

* The Parent Product Category - point to the summary category if following that approach.
* The Asset Group - select the matching asset group.

On the Accounting tab, set the accounts as follows:

* The Product Expense account which is used when the asset is first added to the books using the [\#Asset Addition](http://wiki.adempiere.net/Assets_and_Asset_Management#Asset_Addition) process. This account will be charged the equivalent of the net book value of the asset. If moving from asset accounting using a GL, the product expense account could be pointed at a clearing account and a final GL entry could be made to remove the original assets and accumulated depreciation values to balance the clearing account after the asset has been added using the process. If the asset is first managed through the inventory as a purchase of a product, the Product Asset account will be used by the Material Receipt \(unless the product is identified as a "Service" product type - in which case the value will be assigned to the Work In Progress account, if there is a cost collector defined, or the Product Expense account otherwise\). It is recommended that the Product Expense and Product Asset accounts be pointed at the same account.
* The Product Revenue account will be credited on the sale of the asset, assuming an AR invoice is used to make the sale. The invoice line net amount will be considered as the proceeds of the sale. The sale invoice will trigger an [\#Asset Disposal](http://wiki.adempiere.net/Assets_and_Asset_Management#Asset_Disposal) transaction which will debit the Disposal Revenue Account from the Asset Group with the same amount. In most cases the Product Revenue account and Asset Group Disposal Revenue Account should be set to the same account as the net balance should be zero.
* The Product Asset account should point to the same account as the Product Expense Account for the reasons described above.

In the Garden World demo, the Product Category Accounts for the Building Product Category are set up to point at the suspense balancing account:

* Product Asset HQ-79200-\_-\_-\_-\_
* Product Revenue HQ-79200-\_-\_-\_-\_
* Product Expense HQ-79200-\_-\_-\_-\_



#### Defining the Asset Product

Asset products are defined as if they were regular products in the **Material Management&gt;Material Management Rules** [**Product Window**](http://wiki.adempiere.net/ManPageW_Product). The Product Category should be one that was linked with an associated Asset Group. The product should be stocked if it is at all tangible as the value of the asset will be easier to manage through the acquisition and disposal processes. For assets that are tracked by serial numbers, an appropriate Attribute Set should be defined. Also, if the asset product is unique, a specific Attribute Set Instance can be created with a serial number and set on the Product tab.

Next \(optionally\) create the Asset product using the **Assets** [**Asset Window**](http://wiki.adempiere.net/ManPageW_Asset). Give the asset a suitable name and select the matching Asset Group and Product Category. If these are not properly linked on the Product Category, an error will be displayed when you try to save the record. This step is optional because it can be performed automatically by the invoice. Creating the record manually does give more control over the dates.

Set the Create Date to the day the asset was created in the system and set the In Service Date to the day where depreciation will start to apply.

Select "Owned" if the asset is owned by the client organization and considered a capital asset. If the asset is owned, it can also be selected as subject to depreciation.

When the Asset record is saved, the definitions are ready to be used but no accounting has taken place yet. The value of the asset has not been defined and there are no entries in the Accounting Facts.

### Adding Assets

There are two ways to add assets to the balance sheet:

* Manually, using the **Assets&gt;Asset Transactions** [**Asset Addition Window**](http://wiki.adempiere.net/index.php?title=ManPageW_AssetAddition&action=edit&redlink=1)
* Via a Vendor Invoice.

#### Adding Assets with an Invoice

Assets are added when the invoice line has the "Create Asset" button selected and the asset type is identified as a "Capital" asset. If the product is one of many under a single Asset, select the check box "Is Collective Asset" and select the associated Asset.

If an asset is not identified on the line, one will be created from the connection between the Product Category and the Asset Group. The addition of the asset to the books is performed when the Match Invoice record is created following the receipt of the Asset Product. The addition is performed by an Asset Addition document which creates the necessary postings to add the asset to the books.

As an example of the invoice, consider the following scenario:

In the Garden World example, the Fertilizer organization has an Equipment Shed, a large fabric covered structure roughly 450 square meters in size. The shed was purchased about a year ago for $175,000 in a turnkey fashion so all expenses required to make the asset ready for sale were included in that price. The Equipment Shed is owned and will be depreciated according to the "Building" Asset Group settings of a 10 year life using the Straight Line method. For this asset, there is a Product "Equipment Shed" and a Asset "Fertilizer Equipment Storage Shed". The invoice date and asset creation date are about 2 months ahead of the activation date.

For this example, the asset record was created before the invoice. A standard invoice header record was created. The date of the invoice will become the document date of the Asset Addition document. A single invoice line was added as follows:

* The product set to "Equipment Shed"
* "Create Asset" selected
* Asset Type \(Capital/Expense\) set to Capital
* Asset set to the asset product completed above "Fertilizer Equipment Storage Shed"
* Is Collective Asset deselected
* Qty set to One
* Price set to $175,000

When the invoice was completed, the posting is as follows:

| Account | Debit | Credit |
| :--- | :--- | :--- |
| Tax |   $22,750 |  |
| Inventory Clearing | $175,000 |  |
| Accounts Payable |  | $197,750 |

The material receipt of the asset was accomplished with a standard Material Receipt, adding the "building" to the inventory of the Fertilizer organization. The posting on the MR was as follows:

| Account | Debit | Credit |
| :--- | :--- | :--- |
| Suspense Balancing | $175,000 |  |
| Not invoiced receipts |  | $175,000 |

The Matching Invoice record had the following facts:

| Account | Debit | Credit |
| :--- | :--- | :--- |
| Not invoiced receipts | $175,000 |  |
| Inventory Clearing |  | $175,000 |

If the Asset record was not identified on the Invoice Line, the Asset record would have been created based on the Product Category and Asset Group information.

When the Match Inv was created, an Asset Addition record was also created. In addition to the Asset Addition document, a worksheet is created containing all the expected depreciation expenses over the life of the asset and the current asset balances are established.

The accounting fact posting of the Asset Addition are as follows:

| Account | Debit | Credit |
| :--- | :--- | :--- |
| Building | $175,000 |  |
| Suspense Balancing |  | $175,000 |

The net effect of all the postings, removing the cancelling entries, is:

| Account | Debit | Credit |
| :--- | :--- | :--- |
| Tax | $22,750 |  |
| Building | $175,000 |  |
| Accounts Payable |  | $197,750 |

#### Adding Assets Manually

To add an asset to the books manually, without any invoice, simple create the Asset record and then the Asset Addition document and Complete it.

When adding assets in this manner, there are a few additional options to consider.

* The starting values of the capital asset and accumulated depreciation can be set on the Asset Addition record. When using an invoice, the capital asset value is the purchase price and accumulated depreciation is considered zero. To make this adjustment select the checkbox "Adjust Accumulate Depreciation", then fill in the starting values for the accumulated depreciation and set the starting period. The asset depreciation workbook will start at that period and calculate the depreciation to the end of life.
* The quantity of assets can be set to a number other than one. This is useful if a number of items are grouped as a single "asset" but added and disposed of individually or in smaller sets. This is known as a "Collective Asset".

After completing and posting the Asset Addition Document, the undepreciated value of the asset will be posted to the Product Expense account. A General Journal entry may be required to deal with this expense - for example, to reduce an existing asset and accumulated depreciation amounts.

### Depreciating Assets

The automatic depreciation calculations possible in ADempiere make the periodic depreciation calculations and reporting quite simple - almost a button push effort. This is a great time and accuracy savings for those who traditionally handled depreciation calculations on a spreadsheet. The basic process is as follows:

* Open the **Assets&gt; Depreciation Processing** menu, [**Post Depreciation Entry Window**](http://wiki.adempiere.net/index.php?title=ManPageW_PostDepreciationEntry&action=edit&redlink=1).
* Enter the values for the following fields:
  * Organization
  * Document Type - there is only one choice "Asset Depreciation"
  * Posting Type
  * Accounting Schema
  * Document Date/Accounting Date
  * Period
* Save the record.

At this point, you can check the "Records" tab that will show the depreciation expense entries that will be applied that were drawn from all the available asset depreciation workbooks created when the assets were added to the system. If you change any of the values on the header Entry tab, the list of expense records will change.

When satisfied, complete the Depreciation Entry document. When posted, this will debit the depreciation expense account and credit the accumulated depreciation account according to each line in the "Records" tab.

### Disposing of Assets

#### Asset Disposal

