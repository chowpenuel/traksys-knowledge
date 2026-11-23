<!-- Slide number: 1 -->
# Introduction to Products

### Notes:
Products have a lot of related entities and configuration within TrakSYS. Depending on the solution that is being implemented, you may be using Product, Product Sets, Product Materials, Changeover Types, Changeover Sets, and more.

In this module, we will begin with the most common product-related configuration entities. Additional properties and entities will be covered in future modules as the related solutions are covered.

<!-- Slide number: 2 -->
# Products
General
Products represent the finished goods that are produced from a manufacturing process (System)
A unique Product Code (SKU, Item Number, etc…) identifies each Product
Each Product has a set of standard attributes and user-definable attributes

Related
Product Set: A grouping of products with similar attribute and production information
Product Materials: A Bill of Materials to identify the materials needed to produce the Product
Product Types and Families: Grouping mechanisms for products for both scheduling and production

![](Picture3.jpg)

### Notes:
In TrakSYS, Products have a distinct characterization. They are used to model ANY finished good that is produced by ANY manufacturing process. This means that, if you have multiple production processes in a row, the intermediate goods would be considered a Product. This is because each Product in TrakSYS can be configured to have rates, attributes, changeovers and more associated with it to assist with its Production.

Each product has a Product Code that is used to uniquely identify it and can contain bill of materials. In addition to this, there are several other entities that act as grouping and relational entities. For this module, we will first be covering how the Products, Product Sets and Product Schemes interact. Afterwards, we will cover how these Schemes can be used with Product Mapping to expose Product information.

The other entities, such as Product Materials, Types, and Families, will be covered another time in their own Modules

<!-- Slide number: 3 -->
# Product Sets

![A screenshot of a computer Description automatically generated](Picture7.jpg)

![A screenshot of a computer Description automatically generated](Picture8.jpg)
General
Product Sets represent the product mix that can be produced by a manufacturing process (System)
Each System can be assigned a single Product Set, but a Product Set can be assigned to multiple Systems
Product Sets are assigned a Product Scheme to identify the user-definable attributes for all related products

Advanced
Products within a Product Set must have unique Product Codes, but Products in different Product Sets can share a Product Code
Product Changeover Type Sets are also assigned to the Product Sets. This is addressed in the Production Scheduling Modules.

### Notes:
Let's begin with Product Sets.

A Product Set identifies a group of Products that be produced by a System. Most properties and production information are related to the Product Set, including attribute configuration, tag mapping, and more. Each System can be assigned a single Product Set, but a Product Set can be used by multiple Systems. However, if two Systems have different production expectations for a product (such as different theoretical rates, product attributes, or changeover requirements), those two Systems should not use the same Product Set.

These entities include:
Product Materials:
Product Scheme:
Product Map:
Changeover Type Families:

If two Systems have different production expectations, but have overlaps in the Products they can produce, that is fine. Each system can use a different Product Set, and within each of those Product Sets, both can have a matching Product with the same Product Code. This allows for the Products to be related to each other, even though they may be in different Product Sets and have different ID’s in the database.

<!-- Slide number: 4 -->
# Product Scenario
Scenario

Products represent the finished good that are produced from a manufacturing process (System).

If multiple Systems can produce the same finished good, but have different Attribute requirements or values, more than one version of the finished good may be configured.

This is accomplished through having multiple Product Sets that each have a Product that has the same Product Code.
Lower Rate Lines
Higher Rate Lines

![A screenshot of a computer Description automatically generated](Picture9.jpg)

![A screenshot of a computer Description automatically generated](Picture6.jpg)

### Notes:
In this scenario, there is a packaging area with four systems. Three of them are identical, but the fourth produces a different package size. This difference translates with the theoretical rate for the last line being lower when producing goods. Because of this difference, the first 3 lines would share a Product Set, but the last line would use a different product set. In both Product Sets, there is a Product called Adravil with same Product Code. The first Product Set's Adravil has a theoretical rate of 120.  However, since the last line produces at a unique rate, the theoretical rate of Adravil in the second product set can be lower to 80.  Lines 1-3 and Line 4 create the same product, but end up with different attributes. Since the product code for both product sets are identical, reporting can be done across all four lines.

<!-- Slide number: 5 -->
# Product Scheme
General
Product Schemes consist of 20 definable Attributes that can be configured and enabled as needed
Attributes have a Name and Type to identify and limit what they are intended to represent
All Products within a Product Set will have the same Product Scheme and therefore the same Attributes

![A screenshot of a computer Description automatically generated](Picture2.jpg)

![A screenshot of a calculator Description automatically generated](Picture7.jpg)

### Notes:
Each Product will be able to identify a set of production attributes. This includes a Theoretical Rate, a Target Rate, and then 20 additional “Attribute” fields that can be configured to the implementation’s needs. While this allows for flexibility, it does require some level of standardization to be done effectively. This standardization is enforced through Product Schemes.

A Product Scheme is an entity with 20 children, one for each Attribute. For each of these children, you can identify the Name and Value type you want, and you can disable any additional attribute fields that you don’t want. Each Product Set can then be assigned a Product Scheme, which will then apply those attributes across each product. Since this is applied at the Product Set level, all Products within the Set will have the same attributes exposed. One can then change the individual values for each attribute on their respective product. The effects of the Scheme will be immediately visible in the configuration page of any Product.

<!-- Slide number: 6 -->
# Product Entities

### Notes:
Let’s take a look at the configuration of these entities in a Demonstration.

<!-- Slide number: 7 -->
# Product Mapping

### Notes:

<!-- Slide number: 8 -->
# Product Mapping

![](Picture2.jpg)
What is Product Mapping?
Product Schemes consist of 20 definable Attributes that can be configured and enabled as needed.

A Product Map will map a Product's Attribute Values to a virtual tag. Each Product Map contains a Product Map Item for every Attribute in the corresponding Product Scheme.

Each Map has an identified Product Code Tag that is tracked. When it changes value, the related Product’s Attributes will be mapped into Tags based upon the Product Map Items

### Notes:
Product Mapping is a layer of configuration that sits on top of a Product Set and uses the Product Scheme information. It allows you to take the Attributes of a Product and push its values into Virtual Tags based upon a specific Product Code Tag. This allows you to update a single centralized Tag and then have the map automatically set a list of related tags with values from the product's attributes. This is particularly useful for exposing attribute values that may be useful to other configuration elements. For example, the Target and Theoretical Rate of a Product is very useful KPI and Performance tracking.

<!-- Slide number: 9 -->
# Configuration: Product Map
General
Product Maps can be created as a child entity for a Product Set. This ensures that the Product Map can use the related Product Scheme’s information.
Multiple Product Maps can be made for a single Product Set.
Properties
Product Code Tag: Which Tag will be monitored to identify which Product is being produced
Theoretical and Target Rate Tags: Which Tags to map the standard Theoretical and Target Rates to.
Logic Service: Which Logic Service will be in control of this process

![A screenshot of a product map Description automatically generated](Picture4.jpg)

### Notes:
In a Product Map, you will identify a Product Code Tag. This Tag will then be tracked by the Logic Service and used to determine what Product will have its attributes mapped. In the example provided, the Product Code Tag that we will be tracking is the “OCV.PACK.PL1.PRODUCT” tag.
There are two additional tags that can be configured directly on the Map as well, the Target and Theoretical Rates. All other attributes will be configured independently as a Product Map Item.

<!-- Slide number: 10 -->
# Configuration: Product Map Item

![A screenshot of a chat Description automatically generated](Picture7.jpg)

![A screenshot of a computer Description automatically generated](Picture8.jpg)
General
For each Product Map, there will be 20 Product Map Items, one for each Attribute of the related Product Scheme.

Each Product Map Item can be enabled or disabled depending upon need. The only other property is the Map Tag, which identifies which Tag the Attribute value will be written to.

### Notes:
Each Product Map Item will correspond to a single Product Attribute. Based upon the related Product Scheme, these Items will already have a name associated with them to help with clarity. Simply provide the Map Tag for any attribute that you want to be exposed during production. In the example shown, the “Bottles per Case” attribute in my Product Scheme. The matching Map is set to the “OCV.PACK.PL1.BOTTLES_PER_CASE” tag.

After this configuration is complete, the Logic Service will monitor the Product Code Tag and complete the mapping automatically. Let’s take a look at some examples of this.

<!-- Slide number: 11 -->
# Product Mapping - Example 1

![](Picture20.jpg)

![](Picture21.jpg)

![](Picture22.jpg)
Product Mapping

Attributes are mapped to specific Tags.
Product Configuration

Product is part of a Product Set and has Attributes exposed based upon the Product Scheme
Logic Evaluation

When the Product Map Tag changes, Logic Service finds the matching product and updates the other tags

![A screenshot of a chat Description automatically generated](Picture12.jpg)

### Notes:
In this example, there is a Product called Adravil 200. It has 4 Attributes, including Theoretical Rate and Bottles per Case. Remember that these Attributes can be anything you want and are based upon your Product Scheme.

In the configuration, the designer has given Adravil 200 the following property values:
Product Code as ADRA.200
Theoretical Rate is set to 80
Bottles per Case is set to 36

For the parent Product Set, a matching product map has been made.
The Product Map will be watching the Product Code Tag of “OCV.PACK.PL1.PRODUCT” for changes.  Once logic services detecs a new product code under that tag,
It will map the Theoretical Rate to the “OCV.PACK.PL1.THEORETICAL” tag and
map the Bottles per Case to “OCV.PACk.PL1.BOTTLES_PER_CASE” tag.

The result of this mapping is shown on the right.

<!-- Slide number: 12 -->
# Product Mapping - Example 2

![](Picture3.jpg)

### Notes:
To look at this more explicitly, this example includes the full set of the configuration involved.

Like the previous example, this focuses upon 3 main tags: the Product Code Tag, and two Attribute-related tags.
The Scheme identifies those two attributes for the Product Set, which contains Two Products, each with their own Product Code and Attribute values.

The Product map tracks the Product Code Tag, and then maps each Attribute to the tag with the matching name.

With that configuration in place, the Logic Services tracks the product code tag. In Step 1 of the example, logic service sees the Product Code Tag change to “ADRA”.  Logic service then loads up the product set with the matching product and it's product code. Finally, it then maps the Attribute values to the appropriate Tags.

In this example, the result would be that the “Bottles per Minute” Tag would be set to the value of 200, and the “Bottles per Case” Tag would be set to the value of 24.

<!-- Slide number: 13 -->
# Product Mapping

### Notes:
Let’s look at an example of this in the Demonstration, and see the process in action.
