# Package

## Summary

### Entity Name

Package

### Database Table Name

`tPackage`

### API Object Name

`DbPackage`

### Entity Description

Each row in this table represents an installed TeaGet Package.

## Properties

`Version [ Version ]`

The current version number of the installed package.

`Installed as TrakSYS Version [ InstalledAsTsVersion ]`

The TrakSYS version in which the Package was installed.

`Transfer Mode [ TransferMode ]`

The Database Transfer category (Configuration or UI) for the package.

`SpecInfo [ SpecInfo ]`

The XML data for the package.

`Install Only [ InstallOnly ]`

Enabling Install Only mode prevents Resync errors for scenarios where TeaGet Package is not needed on production server.
