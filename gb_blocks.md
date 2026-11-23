# Function Blocks

Function Blocks were introduced alongside TrakSYS 14 as a way to standardize and leap frog some of the basic development needed when starting an implementation.

Function Blocks represent some of the most common pages, parts, and scripts created when starting a typical implementation. They serve as a starting point and put forth TrakSYS development best practices. Therefore, when extending these Blocks, the patterns should be followed to prioritize maintainability and standardization across TrakSYS implementations.

The documentation around each specific Block in the sections below outline what is included with each part, what they're meant to be used for, and how to implement and extend them. This will also include what configuration or other dependencies each Block requires for it to function correctly.

As Function Blocks are updated, the latest information can always be found alongside the latest version of TrakSYS reference docs. For major Block updates, docs for older versions will be pulled out into the Previous Versions section.

Function Blocks can be downloaded from the Support Portal [here](https://portal.parsec-corp.com/hc/en-us/articles/51525693987731-Function-Blocks), and deployed simply using the new Template Transfer Tooling introduced with TrakSYS 14.

## Related Documentation

Each Function Block has a related PowerPoint document which serves as an overview of its capabilities, how its various components map together, how its components can be interacted with and their respective impacts on TrakSYS services and the TrakSYS database. These documents can be downloaded here from the same link above.

## Manifest

The Manifest Section under each Block details each and every entity that is included with each Block including Content Parts, Content Pages, Scripts, Visual Pages, and Configuration.

## Deployment

Function Blocks are deployed as a template using the Template Transfer Tooling introduced in TrakSYS 14. They may include content pages, content parts, page definitions, scripts, configuration, and other TrakSYS components. As with deploying any other template, when page definitions are included, on the initial deployment the target section of the page definitions must be selected, then subsequent deployments (if applicable) will overwrite tagged page definitions there.

As Blocks may be extended, special care must be taken when updating to ensure customizations are not overwritten. Similarly, if updating Blocks individually, review the Changelog which will call out methods or components updated that other Blocks may depend on.

### Templates

While Function Blocks are deployed using the Template Transfer Tooling, they may also be integrated into template projects and deployed as part of partner or customer templates and later deployed using the same tooling further downstream.
