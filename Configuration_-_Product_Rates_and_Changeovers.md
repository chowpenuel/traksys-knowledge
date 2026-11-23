<!-- Slide number: 1 -->
# Product Configuration

### Notes:
This module will take a further look into the configuration of products, exploring how Product Rates and Changeover Rates/Families can be configured.

<!-- Slide number: 2 -->
# Review - Products
General
Products represent the finished good that are produced from a manufacturing process (System)
A unique Product Code (SKU, Item Number, etc…) identifies each Product
Each Product has a set of standard attributes and user-definable attributes

Related
Product Set: A grouping of products with similar attribute and production information
Product Materials: A Bill of Materials to identify the materials needed to produce the Product
Product Types and Families: Grouping mechanisms for products for both scheduling and production

![](Picture3.jpg)

### Notes:
Before diving into the new content, let's first complete a quick review of products.

In TrakSYS, any good that is produced by a System is considered to be a Product, even if it is an intermediate good that will later be used by another process.
Each Product is configured within a Product Set, with each Product having a Unique Product Code within their Product Set. You can have multiple versions of a Product by configuring multiple Product Sets. The Products will be related to each other by using the same Product Code.

 Each System can use a single Product Set. If Systems have different requirements for the same product, they will need to use different Product Sets. In addition to the product configuration, there are also Product Materials and Versioning that can be utilized. These will not be covered in this Module.

<!-- Slide number: 3 -->
# Review - Product Scheme
General
Product Schemes consist of 20 definable Attributes that can be configured and enabled as needed
Attributes have a Name and Type to identify and limit what they are intended to represent
All Products within a Product Set will have the same Product Scheme and therefore the same Attributes

![A screenshot of a computer Description automatically generated](Picture9.jpg)

### Notes:
For each Product, there are some general properties, and then additional Attributes that can be configured. A Product Set can be assigned a Product Scheme, which will allow you to configure Names and Types for up to 20 attributes. All Products within a Product Set will have the same Scheme applied to them. Outside of the Attributes, all other properties are identical for all products.

<!-- Slide number: 4 -->
# Product Configuration

![A screenshot of a computer Description automatically generated](Picture3.jpg)
General
Each Product has a designated Theoretical and Target Rate Calculation Units Per Minute that is used for OEE, Scheduling and Reporting purposes
Enabled attributes from the related Product Scheme will be displayed, with the matching Attribute label next to it

Advanced – Product Group
Product Sets can have child Product Groups assigned for logical grouping
Products within a Product Group are still part of the same Product Set but are not shown when looking at the root Product Set
Product Groups are different than Changeover Families and do not functionally overlap

### Notes:
The configuration that we will be covering in this module are focused around the Production Scheduling capabilities. This includes the Production Rates and Production Scheduling Property Group.

Each Product can have two rates identified with it, a Theoretical and a Target Rate for Calculation Units per Minute. This is utilized by both the KPI Calculations and the Production Scheduling API.
Theoretical Rate is intended to identify the absolute maximum rate that this product can be produced. It is used to identify what a perfect production environment would produce and it typically unobtainable, representing a 100% performance value.
Target Rate is intended to provide a reasonable goal for production. This value can be updated as production practices improve and capabilities change, acting as a moving goalpost. This typically represents the target performance value.

All other attributes and groupings are for extensibility and mapping purposes.

<!-- Slide number: 5 -->
# Product Configuration
Produced
Materials represent inputs to a System. Products represent an output from a System. A product that is also an input is related to their Material counterpart through the Material Produced property.
A Product can also have a Standard Size and Unit identified for use with Recipes and Bill of Material. This is covered more in-depth during the Batching modules.
Prod Sched
Pre Gap, Post Gap, Pre Padding, and Post Padding are all flat timespans that are referenced when producing the product and affect Production Scheduling.
Product can be assigned to a Changeover Family. This will be covered more after the next Demonstration.

![A screenshot of a computer Description automatically generated](Picture4.jpg)

![A screenshot of a computer Description automatically generated](Picture6.jpg)

### Notes:
Outside of the General Properties Group, Products also have two additional property groupings: Production Scheduling and Produced

In the Production Scheduling tab, you are able to identify a Changeover Family, and additional Production Scheduling Timespans related to the product.
The Timespans are flat values that get added to a job that produces that product. They represent additional start-up or clean-up times that are unrelated to any specific changeovers.
The "Pre" properties occur before the job. The "Post" properties occur after the job.
The "Padding" properties will be included in the projected job duration when using the scheduling API. The "Gap" properties will not be included in the projected job duration, but will create "timeframes that cannot be scheduled" before or after the job when using the scheduling API.

The Changeover Families is a little more complicated. Each Product can be assigned to a single family, which will be used to relate products together based upon Changeover Requirements. This will be covered more after the first Demonstration.

In the Produced Tab, you are able to identify configuration related to Material relations.
Each Product can also be related to a Material with the "Material Produced" property. This allows you to identify that a Product, which is the output of one process, is also a Material, which will be the input to another process. This can be thought of as identifying the Product as an Intermediary Good.
If configuring a Bill of Materials, you can also identify the standard size for the product. When identifying the Material requirements for this Product, the material quantities will be proportional to the Standard Size configured here. The Product Materials are configured as a child entity, and are covered further in later modules.

<!-- Slide number: 6 -->
# Product Rates andProduct Attributes

### Notes:
Let's take a quick look at the Product Configuration in the TS Web before going into the Changeover requirements.

<!-- Slide number: 7 -->
# Changeover Configuration

### Notes:
Next, let's address the Changeover Configuration elements and how they are utilized by Production Scheduling.

<!-- Slide number: 8 -->
# Changeover Families
General
Groups of products with similar changeover requirements are grouped as Changeover Families
Changeover Families are configured in Groups, which are for human readability

![A screenshot of a phone Description automatically generated](Picture2.jpg)

![A screenshot of a computer Description automatically generated](Picture4.jpg)

### Notes:
Changeover Families are configured independently of Products. They are very simple entities that require only a name and a key. Each Product can be assigned a single Product Changeover Family. Product that are assigned to the same Product Changeover Family are expected to have the same changeover requirements.

For example, if you have a production line that makes a number of different products, you will want a Changeover Family for each grouping. In the example on screen, there are two sets of Changeover Family Groups. One for product changeovers that are primarily related to the Meat type, and one that is related to the Packaging type.

<!-- Slide number: 9 -->
# Changeover Types
General
Changeover expectations when transitioning from one product family to another are configured as Changeover Types
The To and From properties can be assigned to any Changeover Family, but can also be assigned to a generic “Any” option
When Production Scheduling is applied, the Pre and Post Duration values will be used to assign additional time to a Job

Notes
Changeover Types are unidirectional
If multiple Changeover Types are applicable, the most specific one will be used

![A screenshot of a computer Description automatically generated](Picture3.jpg)

### Notes:
Once the Changeover Families have been configured, the next step is to identify the relation between these families.
Changeover Types identify the Pre and Post durations for a job when changing from one changeover family to another.

This can be any combination, but keep in mind that this is uni-directional. A changeover from Family A to Family B is not equivalent to a changeover from Family B to Family A.

Additionally, generic changeovers can be configured. In the TO or FROM properties, you can select the "Any" option. The makes the changeover more generic and simplifies some configuration requirements.

When the Scheduling API is used, it will reference these Changeover Types to determine additional Pre and Post durations between jobs. Since some changeovers can be made generic, it is possible that multiple Changeover Types may be applicable. If more than 1 valid Changeover Type is found, then the most specific one will be used. For example, when changing from a Poultry Job to a Beef Job, there would be 4 possible Changeover Types
1) Poultry to Beef
2) Poultry to Any
3) Any to Beef
4) Any to Any
In that example, if Poultry to Beef is configured, it will always take priority over the other options since it is the most specific option.

<!-- Slide number: 10 -->
# Changeover Type Sets

![A screenshot of a computer Description automatically generated](Picture3.jpg)
General
Groups of Changeover Types are put together into Changeover Type Sets. These sets can be assigned to a Product Set.
Each Product Set can utilize a different Changeover Type Set, but a single Changeover Type Set can be assigned more than once.
Different Systems that have different Changeover requirements need different Product Set and Changeover Type Sets.

![A screenshot of a computer Description automatically generated](Picture9.jpg)

![A screenshot of a computer Description automatically generated](Picture8.jpg)

### Notes:
The Changeover Types are configured within Sets. This means it is possible to configure the same changeover for the same Product Family relationships more than once. This is to address the need for different Changeover requirements on different assets, even if they support the same Product Mix.

Changeover Type Sets are related to Product Sets. Each Product Set can be assigned their own Changeover Type Set, and a Changeover Type Set can be used more than once. Assets that share the same Changeover requirements will be able to utilize relate their Product Sets to the same Changeover Type Sets. However, assets that have different Changeover requirements will need to use different Product Sets.

<!-- Slide number: 11 -->
# Product Families andProduct Changeovers

### Notes:
Let's look at this configuration in the TS Web. While we will not go in-depth into Production Scheduling, we will also look at an example of how affects the scheduling process.
