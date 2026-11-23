# Why are some Custom Property records missing in the related Custom Property tables?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/34550659392787-Why-are-some-Custom-Property-records-missing-in-the-related-Custom-Property-tables*
*Last updated: 2025-01-07T19:38:35Z*

---

Applies To | All Versions

When Custom Properties are assigned to a specific entity they are tracked within the related Custom Property table and corresponding View. For example, if Custom Properties are assigned to Products, entries may appear in the `tProductCustomProperty` table and all values should appear within the `viewCustomPropertyProduct` View. However, it is possible that not all values that appear in the View are shown in the `tProductCustomProperty` table. This is intentional and by design.

If any entities (e.g., Products in this case) were created **before** the Custom Properties were created, then entries will not appear in the related Custom Property table (e.g., `tProductCustomProperty`). However, if a Custom Property value that is different than the Default Value assigned to these entities, then a record will be generated in the table. This means that entities that only have the Default Value may not be recorded in this table. Entities created **after** the creation of Custom Properties may appear in this table regardless of the assigned Custom Property value.

Because of this behavior, it is recommended to **not** reference these tables directly. When reading Custom Property values, it is recommended to reference the Views (`viewCustomPropertyProduct` in this case) if SQL is being used. For custom C# code, the Custom Property Dictionary can be referenced when Model Objects are being used (e.g., `product.CustomProperties.GetAsInt("SchemeKey.PropertyKey")`). When programmatically adding or modifying Custom Properties using custom C# code, it is recommended to use the `MergeCustomProperties()` method while using Model Objects.
