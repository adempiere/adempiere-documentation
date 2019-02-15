---
description: >-
  A number of key concepts that are important to understand when working with
  ADempiere
---

# Key Concepts

### Clients, Organizations & Users

ADempiere is built on an organizational model where the **Client** is the highest level of an independent business entity. Each Client will have one or more **Organizations** reporting to it. The Client defines the accounting parameters \(Accounting Schema, Tree definition, Non Monetary UOM's\) that are used by all the Organizations under that client. An **Organization** is a legal entity \(business\) with its own banking, and business processes. Each Organization can have a number of **Users**. The **Users** can be restricted to an organization, multiple organizations or the client through **Roles**.

When you login to ADempiere, you are logging in as a User with a specific Role into a specific Client and Organization.

Any implementation of ADempiere for a business starts with creating the Client. See [Creating the Client](http://wiki.adempiere.net/index.php?title=Creating_the_Client&action=edit&redlink=1).

### Security: Users and Roles

Users are defined as business partner contacts where the business partner is an employee and the user has a password defined. There needs to be a single business partner for each user.

ADempiere implements security through roles which define what elements of the data, menu, processes etc each user has access to. While the administration role may see all aspects of the system and a menu of over 700 entries, a particular functional role may see a menu with a small handful of windows and reports. Roles also help define the workflow and approval levels of the users.

There are a few special users and roles:

* The System user controls the application dictionary and a few other configuration items for the application. The system user can not access client data.
* SuperUser is a system level user that has access to all clients and can access any role.
* For each client, there is an administration user and role created when the client is created and a more restricted user and role.

### Accounting Schema, Combinations, Defaults and keeping track of the money

ADempiere is designed to work with multiple sets of books or "Accounting Schema". Every process that creates accounting consequences does so in all the schema. Schema can be based in different currencies or apply different rules and accounting for a given circumstance.

One of the key benefits of ADempiere is the manner in which accounting consequences are defined. Rather than a single number signifying an account, ADempiere uses a number of fields to generate references to the accounting data. These fields include the traditional account number but add business partners, products, organizations, projects, and other "dimensions". This makes it easy to generate reports or lists of accounting consequences by filtering the various dimensions.

A particular set of dimensions is called a combination and the combinations usually include placeholders for dimensions that will be filled in when a particular transaction takes place. For example the combination defined for product revenue will specify the revenue account but have place holders for the product. The product information will be added when an invoice is completed.

It is important when establishing a new client to completely define the default combinations required by the system in the initial Chart of Accounts. This is a key part of creating a new client. See [Chart of Accounts](http://wiki.adempiere.net/Chart_of_Accounts) for more information.

### Documents and Document Processing

ADempiere is a process and document based system. The processes in the software mimic a document workflow of generation, checks and approvals, action and follow-up. The documents also go through stages of preparation from draft, to prepared, to complete. They can also be voided, reversed and so on.

Most documents, when they are completed, create some accounting consequences in the system. The consequences are created when the document is "posted" and the process that happens is particular to the document. It is important to understand that no accounting consequences can be created without a document and that any consequence or accounting entry can be traced back to the document that generated it.

The document processing is defined by workflows and every document has one. Workflows can be fully automated with documents created and processed behind the scenes with no user intervention. It is also possible to create complex multi-level approval workflows to manage and provide oversight and control with the documents passed from user to supervisor and back.

Another powerful feature of ADempiere is the inter-organizational transactions that can take place.  Where there are multiple organizations for the client, it is possible for the organizations to "do business" with each other. Behind the scenes, when a document is created in one organization, say a Purchase Order, a counter document, in this case a Sales Order, is automatically created in the other organization. A Shipment in one organization generates a Material Receipt in the other and so on. These counter documents ensure that the accounting across the client is consistent and it also saves a lot of time.

### Database Tables and Common Fields

In ADempiere, most database tables contain a set of common fields that are used by most windows or by the underlying rules and software. These are:

| Field | Description |
| :--- | :--- |
| _**Client**_ | A Client is a company or a legal entity.  The Client is created by the System Administrator. Where a server hosts several Clients, any data created for or by one Client cannot be shared with any other client.  The Client is determined when you log into the system. |
| _**Organization**_ | Within a Client there can be one or more Organizations.  An Organization is a unit of the Client.  Examples are stores, departments.  Data can be shared between Organizations.  Depending on your Role, you may have access to all, some or only one Organization. |
| _**Created**_ and _**Created By**_ | These fields are included with nearly every record in the system and record the timestamp of when a record was created and which user was responsible for creating it.  These fields are not usually shown in windows or forms but are available for audits. |
| _**Active**_ | A check box which indicates the that record is active in the system.  There are two methods of making records unavailable in the system: One is to delete the record, the other is to de-activate the record. A de-activated record is not available for selection, but available for reports. There are two reasons for de-activating and not deleting records: \(1\) The system requires the record for audit purposes. \(2\) The record is referenced by other records. E.g., you cannot delete a Business Partner, if there are invoices for this partner record existing. You de-activate the Business Partner and prevent that this record is used for future entries. |
| _**Search Key**_ | A key value for the record in the format required. It provides a fast way of finding a particular record.  The value must be unique but can often be chosen by the user.  If you leave the _**Search Key**_ field empty, the system automatically creates a numeric number for it when the record is saved. The sequence used for this fallback number is defined in the **Document Sequence** window with the name "DocumentNo\_&lt;TableName&gt;", where TableName is the actual name of the table \(e.g. C\_Order\). |
| _**Name**_ |  An alphanumeric identifier of the record.  The _**Name**_ field is used as a default search option in addition to the _**Search Key**_. The name can be up to 60 characters long. |
| _**Description**_ | An optional short description of the record, limited to 255 characters. |
| _**Comment/Help**_ | An optional comment, hint or help about the use of the record.  The text can be up to 2,000 characters long. |
| _**Updated, Updated By**_ | Like _**Created/Created By**_, these fields record the timestamp of the last change made to the record and the user responsible for the change.  These fields are not included on most windows and forms but are available for audits. |

### Record Identifiers

When a field displays information linked to another window or tab, for example a _**Product**_ field in a Sales **Order Line**, the _**Product**_ field is displayed using an Identifier that can include one or more fields from the **Product** window.  These fields are selected and given a sequence by the System Administrator.  The default is often &lt;Search Key&gt;\_&lt;Name&gt; but it can be configured to include other useful fields.

