# Link (URL) Helpers

There are a handful of helper prefixes and suffixes to optimize working with URLs in TrakSYS.

## self

The `self` prefix is used to preserve the current Page URL including QueryString parameters to shorten what is needed when constructing links/URLs. New QueryString parameters can be added after `self:` and if they don't exist in the current QueryString, they will be added. Otherwise, if they do exist, they will be updated.
