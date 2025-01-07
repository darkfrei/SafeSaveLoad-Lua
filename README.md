# SafeSaveLoad-Lua
lightweight utility for serializing and deserializing Lua tables


# Description
The SaveLoad module is a lightweight utility for serializing and deserializing Lua tables. It transforms Lua tables into a human-readable string format that can be stored or transmitted and then reconstructs the original table from this serialized string.

This module is particularly useful for saving and loading data in Lua-based projects, such as game state management, configuration storage, or debugging complex data structures.

# Key Features
Serialization: Converts Lua tables, including nested ones, into a string representation.
Deserialization: Restores tables from their string representations.
Human-Readable Format: Easy to read, edit, and debug serialized data.
Type Safety: Supports number and string keys/values, ensuring compatibility and error avoidance.
Use Cases
Save and load game progress, settings, or other structured data.
Debug or log table data in a readable format.
Share structured data between Lua scripts or applications.


# How to Use
The SaveLoad module provides two core functions for serializing Lua tables into a string format and deserializing them back into Lua tables. This is useful for saving and loading structured data such as configurations, game states, or any nested table structure.

Functions
serializeTable(tbl)
Serializes a Lua table into a formatted string.

Parameters:

tbl (table): The table to be serialized.
Keys must be of type string or number.
Values can be string, number, or another nested table.
Returns:

(string): A string representation of the table that can later be deserialized.
Example:

lua
Code kopieren
local myTable = {
    name = "test",
    id = 123,
    nested = {
        key = "value",
        count = 42,
    },
}

local serialized = SaveLoad.serializeTable(myTable)
print(serialized)
deserializeString(str)
Deserializes a string back into a Lua table.

Parameters:

str (string): The serialized string produced by serializeTable.
Returns:

(table): A Lua table reconstructed from the serialized string.
Example:

```lua
local serialized = [[start table
stringIndex
items
tableValue
  start table
  numberIndex
  1
  stringValue
  sword
  numberIndex
  2
  stringValue
  shield
  numberIndex
  3
  stringValue
  potion
  end table
stringIndex
stats
tableValue
  start table
  stringIndex
  health
  numberValue
  100
  stringIndex
  mana
  numberValue
  50
  end table
stringIndex
level
numberValue
5
stringIndex
player
stringValue
hero
end table]]

local deserialized = SaveLoad.deserializeString(serialized)
```

```lua
local SaveLoad = require("SaveLoad") -- Assuming SaveLoad is in your project's folder

-- Define a table to serialize
local data = {
    player = "hero",
    level = 5,
    stats = {
        health = 100,
        mana = 50,
    },
    items = {"sword", "shield", "potion"}
}

-- Serialize the table
local serializedData = SaveLoad.serializeTable(data)
print("Serialized Data:")
print(serializedData)

-- Deserialize the string back into a table
local deserializedData = SaveLoad.deserializeString(serializedData)
print("Deserialized Data:")
for key, value in pairs(deserializedData) do
    print(key, value)
end
```

# Advantages
Handles nested tables with ease.
Easy to read and debug the serialized format.
Supports string and number types for both keys and values.

# Limitations
Does not support boolean, function, or userdata types.
Keys must be string or number. Other types will raise an error.
Circular references in tables are not supported. Ensure your table structure is acyclic.
