# Functional Solutions

Functional Solutions were introduced alongside TrakSYS 14 to bundle multiple Function Blocks together and offer various out of the box solutions, or at least standardized starting points, for purpose-built implementations. Functional Solutions can also include Dashboards, Reports, and other components that are specific to that bundle -- i.e. not included in any of the individual Blocks.

The Function Blocks that comprise Functional Solutions provide a standardized, extensibile foundation for TrakSYS implementations. In addition to working directly out of the box, they also set clear patterns and structures using standard TrakSYS development techniques and implementation best practices. The Blocks provide clear areas where they may be extended if need be using the established patterns and structures.

The Manifest section documented below each Functional Solution outlines what is included with each, including Blocks, Dashboards, Reports, etc. More detail on how to implement and extend consistuent Blocks can be found in the Function Blocks section of these docs.

Functional Solutions and their respective PowerPoint overviews can be downloaded from the Parsec Support Portal [here](https://portal.parsec-corp.com/hc/en-us/articles/51525810558867-Functional-Solutions).

As Functional Solutions are updated, the latest information can always be found alongside the latest version of TrakSYS reference docs. For major updates, docs for older versions will be pulled out into the Previous Versions section.

## Deployment

Functional Solutions are deployed as a template using the Template Transfer Tooling introduced in TrakSYS 14. They may include Blocks, page definitions, content parts, and other TrakSYS components to deliver a -- wait for it -- Functional Solution that should work out of the box with minimal configuration. These constituent template components (.transfer) files must simply be imported by using the Template Import functionality built-in to a TrakSYS 14 implementation, presumably a development or test environment before being pushed to production via the standard TrakSYS DB Transfer process.

### Updates

Updates to Functional Solutions will be published periodically. Each Solution's changelog will indicate the version of each of its constituent Function Blocks. Since some Block versions may stay the same between releases, the changelog will highlight the differences.

As Functional Solutions are extended during an implementation, special care must be taken when updating Functional Solutions or consituent Function Blocks to ensure customizations are not overwritten. Similarly, if updating Blocks individually, review the Changelog which will call out methods or components updated that other Blocks may depend on.

It's also worth noting that once Solution development has began, an individual Block can be updated separately from the overall Solution. Again, noting where changes may have been made to avoid any overwrite situations.

### Templates

While Functional Solutions are deployed using the Template Transfer Tooling, they may also be integrated into template projects and deployed as part of partner or customer templates and later deployed using the same tooling further downstream.
