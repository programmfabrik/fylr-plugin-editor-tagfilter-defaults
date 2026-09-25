# fylr-plugin-editor-tagfilter-defaults

A fylr plugin that pre-fills editor fields with default values. Which defaults apply depends on the tags and the pool of the record. Users no longer have to type the same values into every new record.

The plugin is frontend only. It fills the editor form, it does not change records on the server.

## Configuration

The defaults are configured in the base configuration under "Editor" in the entry "Tag filter dependent presets". Each row of the table is one rule.

A rule has these settings:

* **Action**: when the rule applies. "Insert" applies to new records, "Update" applies to existing records. The option "Update" is only available if a tag filter or a pool filter is set.
* **Mask**: the mask the rule applies to. Only masks with at least one supported field are listed.
* **Pools filter**: an optional list of pools. The rule only applies if the record is in one of these pools.
* **Tag filter**: an optional tag filter. The rule only applies if the tags of the record match the filter.
* **Default**: the list of fields to pre-fill.

Each entry of the **Default** list sets one field:

* **Type**: currently only "Preset" is supported.
* **Field**: the field to pre-fill. Text fields, number fields, boolean fields, date fields and links to other records (for example list entries) are supported. Date range fields, hierarchy parents and links that can point to more than one object type are not supported. Links need fylr 6.36 or newer.
* **Value**: the value to set.

The value of a text field may contain placeholders such as `%_standard%`. The button next to the mask selection lists the placeholders available for the selected mask.

For links the value is picked like in the editor. If the linked record is deleted later, the rule does nothing for that field.

For date fields the value can be set to "Today" instead of a fixed date. The current date is then used every time the rule applies.

Rules are applied when the editor loads a new record, when the mask changes, when the tags change and when the pool changes. If no rule matches a field, the field is reset to its empty value. **Records edited in bulk mode are never touched.**
