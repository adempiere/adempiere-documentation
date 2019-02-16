---
description: How to design the taxes in ADempiere
---

# Tax Setup

Before entering documents that have tax consequences, the taxes must be created.

Taxes can be complex, with different accounting requirements, calculations and reporting requirements. The tax can vary by product and by the geographical location of the seller, or buyer. In the ADempiere tax model, the tax to use on a document is selected based on a tax category. The tax category is assigned to products and charges and must contain at least one summary or parent tax definition. Subordinate taxes determine the details and actual accounting consequences based on the situation and geography. For really difficult and unruly tax situations, a software or script rule can be created to determine what tax to apply.

{% hint style="info" %}
There is a Tax Setup workflow defined in ADempiere but since you have not setup the products yet, you can skip most of it. Follow the window sequence below instead.
{% endhint %}

## Examples

Before getting into the details, consider a few examples.

### Canada

In Canada, the sales tax varies by province. There is typically a Provincial Sales Tax \(PST\) which is different in each province, and a common national Goods and Services Tax \(GST\). Certain provinces combine these into a Harmonized Sales Tax \(HST\) but there are still products where only the GST or PST portion of the HST applies. GST/HST is a pass through tax meaning that it is tracked as a liability or receivable based on the sales or purchase transactions. The PST is an end-user tax meaning its a liability on a sale but an expense on a purchase.

### EU and VAT

The rules in the EU are complex. A primer can be found on the [VAT](http://wiki.adempiere.net/VAT) page. The page also contains lots of examples. Many of the countries use a graded tax scheme based on the type of product. For example, in Sweden there are four different VAT categories on sold goods and services. These are:

* **Full Rate** - 25%
* **Half Rate** - 12%
* **Low Rate** - 6%
* **No VAT** - 0%

Different products and services belong to these different categories.

## Setup Taxes

Tax setup uses windows found in the menu under **Performance Analysis » Accounting Rules**

### **Tax Category**

The [**Tax Category Window**](http://wiki.adempiere.net/ManPageW_TaxCategory) is used to enter and maintain Tax Categories. Each and every product or charge is associated with a tax category which determines how taxes will be applied to the product. This is where the major differences in taxes applied to various products are defined. Set up the categories to identify the high level differences. Regional differences will be handled in other windows. A good selection of Tax Categories in Canada would be:

* **No Tax** - no tax applied to the document. Tax is not applicable to the transaction.
* **Exempt** - the product or service is exempt from tax. This has special consequences for input tax credits and the accountants will want to track it. The Government determines which products and services are exempt.
* **Zero-Rated** - the product of service is considered tax free without the special consequences. Again, the Government determines where this applies.
* **PST Only** - the product only has Provincial Salse Tax \(PST\) applied.
* **GST only** - the product only has GST applied.
* **PST/GST** - the product can have both PST and GST applied.
* **HST** - the product has HST applied.

### Tax Rate

The [**Tax Rate Window**](http://wiki.adempiere.net/ManPageW_TaxRate)  defines the different taxes used for each tax category. For example Sales Tax must be defined for each State in which it applies. If you have multiple taxes falling in a single category, create a summary level tax with the approximate total tax rate. Then create the subordinate tax rates and assign the the summary level tax as their parent.

> <table>
>   <thead>
>     <tr>
>       <th style="text-align:left"><a href="http://wiki.adempiere.net/File:Note.gif"><img src="http://wiki.adempiere.net/images/6/62/Note.gif" alt="Image:Note.gif"/></a>
>       </th>
>       <th style="text-align:left">
>         <p><b>Note:</b>
>         </p>
>         <p>Every tax rate requires a parent or summary tax. When entering the order
>           or invoice lines the tax is first estimated using the summary tax rate.
>           The correct tax is calculated when the document is prepared or completed.
>           With many possible rates for a tax category, be aware that estimation can
>           be wrong and that the order/invoice grand total shouldn't be trusted until
>           the document is prepared.</p>
>       </th>
>     </tr>
>   </thead>
>   <tbody></tbody>
> </table>

The tax is always calculated from the line net amount. For taxes that include multiple taxes in the base amount, you will have to calculate the net effect and adjust the individual tax rates accordingly. For example, ADempiere calculates the line total tax for two subordinate taxes as 

$$
TT = LNA*(Tax1 + Tax2)
$$

where TT is the Total Tax. Tax1 and Tax2 are the subordinate rates and LNA is the line net amount. If you need the calculation where Tax2 is based on the Tax1 amount as in

$$
TT = LNA*Tax1 + (LNA*Tax1)*Tax2
$$

you will have to adjust the Tax2 rate to equal Tax1\*Tax2.  Similarly, if the equation was 

$$
TT = LNA*Tax1 + LNA*(1+Tax1)*Tax2
$$

the adjusted Tax2 rate would be \(1+Tax1\)\*Tax2. For more complex cases, you may need to define custom rules to calculate the tax.

#### Dealing with Regional Differences

The tax rates are defined regionally as there can be major differences. The "Billing From" and "Shipping To" location information determines the match with the Country and Regions on the Tax Rate and which tax to apply. In other words, if HST only applies to sales billed in Canada and shipped to customers located in Canada, the HST Tax Rate has the From and To countries set to Canada. HST will not be applied to sales billed in Canada and shipped to customers in the USA. The granularity of the regional definitions can be extended from countries and regions to ZIP codes. Leaving the country or regions fields blank means the tax rate will apply in all countries or regions.

{% hint style="info" %}
A corollary rule is that every business partner needs to have a bill from and ship to location defined, as does every warehouse that receives goods. If not, there will be errors.
{% endhint %}

#### Exempt Tax Rates

You can define tax rates as "SO Exempt". If a business partner is flagged as Tax Exempt, the software will find the the first tax rate marked as SO Exempt with the lowest actual rate - not necessarily zero, just the lowest rate. In the simplest case, define a single tax rate as SO Exempt with the rate set to 0%. 

#### How Tax Rates are Selected

There is no restriction on the number of tax rates assigned to a category so it is possible to have many to choose from. The software decides which tax rate to apply by simply picking the first summary tax rate it finds that can be applied.  It is not possible to force the order of the search except that summary tax rates with no country or region defined will be tested first.

The Valid From date field will only limit new taxes which will come into effect. The date is compared to the billing date. There is no way to define a date to stop applying a tax. For that, you have to manually mark the rate as inactive. For special cases, a software or script rule can be defined to determine what amount of tax to apply.

#### Tax Rate Accounting

On the Accounting Tab, you can define the accounting for each tax rate. There are five accounts:

| Account | Description |
| :--- | :--- |
| Tax Due | The account for taxes owed and payable |
| Tax Credit | The account for taxes expected to be refunded or received |
| Tax Expense | The account for paid taxes that can't be reclaimed |
| Tax Liability | The account for tax declaration liability |
| Tax Receivables | The account for tax credit after tax declaration |

### Global Tax Management

There are a few other windows that you can use to define tax related information. The information in these windows is not used by ADempiere but is available for use by any rules or scripts you may need to develop. Find them in the menu under **Performance Analysis » Accounting Rules » Global Tax Management**:

* [**Tax Rate Parent Window**](http://wiki.adempiere.net/index.php?title=ManPageW_TaxRateParent&action=edit&redlink=1) - The Tax Rate Parent Window defines the different subordinate taxes used for each tax category. It is essentially similar to the Tax Rate windows but shows the child taxes in an included tab.
* [**Tax Group Window**](http://wiki.adempiere.net/index.php?title=ManPageW_TaxGroup&action=edit&redlink=1) - allows you to group the business partner with a reference tax.
* [**Tax Type Window**](http://wiki.adempiere.net/index.php?title=ManPageW_TaxType&action=edit&redlink=1) - another method to group taxes together.
* [**Tax Base Window**](http://wiki.adempiere.net/index.php?title=ManPageW_TaxBase&action=edit&redlink=1) - defines the tax base as the product price, quantity, cost or weight.
* [**TaxDefinition Window**](http://wiki.adempiere.net/index.php?title=ManPageW_TaxDefinition&action=edit&redlink=1) - You can use the tax definition information to create the logic necessary to get the tax rate to your document.

