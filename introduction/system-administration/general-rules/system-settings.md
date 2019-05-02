# System Rules

## Trees and Tree Maintenance

Trees are collections and organizations of data using a summary and child structure. They are primarily used in financial reporting to summarize information in useful ways.

Each Accounting Dimension, such as Product, can have multiple trees and which tree gets used in a report is defined in a Reporting Hierarchy. Financial Reports are defined in lines and columns that can use the summary level elements of the tree. For example, in the Garden World Balance Sheet, there is a Reporting Line for Cash and the Account Element Value is set to 11 - Cash. This is a summary level account and the line value on the report would include all activity in all the subordinate accounts shown in the tree below.

![](../../../.gitbook/assets/image-10.png)

Each Accounting Dimension requires at least one tree and the default trees are used if no Reporting Hierarchy is selected.

Where it is important to have multiple trees, a Reporting Hierarchy can be created to define the collection of trees to use in a given report. You can use the trees and reporting hierarchy to change the meaning of the summary product or to use different summary products.

For example, in Garden World, suppose it is important to report only on the sale of plants. A summary level product "Plants" could be created and the Product tree modified to group the various "plant" Products under the Summary Level Product. Then a financial Report Line Set or Report Column Set could be created that referenced this summary product and the "Plant Results" financial report would only shows results for the "plant" products. If it was important to show only "tree" plants, you could create a new product tree and hierarchy where the Plants summary level product only had "tree" type products as children. More realistically, you may need to use different categorizations altogether rather than subsets, such as New versus Legacy products in one tree and Plants, Tools, Furniture, Misc in another.

