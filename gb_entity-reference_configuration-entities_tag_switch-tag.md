# Switch Tag

## Summary

### Entity Name

Switch Tag

### Database Table Name

`tTag`, `tTagSwitch`

### API Object Name

`DbTagSwitchComposite`

### Entity Description

Switch Tags define complex conditional logic using a single Switch Tag and a set of Cases. If you need to compare a Tag to many possible values, you can substitute a Switch Tag for many Compare Tags. Each Switch Tag defines a set of Cases, which the Logic Service compares to the Switch Tag setting for equality; a Case specifies a constant or Tag to compare to the Switch Tag and a Value constant or Tag to return if the Case matches. You can specify a Switch Default to use as the Tag's return value if there is no matching Case; otherwise the Tag retains its previous value.

## Properties

`Switch Tag [ SwitchTagID ]`

Tag to use as the "Switch." Every scan, the Logic Service compares the value of the Switch Tag to each Case Tag. If it finds a match, this Tag returns the value of the matching Case Value; if the Logic Service does not find a match, it sets this Tag's value according to the Use Default setting.

`Use Default [ UseDefault ]`

When checked, the Logic Service will use the Switch Default setting to set the Tag value if no Cases match the Switch Tag's value. Otherwise, the Tag retains its previous value when there is no matching Case.

`Switch Default [ DefaultTagID or DefaultConstant ]`

Constant or Tag value to use as the Tag's value when no Cases match the Switch Tag value. This setting is only available when Use Default is checked.
