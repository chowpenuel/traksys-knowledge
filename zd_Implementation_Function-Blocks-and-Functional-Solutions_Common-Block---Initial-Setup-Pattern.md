# Common Block - Initial Setup Pattern

*Source: https://portal.parsec-corp.com/hc/en-us/articles/53922137885971-Common-Block-Initial-Setup-Pattern*
*Last updated: 2026-07-30T21:01:52Z*

---

Applies To | TrakSYS 14.0.0+

### Summary

This article describes the initial deployment of the Common and Orders Function Blocks. Common must be deployed first because it provides the expected parent Sections and foundational components used by other blocks. Orders is required by some downstream blocks and also demonstrates the deployment pattern used by most Function Blocks.

**Recommendation:** Deploy and validate Common and Orders in a development environment before using Page Definition Shadows or promoting the configuration to production.

### Deployment Overview

  * **Template download:** Obtain the Common and Orders template packages from the appropriate [Function Block](https://portal.parsec-corp.com/hc/en-us/articles/51525693987731-Function-Blocks) pages on the support portal.
  * **Template import:** Import each template into TrakSYS in prerequisite order.
  * **Page Definition deployment:** Manually deploy the Sections and Hub1 Page Definitions supplied by each imported template.
  * **System View configuration:** Provide a matching System View and Systems so the deployed operational pages have content to display.



### Requirements

  * Access to the support portal pages used to download the [Function Block](https://portal.parsec-corp.com/hc/en-us/articles/51525693987731-Function-Blocks) templates.
  * Access to the root Site Developer area and the Templates page in the target TrakSYS installation.
  * Permission to import templates and deploy Page Definitions.
  * Permission to configure System Views, Systems, and Page Definition Shadows as needed.
  * The [block-specific documentation](https://docs.parsec-corp.com/blocks) for any additional Function Blocks you plan to deploy.



### Prerequisite Order

Import and deploy templates in the order required by their prerequisites.

**Order** | **Template** | **Purpose**  
---|---|---  
1 | Common | Required first. Provides the parent Sections and foundational components used by other Function Blocks.  
2 | Orders | Required by some downstream blocks and used in this article as the baseline example for deploying a block on top of Common.  
3 | Other blocks | Deploy only after their documented prerequisites. Review the block-specific documentation before deployment.  
  
### Download the Function Block Templates

1\. Open the appropriate Function Block page on the TrakSYS support portal.

2\. Download the Common and Orders template packages. Download any additional blocks only after reviewing their prerequisites.

![](https://portal.parsec-corp.com/hc/article_attachments/53922161021203)

### Import a Function Block Template

Repeat this procedure for each template, beginning with Common. Respect the documented prerequisites for every block.

1\. In the target TrakSYS installation, open the root Site, select **Developer** , and then open **Templates**.

![](https://portal.parsec-corp.com/hc/article_attachments/53922137871891)

2\. Select **Import Template** and choose the downloaded template package.

3\. Review the import confirmation. If needed, select **Compare Template Content** to inspect the differences between the source template and the destination installation. Select **Import** when ready.

**Version note:** A source and destination version mismatch is acceptable when the destination TrakSYS version is newer than the source version.

![](https://portal.parsec-corp.com/hc/article_attachments/53922161025299)

4\. Confirm that the template import completes successfully.

**Important:** A successful template import loads the configuration, scripts, views, and supporting files. It does not deploy the Page Definitions. The Page Definitions must be deployed separately.

### Deploy the Page Definitions

1\. Return to the **Templates** page.

2\. Find the imported template, open **More options** (the vertical ellipsis), and select **Pages**.

![](https://portal.parsec-corp.com/hc/article_attachments/53922161026067)

3\. Review the deployable Page Definitions included with the block.

4\. Deploy each required Page Definition to its intended parent location.

![](https://portal.parsec-corp.com/hc/article_attachments/53922161029139)

### Deploy the Common Block

Deploy Common before any other Function Block. Common supplies four top-level Sections that act as parents for content supplied by downstream blocks. Deploy all four Sections.

![](https://portal.parsec-corp.com/hc/article_attachments/53922161029523)

#### Configure the Blocks Section

The Blocks Section is the primary parent for operational Function Block pages. After deploying the Section, create a System View with the same key. By default, the Section key is `Blocks`, so the System View key should also be `Blocks`.

**Recommended key:** Keep the Section and System View key as `Blocks` unless the implementation has a specific reason to use a different coordinated key.

The Blocks System View is normally used as a controlled baseline and testing view. Add at least one representative System of each type used by the deployed Blocks. Those Systems may also belong to other operational System Views.

![](https://portal.parsec-corp.com/hc/article_attachments/53922137876627)

#### Use Page Definition Shadows for Operational Copies

A typical implementation keeps the Blocks Section as the tested baseline and creates Page Definition Shadows for operational areas. For example:

  * Deploy and validate the Blocks Section.
  * Create Page Definition Shadows as needed, then create a matching System View for each Shadow using the same key.

![](https://portal.parsec-corp.com/hc/article_attachments/53922137877267)

  * Deploy and test new Function Block content in Blocks.
  * Update the Shadows after the baseline configuration is approved.

![](https://portal.parsec-corp.com/hc/article_attachments/53922137878035)

The baseline Blocks Section should be permission-controlled and maintained in a development environment for configuration, templating, and testing. Promote the approved configuration to production through the implementation's normal deployment process.

### Deploy the Orders Block

After Common is deployed, import and deploy Orders using the same template import and Page Definition deployment procedures. Orders contains one deployable Hub1 Page Definition named Orders.

1\. Open the imported Orders template and select **More options > Pages**.

2\. Deploy the Orders Hub1 beneath the Blocks Section.

![](https://portal.parsec-corp.com/hc/article_attachments/53922161034643)

3\. Open the deployed Orders page and confirm that the selected Blocks System View provides Systems for the page to display.

### Deploy Additional Function Blocks

Most other Function Blocks follow the same import and deployment pattern as Orders. However, a block may contain multiple deployable Hub1 Page Definitions intended for different parent Sections.

**Example:** The Tasks Block includes Tasks and Manage Tasks Hub1 Page Definitions. Deploy Tasks beneath Blocks and Manage Tasks beneath Manage.

Hub1 Page Definitions within the same block may use the same keys or titles while having different names and intended parent Sections. Do not deploy Hub1s with conflicting keys beneath the same Section.

**Key conflict:** Deploying Tasks and Manage Tasks beneath the same Section causes a Page Definition key conflict. Use the Page Definition name and the block-specific documentation to identify the correct parent for each Hub1.

Other blocks may supply additional Hub1s. Review the names carefully and consult the associated documentation whenever the intended parent Section is unclear.

![](https://portal.parsec-corp.com/hc/article_attachments/53922161035027)

### Validate the deployment

  * Confirm that Common was imported and that all four parent Sections were deployed.
  * Confirm that the Blocks Section key matches the Blocks System View key.
  * Confirm that the Blocks System View contains representative Systems.

![](https://portal.parsec-corp.com/hc/article_attachments/53922161035795)

  * Confirm that Orders (and any additional content) was deployed beneath Blocks.
  * Open the deployed pages and verify that expected Systems and content are displayed.
  * Validate the baseline Blocks Section before updating any Page Definition Shadows.

![](https://portal.parsec-corp.com/hc/article_attachments/53922137880339)

**Blank page:** If a deployed operational page is blank, verify that the matching System View exists and contains at least one appropriate System.

### Deployment notes

  * Common must be deployed before downstream Function Blocks.
  * Template import and Page Definition deployment are separate operations.
  * Deploy each Hub1 to its documented parent Section to avoid key conflicts.
  * Use the baseline Blocks Section for controlled testing before updating operational Shadows.
  * Review the documentation for each additional Function Block before deployment.


