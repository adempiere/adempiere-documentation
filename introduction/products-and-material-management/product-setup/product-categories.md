---
description: How to use the Product Categories
---

# Product Categories

A Product Category provides a way to set values and behavior across all the products that belong to the Category.  This is a great time saver when first setting up products and also provides a way to make changes to hundreds of products at a time. 

The most important values are the accounting elements that the associated products should use.  The Product Category header provides a few others:

* **Parent Product Category** - this can be useful when reporting by Product Category. The parent Category provides a way to summarize a number of other Categories.
* The **Material Policy** to use when selecting items from inventory.  The choices are First In, First Out \(FiFo\) or Last In, First Out \(LiFo\).  This choice can not be overwritten by the products assigned to this category.  If left empty, the Material Policy set in the Client window will be used.
* The **Asset Group** used to connect assets to products when buying and selling assets frequently.  This connection makes it easier to manage the accounting of capital asset values.  See [Assets and Asset Management](../../assets-and-asset-management.md#asset-groups) for more information.

  **Planned Margin %** - this value is used in calculating the planned margin for products created by Projects. Specifically, where the project line hasn't identified a specific product but the product category is known.

* **Self-Service** - A flag to indicate if the product category should appear in the web store.
* The **Print Color** - Currently not implemented.  May be used to highlight the products assigned to the category by color in menu trees or reports.

#### Product Category Accounting

This is an important tab as it provides the main mechanism to assign the same accounting setup to many products.  When a new product is created, the accounts defined in the Product Category Accounting tab are copied to the product.  In the Product Window, its possible to override these accounts.  These accounts are part of the default accounting setup and will be set to defaults when the a new Accounting record is created.  They accounts must be defined for the ADempiere software to function - even if they will not be used.  

Changes made to the Product Category Accounting can be copied to all the assigned products using the "Copy Accounts" button at the bottom of the Accounting Tab.

{% hint style="info" %}
A set of accounts is needed for each Accounting Schema defined for the system. These will be set to the defaults for the system when the Product Category if first created.
{% endhint %}

{% hint style="info" %}
Note that  For Product Categories connected to Asset Groups, refer to the [Asset Groups](asset-groups.md) page for hints on how to link the accounts.  
{% endhint %}

The required accounts are:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Account</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Product Asset</td>
      <td style="text-align:left">
        <p></p>
        <p>The account used to record the cost of the product. For stocked products,
          this would typically be the balance sheet inventory account. For non-stocked
          products, this could be set to an appropriate expense account. The costs
          recorded are determined by the cost methods used.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Product COGS</td>
      <td style="text-align:left">The Cost of Goods Sold (COGS) account to use to record the costs of the
        product shipped as an expense.</td>
    </tr>
    <tr>
      <td style="text-align:left">Product Revenue</td>
      <td style="text-align:left">The account used to record the revenue from sales of the product.</td>
    </tr>
    <tr>
      <td style="text-align:left">Product Expense</td>
      <td style="text-align:left">The account used to record expenses associated with the product.</td>
    </tr>
    <tr>
      <td style="text-align:left">Inventory Clearing</td>
      <td style="text-align:left">The Account used for posting matched product (item) expenses (e.g. AP
        Invoice, Invoice Match). You would use a different account then Product
        Expense, if you want to differentiate service related costs from item related
        costs. The balance on the clearing account should be zero and accounts
        for the timing difference between invoice receipt and matching.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p>Cost Adjustment</p>
      </td>
      <td style="text-align:left">The account to record cost adjustments when, for example, landed costs
        are added</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p>Invoice Price Variance</p>
      </td>
      <td style="text-align:left">An account used to record the difference between the invoice price and
        the product asset cost when matching AP invoices to material receipts.
        The material receipt document creates accounting facts in the Product Asset
        account and the Not Invoice Receipt account. The matching processes cancels
        the Not Invoice Receipt account amount with the Invoice amount and any
        difference is charged to the Invoice Price Variance.</td>
    </tr>
    <tr>
      <td style="text-align:left">Purchase Price Variance</td>
      <td style="text-align:left">The account used to record the difference between the Standard Cost and
        the Purchase Order Price. The Purchase Price Variance is only used in Standard
        Costing.</td>
    </tr>
    <tr>
      <td style="text-align:left">Average Cost Variance</td>
      <td style="text-align:left">Not currently used.</td>
    </tr>
    <tr>
      <td style="text-align:left">Trade Discount Received</td>
      <td style="text-align:left">The account used to post the amount of trade discounts received on AP
        invoices/credit memos if the "Post Trade Discount" flag is selected in
        the Account Schema. If the invoice is based on an item with a list price,
        the discount received is the difference between the invoice line list price
        amount and the actual price amount.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p>Trade Discount Granted</p>
      </td>
      <td style="text-align:left">The account used to post the amount of trade discounts granted on sales
        invoices/credit memos if the "Post Trade Discount" flag is selected in
        the Account Schema. If the invoice is based on an item with a list price,
        the discount granted is the difference between the invoice line list price
        amount and the actual price amount.</td>
    </tr>
    <tr>
      <td style="text-align:left">Work in Process</td>
      <td style="text-align:left">The account used to record work in progress costs during manufacturing.
        It is equivalent to the Product Asset account but records the costs issued
        to a manufacturing order or services purchased as part of the manufacturing
        process. When the manufacturing order is complete and the results issued,
        the value of the Work in Progress is transferred to the Product Asset account.</td>
    </tr>
    <tr>
      <td style="text-align:left">Floor Stock</td>
      <td style="text-align:left">
        <p>The account to use when issuing stock to a work order where the issue
          method of the Component of the Manufacturing Order is set to "Floor Stock".
          The issue is handled as
          <br />Debit Floor Stock Account</p>
        <p>Credit Work in Process Account</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Method Change Variance</td>
      <td style="text-align:left">The account to use during a manufacturing process when there is a difference
        between the Standard BOM, Standard Manufacturing Workflow and the Manufacturing
        BOM Manufacturing Workflow. It is used in Standard Costing to record the
        difference in costs in the manufacturing process for this product.</td>
    </tr>
    <tr>
      <td style="text-align:left">Usage Variance</td>
      <td style="text-align:left">The Usage Variance is used in Standard Costing. It reflects the difference
        between the Quantities on the Standard BOM or Time on the Standard Manufacturing
        Workflow and Quantities on the Manufacturing BOM or Time on the Manufacturing
        Workflow of the Manufacturing Order.</td>
    </tr>
    <tr>
      <td style="text-align:left">Rate Variance</td>
      <td style="text-align:left">The Rate Variance is used in Standard Costing. It reflects the difference
        between the Standard Cost Rates and The Cost Rates of the Manufacturing
        Order.</td>
    </tr>
    <tr>
      <td style="text-align:left">Mix Variance</td>
      <td style="text-align:left">The Mix Variance is used when a co-product received in Inventory is different
        the the quantity expected</td>
    </tr>
    <tr>
      <td style="text-align:left">Labor</td>
      <td style="text-align:left">The account to use to record the labor costs of manufacturing this product.</td>
    </tr>
    <tr>
      <td style="text-align:left">Burden</td>
      <td style="text-align:left">The account to use to record the burden costs of manufacturing this product.</td>
    </tr>
    <tr>
      <td style="text-align:left">Cost of Production</td>
      <td style="text-align:left">The account to use to record the costs of manufacturing other than labor.</td>
    </tr>
    <tr>
      <td style="text-align:left">Outside Processing</td>
      <td style="text-align:left">The account to use to record the outside costs of manufacturing this product
        for outside/outsourced processing.</td>
    </tr>
    <tr>
      <td style="text-align:left">Overhead</td>
      <td style="text-align:left">The account to use to record the overhead costs of manufacturing this
        product.</td>
    </tr>
    <tr>
      <td style="text-align:left">Scrap</td>
      <td style="text-align:left">The account used to record the scrap costs of manufacturing this product.</td>
    </tr>
  </tbody>
</table>