# oas_course
Set of materials for OAS course


# Presentation:
<!-- TODO link to the presentation -->

# Practical excercises

This section is divided into 4 sections:
 - JSON Schema
 - OpenAPI Schema
 - OpenAPI Schema - advanced
 - Using OpenAPI Schema in practice

## 1. JSON Schema

Open API Schema is based on JSON Schema. So, we will start with the basics of JSON Schema.

Useful links and resources:
[Understanding JSON Schema](https://json-schema.org/understanding-json-schema/basics.html)

[jsonschema.net](https://jsonschema.net/) to create JSON Schemas from JSON objects.

Also most of the modern LLMs can generate JSON Schema from natural language.

### 1.1 Basic JSON Schema

Given the following JSON object representing a menu item:

```json
{
  "id": 456,
  "name": "Cappuccino",
  "description": "A delicious cappuccino made with our finest espresso.",
  "price": 3.50
}
```
Create a JSON Schema that describes JSON object with the following conditions:

**`id`**: required attribute, integer

**`name`**: required attribute, string, minimum length of 3, maximum length of 50

**`description`**: optional attribute, string, maximum length of 100, nullable

**`price`**: required attribute, number, minimum value of 0

**Objective:**

Learn to define a JSON Schema for describing a simple JSON object representing a menu item. Result should be valid JSON Schema with all the required attributes, title, descriptions, examples

**Result:**

[1_result.yaml](JSON_schema/1_result.yaml)

### 1.2 JSON Schema - enums and simple arrays

Building upon the `MenuItem` schema from Exercise 1.1, extend the schema to include the following:

- **`size`**: An optional attribute that specifies the size of the menu item. It should be a string with one of the following values: "Small", "Medium", "Large". Default value should be "Medium".

- **`extraItems`**: An optional array that lists additional items that can be added to the menu item. Each element in the array should be a string representing the name of the extra item. The array can be empty and can have maximum 5 elements.

**Example JSON Object:**

```json
{
  "id": 456,
  "name": "Cappuccino",
  "description": "A delicious cappuccino made with our finest espresso.",
  "price": 3.50,
  "size": "Medium",
  "extraItems": ["Extra Shot"]
}
```

**Objective:**

Learn how to enhance an existing JSON Schema by adding enumerated values (enum) and arrays, ensuring that the new properties adhere to specified constraints.

**Result:**

[2_result.yaml](JSON_schema/2_result.yaml)

### 1.3 JSON Schema - complex arrays

Building upon the `MenuItem` schema from Exercise 1.2, extend the schema to include a `modifiers` property. This property allows customization of the menu item with various options.

**Requirements:**

**`modifiers`**:
   - **Type**: Array of objects
   - **Each object**:
     - **`name`**:
       - **Type**: String
       - **Description**: The name of the modifier (e.g., "Milk Type", "Syrup Flavor")
       - **Required**: Yes
     - **`options`**:
       - **Type**: Array of strings
       - **Description**: A list of possible options for this modifier (e.g., ["Whole Milk", "Skim Milk", "Soy Milk"])
       - **Items**:
         - **Type**: String
       - **Minimum Items**: 1
       - **Unique Items**: True
       - **Required**: Yes

**Example JSON Object:**

```json
{
  "id": 456,
  "name": "Cappuccino",
  "description": "A delicious cappuccino made with our finest espresso.",
  "price": 3.50,
  "size": "Medium",
  "extraItems": ["Extra Shot"],
  "modifiers": [
    {
      "name": "Milk Type",
      "options": ["Whole Milk", "Skim Milk", "Soy Milk"]
    },
    {
      "name": "Syrup Flavor",
      "options": ["Vanilla", "Caramel", "Hazelnut"]
    }
  ]
}
```

**Objective:**

Learn how to enhance an existing JSON Schema by adding complex arrays, ensuring that the new properties adhere to specified constraints.

**Result:**

[3_result.yaml](JSON_schema/3_result.yaml)

### 1.4 JSON Schema - oneOf

Building upon the `MenuItem` schema from Exercise 1.3, enhance the schema to include a `promotion` property that can represent different types of promotions applied to a menu item. Utilize the `oneOf` keyword to define validation rules for the promotion types.

**Requirements:**

1. **`promotion`** (optional):
   - **Type**: Object
   - **Description**: Details of the promotion applied to the menu item.
   - **Validation**:
     - **`oneOf`**: The `promotion` object must match exactly one of the following schemas:
       - **Discount Promotion**:
         - **Properties**:
           - `type`: Must be the string `"discount"`.
           - `amount`: A number representing the discount amount.
         - **Required**: `type`, `amount`
       - **Buy One Get One Free Promotion**:
         - **Properties**:
           - `type`: Must be the string `"bogo"`.
           - `description`: A string describing the promotion.
         - **Required**: `type`, `description`

**Example JSON Object:**

```json
{
  "id": 456,
  "name": "Cappuccino",
  "description": "A delicious cappuccino made with our finest espresso.",
  "price": 3.50,
  "size": "Medium",
  "extraItems": ["Extra Shot", "Soy Milk"],
  "modifiers": [
    {
      "name": "Milk Type",
      "options": ["Whole Milk", "Skim Milk", "Soy Milk"]
    },
    {
      "name": "Syrup Flavor",
      "options": ["Vanilla", "Caramel", "Hazelnut"]
    }
  ],
  "promotion": {
    "type": "discount",
    "amount": 1.00
  }
}
```

**Objective:**

Learn how to enhance an existing JSON Schema by adding a `promotion` property that can represent different types of promotions applied to a menu item. Utilize the `oneOf` keyword to define validation rules for the promotion types.

**Result:**

[4_result.yaml](JSON_schema/4_result.yaml)



OAS versions:

[Initial version](https://github.com/DXHeroes/oas_course/commit/fb8391b789b360007c5e29cdddb8c18ac52bcd41)

[First task diff](https://github.com/DXHeroes/oas_course/commit/c2233d7793e1f54603f79e2297125dd115a8e410)

[Second task diff](https://github.com/DXHeroes/oas_course/commit/a8191f9df8f96e464dec874e5b56260a0a1b78c9)

[Thirth task diff](https://github.com/DXHeroes/oas_course/commit/f382d93bc7d8bc6b32b8168392154ca42ec92337)

[Fourth task diff](https://github.com/DXHeroes/oas_course/commit/09e04d3d9bfae59c6d7e9cbf939963c32fcfbfa7)

[Fifth task diff](https://github.com/DXHeroes/oas_course/commit/75f46c928e91a3b7fe967cbc27052a47d79ce0b2)
