# Glossary

## Accounting Facts

An Accounting Fact or just Fact is the results of a document posting. It includes all the information about the accounts and Dimensions used and the debit/credit information. The Facts are the basis of financial reports and can be traced back to the documents that created them. Facts are also referred to as Accounting Consequences.

## Application Server

A software program running on a server that provides a web interface or access to a Java Client. The Application Server also performs system and client processes as required - for example, the off-line posting of documents.

## Client

A Client is the highest level business entity in the ADempiere Application. It represents the entire business and may include one or more Organizations as separate legal entities or departments. Client data can not be shared with other Clients.

ADempiere is a multi-tenant system. Client data and the application that uses it are hosted on a server as a tenant and there can be multiple tenants on a server.

A Client is not to be confused with the [Java Client](glossary.md#java-client), a Java software application that runs on a local computer and communicates with the Application Server to access data.

## Client Administrator

A Client Administrator is a User logged into a Role that provides administrative control of the Client. The Client Administrator's main function is to define the Roles and rule used by the Client. Client Administrators can only affect their Client.

## Combination

The set of Dimensions used in generating an Accounting Fact. For accounting systems that don't use dimensions, the Combination is equivalent to the account number. For ADempiere, the Combination uses the account number plus a number of additional Dimensions. The Combinations keep the actual account number simpler - for example, you don't have to have a revenue account for each particular product. They also make reporting by Dimension simpler.

## Commitment Accounting

A type of accounting that creates Accounting Facts for Sales or Purchase Orders and similar documents to record the legal/financial commitment that the Order represents. Commitment Accounting is controlled in the **System Configurator** window and the default is not to use it.

## Dimension

A Dimension is a record of a field on a document that is included in the Accounting Facts generated when the document is posted. Typical Dimensions in ADempiere include the Client, Organization, Business Partner, Product, Project, Campaign, and Activity.

## Dunning

The process of making repeated and insistent demands upon a customer, especially for the payment of a debt.

## Dunning Run

A collection of information and also the process of collecting information for the purposes of Dunning.

## Identifier

See [Record Identifiers](glossary.md#record-identifiers).

## Integrator

A person or company who is involved in the customization, installation and configuration of the ADempiere software. Integrators are typically consultants who are not involved in the day-to-day operation of the system but who played a role in the adoption of the software at a particular company.

## Java Client

A Java Client is a stand-alone software application that runs on the local computer. Unlike a web-based application, a Java Client does not require a browser but it may communicate with a server over a network.

## Record Identifiers

When a field displays information linked to another window or tab, for example a _**Product**_ field in a Sales **Order Line**, the _**Product**_ field is displayed using an Identifier that can include one or more fields from the **Product** window. These fields are selected and given a sequence by the System Administrator. The default is often &lt;Search Key&gt;\_&lt;Name&gt; but it can be configured to include other useful fields.

For System Administrators, the identifier is the collection of fields used in a Table Direct reference of an ID field. The fields used and their sequence are selected from the Table and Column window, Column tab. Typical usage would be &lt;Search Key&gt;\_&lt;Name&gt;.

## Role

A security measure that limits the possible actions and access of a User to their intended function. When a User logs in to the application, they log in to a particular Role. Roles are defined and managed by Client Administrators.

## System Administrator

A particular User and Role in ADempiere that can define how the application behaves, what data is shown and how it is used. The System Administrator creates Clients and supports all Clients on a server but is not able to access the Client's data. Each Client can also have Roles with Administrative privileges but these are restricted to the Client and can not affect other Clients on the server.

## User

A person who is logged in to the application. Users are defined by the Client Administrator. Users may be associated with a Business Partner Contact and are typically assigned specific Roles and Organizational access.

