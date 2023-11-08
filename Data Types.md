Newlife uses a number of data types, some standard, some specialized.

## Standard


| Type | Description | Notes |
| :--- | :---------- | :---- |
| Object | This is an object type as defined here (e.g ClothingItem). | Sometimes abbreviated as "obj". Further methods can be called on this e.g. `$w.getLegwear().getBasicDesc()` |
| String | A text string. | Sometimes abbreviated as "str". These include both Strings intended for direct insertion into output and enumerated values.  |
| Enum | An enumerated string. | These are technically strings but valid values are from a set range.  They are usually all uppercase.  They are defined in the enum reference documentation that are intended to be tested in conditional statements. If a method takes an enum value as a parameter then it will error if provided a String that isn't a valid type for that enum. |
| Boolean |  A true/false value. | Sometimes abbreviated as "bool". |
| Void | Null | **Only in return types.** This means the method returns nothing. Typically the case for methods that change the game's state. |
| Integer | An integer (whole-number) numeric value. | Often abbreviated as "int". Newlife custom scenes do not use any floating-point numbers: only integers. |

Velocity also uses the above types and also uses lists (single dimension arrays) and maps (hashed arays).

## Specialized

| Type | Description | Notes |
| :--- | :---------- | :---- |
| Baby | Collection | Contains generalized information about babies |
| ClothingItem | Object | A clothing item |
