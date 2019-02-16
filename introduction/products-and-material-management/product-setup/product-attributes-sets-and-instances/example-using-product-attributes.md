# Example - Using Product Attributes



## Example - Using Product Attributes <a id="firstHeading"></a>

> <table>
>   <thead>
>     <tr>
>       <th style="text-align:left"><a href="http://wiki.adempiere.net/File:Note.gif"><img src="http://wiki.adempiere.net/images/6/62/Note.gif" alt="Image:Note.gif"/></a>
>       </th>
>       <th style="text-align:left">
>         <p><b>Note:</b>
>         </p>
>         <p>This page describes features not yet incorporated. Some of the features
>           described here are part of the changes in ADEMPIERE-72 - fixes to the info
>           windows and lookup/search fields. In version 3.8 and earlier, product attributes
>           and instance attributes can not co-exist.</p>
>       </th>
>     </tr>
>   </thead>
>   <tbody></tbody>
> </table>



### Fertilizer in Garden World



#### Attribute setup

Garden World sells lawn fertilizer in 50 and 70kg bags. They want to expand this to a variety of formats \(50 or 70 Kg bags, cubic yards\), chemical specifications, and base compost \(chemical, manure, mushroom, peat\). Each product has a lot number and a guarantee date. Each of these things represents an attribute of the fertilizer product. Collectively, they represent an attribute set and, with a specific lot and guarantee date defined, they represent an instance of the attribute set.

The demo database has an attribute set defined for Fertilizer Lot and that needs to be expanded to include the format, chemical specs and base compost. This is done by defining attributes for each of these items as follows:

* Open the [**Attribute Window**](http://wiki.adempiere.net/ManPageW_Attribute) window and create new attributes as follows:
  * New Attribute - Package
    * Name: Pkg
    * Description: Fertilizer Package
    * Attribute Value Type: List
    * Instance Attribute: checked
    * Attribute values
      * New Value - 50Kg
        * Key: 50Kg
        * Name: 50Kg
        * Description: 50 Kilogram bag
      * New Value - 70Kg
        * Key: 70Kg
        * Name: 70Kg
        * Description: 70 Kilogram bag
      * New Value - Cubic Yard
        * Key: CY
        * Name: CY
        * Description: Cubic Yard
  * New Attribute - Chemical - Nitrogen
    * Name: N
    * Description: Nitrogen
    * Attribute Value Type: Number
    * Instance Attribute: unchecked
  * New Attribute - Chemical - Phosphorous
    * Name: P
    * Description: Phosphorous
    * Attribute Value Type: Number
    * Instance Attribute: unchecked
  * New Attribute - Chemical - Potassium
    * Name: K
    * Description: Potassium
    * Attribute Value Type: Number
    * Instance Attribute: unchecked
  * New Attribute - Base
    * Name: Base
    * Description: Base Component
    * Attribute Value Type: List
    * Instance Attribute: unchecked
    * Attribute values
      * New Value - Chemical
        * Key: Chem
        * Name: Chem
        * Description: Chemical
      * New Value - Manure
        * Key: Man
        * Name: Manure
        * Description: Manure
      * New Value - Mushroom
        * Key: Mus
        * Name: Mushroom
        * Description: Mushroom
      * New Value - Peat
        * Key: Peat
        * Name: Peat
        * Description: Peat

Next, open the [**Attribute Set Window**](http://wiki.adempiere.net/ManPageW_AttributeSet) and find the attribute set "Fertilizer Lot". Note that the attribute set contains a lot number and a guarantee date. Add the new attributes to this attribute set.

Clear the cache or log out and in before continuing.

#### Assigning Attributes to Products

Now, open the [**Product Window**](http://wiki.adempiere.net/ManPageW_Product) and find the Fertilizer \#50 product. Note that the attribute set is already defined as Fertilizer Lot. Click on the button in the Attribute Set Instance field to open the [Product Attribute Dialog](http://wiki.adempiere.net/Product_Attribute_Dialog) and set the product attributes for the Fertilizer \#50 product. Specifically, set these as shown:

[![Image:Product\_asi\_example.png&#x200E;](http://wiki.adempiere.net/images/a/ab/Product_asi_example.png)](http://wiki.adempiere.net/File:Product_asi_example.png)

Note that the lot and guarantee dates do not appear on this window. They will be set later.

Repeat this process for the Fertilizer \#70 product: find the product, assign the attribute set then assign the product attributes. For Fertilizer \#70, use the 70Kg package.

Now we have to make some fertilizer that meets these specs. We will do this with the [**Production Window**](http://wiki.adempiere.net/ManPageW_Production) window. Create a new production header and save it. Then move to the [**Production Plan Tab**](http://wiki.adempiere.net/ManPageW_Production#Tab:_ProductionPlan) and select Fertilizer \#50 as the product and a quantity of 40. Set the Locator to Fertilizer and save the record. Create a second record and repeat this step with the Fertilizer \#70 product. Move back to the [**Production Header Tab**](http://wiki.adempiere.net/ManPageW_Production#Tab:_ProductionHeader) and click the "Create/Post Production" button. This will pull the BOM from the product window and fill the [**Production Line Tab**](http://wiki.adempiere.net/ManPageW_Production#Tab:_ProductionLine).

Move to the [**Production Line Tab**](http://wiki.adempiere.net/ManPageW_Production#Tab:_ProductionLine) and find the Fertilizer \#50 product. Note that the Attribute Set Instance field is blank. Click the Attribute Set Instance button and the [Product Attribute Dialog](http://wiki.adempiere.net/Product_Attribute_Dialog) will appear again.

[![Image:Production\_asi.png&#x200E;](http://wiki.adempiere.net/images/3/35/Production_asi.png)](http://wiki.adempiere.net/File:Production_asi.png)

The form is a copy of the attribute set instance template created in the product window and now the instance attributes are visible. In this dialog, the lot number and guarantee date can be set manually or you can click on the New Record button to calculate the next lot number or the guarantee date based on the attribute set information. The logical place to do this is in the production process.

Close the Product Attribute Dialog and note that the Attribute Set Instance field is filled in. Save the record. If you click on the Attribute Set Instance button again, you can see the values of the attributes. Repeat this with the Fertilizer \#70 Production Plan.

Back on the [**Production Header Tab**](http://wiki.adempiere.net/ManPageW_Production#Tab:_ProductionHeader) and click the "Create/Post Production" button again to complete the process. The new product will appear in the Fertilizer locator.

Open the Product Info window to see the attributes available.

[![](http://wiki.adempiere.net/images/thumb/e/e4/Productinfo_fert50.png/800px-Productinfo_fert50.png)](http://wiki.adempiere.net/File:Productinfo_fert50.png)

Select or search for the Fertilizer \#50 product. The Warehouse tab shows 40 in stock. If you click on that line in the Warehouse tab and then click on the Available to Promise tab, and the Show Detail check box, you will see the instance attribute information. In this case, \(&lt;&lt;120&gt;&gt; 2013-06-30\).

To see the Product attribute info for the Fertilizer \#50 product, click on the Product Attribute tab. It will list the product attributes as

```text
***  Product Attribute  ***
 Pkg: 50Kg
 N: 10
 P: 20
 K: 15
 Base: Chem
```

