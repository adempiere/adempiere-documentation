---
description: >-
  Dunning is the process of informing customers about the state of their account
  and collecting money from customers that they owe to the organization.
---

# Dunning

Dunning is the process of informing customers about the state of their account and collecting money that they owe to the organization. As a process, it generally starts with polite requests, perhaps verbally or a sent statement of account, followed by e-mails and letters that might escalate to legal threats before the account is written off and passed to a collections agent.

An example of a company policy on Dunning might be as follows:

1. For invoices over their due date by less than 15 days, a polite phone call to inquire and request payment. No action taken on the Customers's Account.
2. For returned checks - enter a negative payment and a new invoice charging a returned check fee. Find the original payment and reset the payment allocation. Allocate/cancel the original payment and the returned check. This will leave the invoice unpaid. Call the customer and politely request payment. No action taken on the Customers's Account.
3. For invoices over 30 days, a letter requesting immediate payment. No action taken on the Customers's Account.
4. For invoices over 60 days, a letter threatening that the amounts will be passed to a collections agent.  The Customers credit is stopped and the payment term applied to new invoices is changed to Immediate.
5. For invoices over 90 days, write off the amount owing and pass the invoice to a collections agent. This is a manual process.

ADempiere includes tools to help with the Dunning process making it easy to manage collections for a large number of customers by keeping track of where each customer and invoices sits in the process. The intent is that the Dunning process be "run" on a periodic basis and at each run, invoices move through the process until they are paid or written off. There are two key periodic tasks:

1. Generating lists of invoices and payments relevant to the Dunning policy, referred to as a "Dunning Run"; and
2. Printing or emailing Dunning letters to the delinquent customers, a process called "Print Dunning Letters."

The Dunning process can be customized for a particular Business Partner or Business Partner Group and each process can have multiple levels or steps that collectively define the Dunning policy of the company. Each level can take a number of actions such as printing letters, sending emails, stopping credit or resetting the payment terms for the Customer.   Customer Invoices are flagged as being in the Dunning process and associated with a particular Dunning Level. 

The relationship with individual customers can be further managed by setting a _**Dunning Grace**_  _**Date**_ in the **Business Partner** window, **Customer** tab, which affects all invoices, or in the **Invoice \(Customer\)** window, **Invoice** tab, for a particular invoice.  The Customer or Invoice affected will not be included in Dunning processes until after the Dunning Grace Date.

## Dunning Setup

To start using Dunning, the dunning policies must be defined and setup according to your needs.  Once the setup is complete, Dunning becomes a periodic and repeatable activity of creating **Dunning Runs** and **Printing Dunning Letters**.   

### The Dunning Policy

A Dunning policy definition starts with a Dunning record and one or more Levels. Open the **Dunning** window in the **Partner Relations** **&gt; Business Partner Rules** menu.  The **Dunning** window is relatively simple.  You will need to create a new record for each distinct dunning policy or collection of levels you require.  The key fields are as follows:

| Field | Description |
| :--- | :--- |
| _**Name**_  | Any useful name.  The _**Name**_ is used to identify the Dunning process to apply to Business Partners and Business Partner Groups. |
| _**Default**_ | Indicates the Dunning record is the default Dunning process.  It is not currently used. |
| _**Create levels sequentially**_ | Select if the actions defined by the Dunning Levels need to be performed in order.  For example, if you have several reminders based on the number of days an invoice is due, it might not be a good idea to send all of them at the same time to the same customer.  On the other hand, if the Levels can be performed in parallel, then you can deselect this field. Examples of parallel actions might be sending a statement and stopping credit for overdue accounts. |

###  Dunning Levels

The Dunning Level  defines the actions that should be taken based on some triggers.  To understand how to setup the levels it helps to know how they are used.

The gathering of information on which Business Partner needs to be Dunned is called a "run".  When the Dunning process is run, it is run for a particular level or all levels and for a particular date. The date when the Dunning process is run determines the age of the invoices and the number of days after the payment due date for each unpaid invoice. For each level, all the invoices that meet the constraints of the Level are identified.  If payments are to be included, these are also identified.  Fees, if any are added. All this information is  gathered in a Dunning Entry for each Business Partner but nothing is done with the information at this point.  You can review the Dunning Entries and the Entry Details \(the identified invoices etc..\) and verify that all is in order or you can re-run the Dunning process and recreate the Dunning Entry information.  If a new run is performed before the previous was processed, the Entries and Entry Details will be duplicated. 

Actions are taken when the Dunning Entry is processed.  This could include the sending of e-mails or printing of letters and other actions as mentioned below.  Once processed, no further changes are allowed and the invoices identified will be in the dunning process. Once processed, if a new run is performed, the Entries and Entry Details will be different depending on the constraints set in the Level.

The Level defines the constraints using the following fields:

| Field | Description |
| :--- | :--- |
| _**Show All Due**_ | If true, the dunning letter with this level includes all due invoices, including invoices that are not due yet. If false, it will only show invoices where the _**Days after due date**_ is less than the days due of the invoice or within the range of _**Days From**_ and _**Days To**_ if _**Range**_ is selected.  |
| _**Show Not Due**_ | If true, invoices that are not due yet \(based on the Dunning Run date\) will be included.  If false, only invoices with a positive number of days due will be included \(&gt;=0\).  The field is ignored if _**Range**_ is selected. |
| _**Range**_ | If selected, only invoices with days due that fall between _**Days From**_ and _**Days To**_ are considered.  _**Range**_ is only displayed if _**Show All Due**_  is deselected.  __ |
| _**Days after due date**_ | Indicates the number of days after the payment due date to initiate dunning. If the number is negative, it will include invoices due in the future \(not due\). _**Days after due date**_  is only displayed if _**Range**_ and _**Show All Due**_ are deselected. |
| _**Days between dunning**_ | The Days Between Dunning indicates the minimum number of days between sending dunning notices.  Invoices that were dunned more recently than this will be ignored.  _**Days between dunning**_ is only tested if _**Range**_ and _**Show Not Due**_ are deselected. See the note below. _**Days between dunning**_ is only displayed if _**Range**_ and _**Show All Due**_ are deselected. |
| _**Days From**_ | The inclusive lower limit of the invoice days due to consider.  Invoices with days due less than _**Days From**_ will be ignored.  Only relevant if _**Range**_ is selected. |
| _**Days To**_ | The inclusive upper limit of the invoice days due to consider.  Invoices with days due more that _**Days To**_ will be ignored.  Only relevant if _**Range**_ is selected. |
| _**Include Payments**_ | If selected, unallocated payments for the Business Partner will be included.  If _**Is Statement**_ is selected, all payments will be included.  Otherwise, payments will only be included if there is at least one invoice - this prevents dunning for money you owe to the customer. |
| _**Charge fee**_ | Indicates if the dunning letter will include fees for overdue invoices.  Note that the fee amount is not automatically added to the customer's account. |
| _**Fee Amount**_ | The _**Fee Amount**_ indicates the charge amount on a dunning letter for overdue invoices. This field will only be display if the _**Charge Fee**_ checkbox has been selected. Note that the fee amount is not automatically added to the customer's account. |
| _**Print Text**_ | A label to be printed on documents or correspondence.   |
| _**Note**_ | Optional additional information about this record. |
| _**Dunning Print Format**_ | The **Dunning Print** process will generate a PDF of the list of entries associated with this Level and either print it or send it as an attachment to an e-mail.  If you do not specify a _**Dunning Print Format**_, the PDF will not be generated and the Dunning Run will not be processed. |
| _**Credit Stop**_ | Select if the Customer's _**Credit Status**_ should be set to _Credit Stop_ for any invoices found at this level.  This may help prevent further losses.  |
| _**Set Payment Term**_ | Select if the Customer's _**Payment Term**_ should be changed, for example from _Net 30_ to _Immediate,_ if any invoices are found at this level. |
| _**Payment Term**_ | The Payment Term to set if _**Set Payment Term**_ is selected.  _**Payment Term**_ only appears if _**Set Payment Term**_ is selected. |
| _**Collection Status**_ | The Collection Status to set on the affected invoices.  If left blank and _**Is Statement**_ is not selected, the invoice _**Collection Status**_ will be set to _Dunning_.   |
| _**Is Statement**_ | Select if the dunning level is intended as a statement of accounts for the Customer.  If selected and _**Collection Status**_ is blank, then the _**Collection Status**_ of any affected invoices will not be changed. |

{% hint style="info" %}
For the first Dunning Level, its important to set the _**Days between dunning**_ to zero since invoices that have not yet been dunned have zero days since the last dunning.  If you set _**Days between dunning**_ &gt; 0 on all Levels, no new invoices will ever be found.  

This only applies if you deselect the _**Show all due**_ and _**Show not due**_ flags. 
{% endhint %}

### Assigning a Dunning Policy to Business Partners

Each Business Partner needs to be associated with a Dunning policy or they will not be included in the Dunning process.  The Dunning policy can be set for a Business Partner Group or individual Business Partners.  The individual setting takes precedence.

To set the Dunning policy for a whole group, open the **Business Partner Group** window in the **Partner Relations** **&gt;** **Business Partner Rules** menu.  Select the desired Dunning entry in the _**Dunning**_ field.

To override the Group Dunning policy, set the _**Dunning**_ field in the **Customer** tab of the **Business Partner** window for a particular Business Partner.

## Dunning Runs

A **Dunning Run** is a record of the dunning process. The **Dunning Run** record identifies the _**Dunning Date**_ and _**Dunning**_ policy and _**Dunning Level**_ that was used.  Each affected Business Partner becomes an **Entry** in the **Dunning Run** and each invoice, payment and fee becomes a **Line** of the **Entry.**

The **Dunning Run** window can be found in the **Open Items** menu.  

There are two ways to create Dunning Runs:

1. Manually, by creating a record in the **Dunning Run** window with a _**Dunning Date**_, _**Dunning**_ policy, and optionally a _**Dunning Level**_; or
2. Via a process, **Create Dunning Run**, which will also create the **Entry** and **Line** information. 

The **Create Dunning Run** process is found in the **Open Items** menu as is the **Dunning Run** window.  The **Dunning Run** window/tab also includes a button that executes the **Create Dunning Run** process.

### Creating Dunning Runs Manually

Open the **Dunning Run** window and create a new record.  Set the fields accordingly. The key fields are as follows:

| Field | Description |
| :--- | :--- |
| _**Dunning Date**_ | Mandatory. Specifies the date of the Dunning Run.  The _**Dunning Date**_ determines the number of days payments are past their due date for invoices.  The _**Dunning Date**_ defaults to the current system date. |
| _**Dunning**_ | Mandatory. The Dunning policy used to create the **Entry** and **Line** records. |
| _**Dunning Level**_ | The Dunning Level used to create the Entry and Line records.  If blank, all Levels of the Dunning policy will be used. |

In addition to these three key fields, there is a Button _**Create Dunning Run**_  _****_and a flag _**Processed**_. The button process and parameters are described below.  When run from the **Dunning Run** window, the _**Create Dunning Run**_  process will generate the Entry and Line records for the Dunning Run.

The _**Processed**_ flag is read-only and will be set once the **Dunning Run** is sent/printed.

{% hint style="warning" %}
There is a button _**Send**_ in the **Dunning Run** window that appears when the _**Processed**_ flag is set. It is not used.  See issue [\#2363](https://github.com/adempiere/adempiere/issues/2363).
{% endhint %}

### Creating Dunning Runs via the Process

Dunning Runs can also be created using the **Create Dunning Run** process found in the **Open Items** menu.  The benefit to using the **Create Dunning Run** process from the menu is that it will create a number of **Dunning Run** records at once along with their associated **Entry** and **Line** information.  

{% hint style="warning" %}
If you run the **Create Dunning Run** process from the menu, it may duplicate an existing ****unprocessed **Dunning Run** rather than recreate the Entry and Line records.
{% endhint %}

Whether run from the menu or from a **Dunning Run** record, the process is similar.  The **Create Dunning Run** process has a number of parameters that control how the **Dunning Run**, **Entry** and **Line** records are created:

| Parameter | Description |
| :--- | :--- |
| _**Organization**_ | Sets the Organization to use in the Dunning Run.  If not _All \(\*\),_ the invoices and payments added to the Entry Lines will be limited to those belonging to the specified Organization. |
| _**Include Disputed**_ | If selected, the Lines will include invoices that are marked as _**In Dispute**_. |
| _**Only Sales Invoices**_ | If selected, only Sales \(Customer\) Invoices will be included.  Otherwise, both Sales and Purchase \(Vendor\) invoices will be included.  This is useful where a Business Partner is both a Customer and Vendor and contra allocations are possible. |
| _**Default Sales Rep**_ | The Sales Rep added to the Entry when it is created.  The _**Default Sales Rep**_ is not used to filter the invoices or payments. |
| _**Dunning Currency**_ | If _**Include All Currencies**_ is not selected, only invoices in the selected  currency are included in the Lines. |
| _**Include All Currencies**_ | Select to include items in all currencies in the Dunning Run. |
| _**Business Partner**_ | If not blank, only generate Entries and Lines for the specified Business Partner. |
| _**Business Partner Group**_ | If not blank, only generate Entries and Lines for Business Partners in the specified Business Partner Group. Ignored if _**Business Partner**_  is not blank. |
| _**Dunning Date**_ | Specifies the date of the Dunning Run.  The _**Dunning Date**_ determines the number of days payments are past their due date for invoices.  The _**Dunning Date**_ defaults to the current system date. |
| _**Dunning**_ | If selected, only that Dunning policy will be used to create a Dunning Run.  If blank, Dunning Runs will be created for all active Dunning policies for the Client.  This is only relevant if the **Create Dunning Run** process is performed from the Menu and not from the **Dunning Run** window.  In the **Dunning Run** window, if the parameter is not blank it will replace the _**Dunning**_ policy set in the **Dunning Run** record. |
| _**Dunning Level**_ | If a _**Dunning**_ policy is specified, the Dunning Run Entry and Line information can be limited to a single Dunning Level. If not specified, Entries will be created for each Dunning Level in the Dunning policy. In the **Dunning Run** window, if the parameter is not blank it will replace the _**Dunning Level**_ set in the **Dunning Run** record. |

### Dunning Run Entries and Lines

Once the Dunning Run Entries and Lines have been created by the **Create Dunning Run** process, they can be reviewed and adjusted if required.  No changes to the status of the invoices or customers has occurred and won't until the Dunning Run is printed.  Until then, Run Entries and Lines can be deleted or made inactive \(by deselecting the _**Active**_ field\).  The entire Run can also be deleted. It may be apparent, for example, that payments can be allocated to unpaid invoices and that this should be done before the Customer is sent a dunning note.  If necessary, the Create Dunning Run process can be repeated and the Dunning Run entries will be recreated.

To review the Dunning Run, open the **Dunning Run** window in the **Open Items** menu.  The **Dunning Run** tab is pretty straight forward.  Processed runs will be read only.  Click the _**Create Dunning Run**_ button to recreate the entries if required.

{% hint style="info" %}
The _**Create Dunning Run**_ process will overwrite the  _**Dunning Date, Dunning** policy and **Dunning Level**_ ****fields.
{% endhint %}

#### Dunning Run Entry

The **Entry** tab shows records for each Business Partner and Dunning Level.  If a Level was not specified on the **Dunning Run** tab, there may be multiple **Entry** records for each Business Partner, one for each Level that applies.  The following describes the key fields:

| Field | Description |
| :--- | :--- |
| _**Dunning Level**_ | Read only.  Shows the Dunning Level that applies to this Entry. |
| _**Business Partner**_ | Mandatory.  The Business Partner that is responsible for the Line items. Note that this should be a read-only field. Be careful not to change it.    |
| _**Partner Location**_ | Mandatory. This will default to the Business Partner Location that is flagged as "Remit To" or "Pay From".  If these aren't found, the first "Bill To" location will be used and if this also isn't found, the first active location will be used.  If there are no active locations, the Create Dunning Run process will throw an exception.  |
| _**User/Contact**_ | Select the User or Contact who will receive the Dunning letter or email.  The **User/Contact** will default to the first User associated with the _**Partner Location**_ selected or the only User if there is just one User/Contact for the _**Business Partner**_. If there are multiple Users but none associated with the Partner Location, the field will be left blank. The _**User/Contact**_ is required and the User record requires a valid email address if the Dunning letter will be sent by email. |
| _**Currency**_ | Mandatory. The currency to use on the dunning letter.  Defaults to the Currency used in the Create Dunning Run process. Invoice amounts will be converted to this currency using the default exchange rate in effect when the record is first saved.   |
| _**Sales Representative**_ | Mandatory. Defaults to the Sales Representative set in the Create Dunning Run process. The Sales Representative info can be used as contact info in letters and will be the "From" addressee on emails. |
| _**Note**_ | The _**Note**_ text can be used on the dunning letter to the Customer. |
| _**Amount**_ | Read only. The converted total amount of all the invoices, payments, fees and interest in the **Lines**.  A negative amount may indicate that the company owes the customer money. |
| _**Quantity**_ | Read only.  A count of all the invoices and payments in the Lines.  The count does not include lines for fees or interest. |

#### Dunning Run Line

The Line ****tab list the invoices, payments, fees and interest being dunned.  The fields are self explanatory.

{% hint style="warning" %}
The _**Times Dunned**_ field is a count of the number of times the item appears on Dunning Run Lines, including unprocessed ones. See issue [\#2365](https://github.com/adempiere/adempiere/issues/2365).
{% endhint %}

#### Previewing the Dunning Letter

It is possible to preview or print a Dunning Letter from the **Entry** tab of the **Dunning Run** window.  Simply select an Entry record and click the Print or Print Preview icon in the toolbar.  A Dunning Letter for that entry, using the assigned print format will be shown/printed. An example is linked below.

{% hint style="info" %}
Printing  or previewing the Dunning Letter this way does not "process" the Entry.  It only allows you to see the document that was or will be sent to the customer.  To "process" the Entry, you have to run the **Print Dunning Letters** process discussed below.
{% endhint %}

{% file src="../../.gitbook/assets/dunningentryexample.pdf" caption="Example Dunning Letter" %}

## Print Dunning Letters

The process **Print Dunning Letters** in the **Open Items** menu will print the Dunning Run information and/or send the information as a PDF attachment to the customers.  Running the process will mark the Dunning Run as "Processed", making it read-only.  The process will also update the _**Collection Status**_ and  _**Dunning Level**_ of the Invoice, and, if so configured in the Dunning policy, set the Customer's Business Partner _**Credit Status**_ to _Credit Stop_ and replace the Customer's default _**Payment Term**._

There are a few parameters you can set to control how the process runs. The process can be run multiple times to reprint the information or change the parameters.

| Parameter | Description |
| :--- | :--- |
| _**EMail PDF**_ | If selected, the a PDF report listing the Dunning Run Entry Lines will be emailed to the Customer. |
| _**Mail Template**_ | The email template to use.  Mandatory if _**EMail PDF**_ is selected. |
| _**Dunning Run**_ | The Dunning Run to print.  Only unprocessed Runs can be chosen.  If left blank, ALL Dunning Runs will be \(re\)printed. |
| _**Only if BP has Balance**_ | If selected, emails or printed reports will only be generated if the Entry _**Amount**_ shows a positive balance greater than zero.  |
| _**Print Unprocessed Entries Only**_ | If selected, only unprocessed Entry records will be printed.  If not selected, processed Entry records will be reprinted as well.  |

{% hint style="warning" %}
If the _**Dunning Run**_ parameter is left blank and _**Print Unprocessed Entries Only**_ is deselected, ALL Dunning Runs will be \(re\)printed.  If _**EMail PDF**_ is also selected, all the Dunning Run Entries will be \(re\)sent to the Customers. _****_See issue [\#2369](https://github.com/adempiere/adempiere/issues/2369).
{% endhint %}

