# Introduction

Welcome to the documentation for Seemli Litium MediaMapper. This tool is designed to facilitate flexible mapping of media files, tailored to Litium’s data model. Before diving into the configuration steps and features, it is essential to understand a few core concepts that are fundamental to using this tool effectively.

## Core Concepts

### Mapping
Mapping refers to the process of associating media files with specific elements or fields within Litium’s data structure. This allows users to organize and integrate media files within the system effectively, ensuring that each file is located and utilized appropriately.

### Schema
A Schema is a structured framework used in the tool that defines how media files should be named and organized. It is built using placeholders and determines the format in which files are imported and recognized by the system. Adhering to the correct schema is crucial for accurate and effective mapping of media files.

### Placeholders
Placeholders are symbolic representations used within the schema to denote specific segments or components of a file name. They act as variable containers that are replaced with actual data during the mapping process. Placeholders are instrumental in building the schema, allowing users to create flexible and dynamic naming conventions. For example, `{id}` is a placeholder that could be replaced by the actual id of a file when it is mapped.

### Configuration
Configuration is the process of setting up the mapping parameters, schema, and other specifications that determine how the media files are processed, mapped, and integrated within Litium. Proper configuration is essential to align the tool’s functionality with user needs and system requirements.

### Root Folder & Destination Folder
- **Root Folder:** It is the initial folder where configurations are active, and new files are uploaded for mapping.
- **Destination Folder:** It is where the files will reside post-mapping. It is defined during configuration, determining the hierarchical structure and location of the mapped files within the system.

### Media Template & Media Fields
- **Media Template:** It is a predefined structure that dictates how the imported file should be formatted and displayed within Litium.
- **Media Fields:** These are specific fields within the media template where placeholders can be mapped, allowing for the incorporation of varied data types like Text, LimitedText, MultirowText, and MultiField in the media file.

By understanding these core concepts, users can leverage the full capabilities of the Seemli Litium MediaMapper, configuring and managing media files with precision and flexibility within the Litium environment.

Now, let’s proceed to the detailed sections to understand how to implement these concepts and effectively use Seemli Litium MediaMapper.


# Seemli Litium MediaMapper

### Table of content

- [Mapper types](#mapper-types)
- [Configuration steps](#configuration-steps)
    - [Id](#id)
    - [Delimiter](#delimiter)
    - [Schema](#schema)
    - [Root folder](#root-folder)
    - [Destination folder](#destination-folder)
    - [Media template](#media-template)
    - [Media fields](#media-fields)
- [Display image mapping](#display-image-mapping)
- [Product field mapping](#product-field-mapping)
- [Placeholders](#placeholders)
    - [System placeholders](#system-placeholders)
    - [User placeholders](#user-placeholders)


# Mapper types
This product supports the following types of mapping

- Product field mapping
- Display image mapping
- Media field mapping

# Configuration steps
These are the general steps that can be configured. Note that the different Mapper types might have other steps of configuration - you will learn more about them further down.

- [Id](#id)
- [Delimiter](#delimiter)
- [Schema](#schema)
- [Root folder](#root-folder)
- [Destination folder](#destination-folder)
- [Media template](#media-template)
- [Media fields](#media-fields)

## Id
Placeholder: `{id}`

You must include the configuration id in your schema. This lets the mapper know which configuration to use when importing a file.

Example:

We have a configuration with `id = disp`\
We have a schema like `{id}_{variantid}_{name}`\
We have a file that i have renamed to fit the schema `disp_variant1_a nice name.jpg`

The mapper will now match the `{id}` placeholder with the importing file and use that configuration.

## Delimiter
The delimiter is the character used between schema placeholders.

Example:

We have a delimiter like `_`\
Then our schema will look like `{id}_{variantid}_{name}`\
And the name of the file again, could look like: `disp_variant1_a nice name.jpg`

## Schema
The schema serves as the blueprint for your file naming convention, allowing the tool to correctly identify and map each file based on its name. It is constructed using [placeholders](#placeholders), which represent the different components of the file name. The effectiveness of your mapping process heavily relies on correctly building your schema.

### Using Placeholders in Schema
#### System Placeholders
System placeholders are predefined and have specific meanings and functionalities within the tool. For instance, `{id}` represents the configuration ID, and `{name}` represents the name of the file. 

- **Example with `{id}` Placeholder:**
    If your schema is `{id}_{variantid}_{name}`, and you have a file named `disp_variant1_productname.jpg`, the `{id}` placeholder will be replaced by `disp`.

- **Example with `{name}` Placeholder:**
    For a schema like `{id}_{variantid}_{name}`, a file named `disp_variant1_productname.jpg` will have `{name}` replaced by `productname`.

#### User Placeholders
User placeholders are created by you to add flexibility and customization to your schema. You can create a user placeholder to represent any specific data point or identifier in your file name.

- **Example of Creating a User Placeholder:**
    If you need a placeholder for a specific product attribute, like color, you can create a user placeholder `{color}`. 
    For a schema like `{id}_{color}_{name}`, a file named `disp_red_productname.jpg` will map `red` to `{color}`.

- **Example of Using Multiple User Placeholders:**
    You can combine multiple user placeholders to create complex schemas.
    Schema: `{id}_{color}_{size}_{name}`
    File: `disp_red_large_productname.jpg`
    Here, `{color}` will be `red` and `{size}` will be `large`.

### Tips for Building Effective Schemas
1. **Be Consistent:**
   Maintain a consistent naming convention across all files to avoid mapping errors.
   
2. **Use Descriptive Placeholders:**
   Choose placeholder names that accurately represent the data they hold, making the schema intuitive and easy to understand.

3. **Test Your Schema:**
   Before implementing a new schema, test it with a few files to ensure that all placeholders are working as expected and the files are mapped correctly.

4. **Optimize for Scalability:**
   Construct your schema in a way that can easily accommodate new placeholders and changes in file naming conventions.

By being very careful and paying attention to every detail, you can create an accurate and flexible mapping of your media files to meet your unique needs and preferences.

## Root folder
The configuration is active only in the root folder. Ensure you upload your files to this folder for proper mapping.

The folders are fetched from Litium, so if you wish to create a new folder, you need to do so in Litium BO, and then reload the configuration.

## Destination folder
The destination folder configuration is built up by three parts.

- Root folder
- Path
- Overwrite existing file

#### Root folder
Select the folder, in which you want the file to end up after the mapping is done. You can then build a path to narrow down the structure with folders, see below.

#### Path
This section is similar to when you build your schema. You can make use of the placeholders, or simply write a free text word (press enter to add). The path will then create a folder structure in which to save the file in.

Example:

**Root folder:** `Product images`\
**Path:** `{variantid}/{id}/temp/{myplaceholder}`\
**Schema:** `{id}_{variantid}_{myplaceholder}_{name}`\
**file name on import:** `disp_variant1_123_nice file name.jpg`

The file will then end up in the folder:
```
+ root
  |
  +-- Product images
      |
      +-- variant1
          |
          +-- disp
              |
              +-- temp
                  |
                  +-- 123
                      |
                      +-- nice file name.jpg
```

*Note:*

*Above example have mapped the `{name}` placeholder to the file name field, see [here](./examples/name_to_media_field.md) for example*


#### Overwrite existing file

Check this box if you want any file in the destination folder to be overwritten **(deleted)** in case it exists with the same name.

Otherwise the code will rename the mapped file with a suffix.

Example:

Two files exists in destination folder:
```
nice file name.jpg
nice file name1.jpg
```

If an import runs on a file named `nice file name.jpg`, it will be renamed to `nice file name2.jpg`

## Media template

Select the media template for which you want the imported file to have

## Media fields

If you want any mapping of placeholders to fields in the media template, this is where you will do that.

Currently, the mapper supports only `Text`, `LimitedText`, `MultirowText`, and `MultiField` field types.

**Multi fields:** That includes a field that are of any field type that you see above.


Read [here](./examples/name_to_media_field.md) for an example of mapping the `{name}` placeholder to a name field on the file

# Display image mapping

Display image mapping does not have any unique configuration as of today other that the ones named above. But will map to Litiums product image container instead of a product field.

#  Product field mapping

 *Insert image of chosing product field mapping*

The product field mapping has some extra configuration steps to make.

## Product field selection
This is where you select to which field you want the file to map to.
You will only be presented with options of fields that are of types:

`MediaPointerImage`, `MediaPointerFile`, `Pointer`, `MultiField`

**Pointer:** With any of the pointer options:

`MediaFile`, `MediaImage`, `MediaVideo`

**Multi field:** That includes a field that are of any field type that you see above.

## Product field configuration
You can configure different things depending on the field type that you select.


#### What about multi select fields?
As of today the mapper will just append to the array if the field is multi select.

### MediaPointerImage
Just maps the file to the field

### MediaPointerFile
Just maps the file to the field

### Pointer
Just maps the file to the field

### Multi field
The multi field is a special case. Here we need to make use of our [placeholders](#placeholders) again. The idea behind this mapping is that we fetch the fields in the multi field, and then create a mapping of field -> placeholder.

See [here](./examples/multifield_configuration.md) for a more detailed example.

# Placeholders
There are pre existing placeholders called system placeholders, and then there are user placeholders. System placeholders are there to exist and have a tight coupling in the code. The user placeholders are there for you to have some extra flexibility. Let's see an example further down.


## System placeholders

- `{id}`
- `{name}`
- `{variantid}`
- `{baseproductid}`
- `{file}`
- `{sort}`

#### {id}

The `{id}` placeholder is linked to the configuration id.
Read about the id configuration [here](#id)

#### {name}

The `{name}` placeholder is linked to the name of the file. This placeholder is not required, but it is probably a good idea to include, well depending on your use case ofc. Read here about an example where we map the name to the name field of the file, renaming it after the import.

See [here](./examples/name_to_media_field.md) for example.

#### {variantid}
The `{variantid}` placeholder is linked to the variant id, i.e the article number. Include this placeholder in your schema to map files to variants.

#### {baseproductid}
The `{baseproductid}` placeholder is linked to the base product id. Include this placeholder in your schema to map files to base products.

*Note*

*If the schema both include `{variantid}` and `{baseproductid}` the mapper will prioritize `{variantid}`*

#### {file}
The `{file}` placeholder is linked to the actual file itself. There are not many use cases for this, but there are one for example.

You are creating a configuration that will map files to a Multi field.
[See example here](./examples/multifield_configuration.md)

#### {sort}
The `{sort}` placeholder is used to be able to set a sorting when mapping to an array.
\
It's zero-index based, meaning the first place in the array is index 0, second is 1, and so on.
\
For example a mapping to display images could look like:

**Schema:** `{variantid}_{id}_{sort}`
\
**filename:** `artnr123_disp_0.jpg`

The above configuration will make the file end up first among the display images for variant `artnr123`

**If no sorting is in the schema, and the mapping is for an array entity (display images, array pointers, etc) then a default value of 0 will be used, which means it will be placed first in the array**

## User placeholders

The user placeholders are created by you and mapped by you. Maybe you need to map a ceratin value to a specific field in a multi field, or a field on the field template, or maybe use it in the destination folder path.

Example:
You have created a new placeholder `{myplaceholder}`

You have included the placeholder in the schema `{id}_{variantid}_{myplaceholder}_{name}`

Now you configure a media template field to map to your new placeholder
*Insert image of the mapping of placeholder*

*Note:*

*You are in control of the user placeholders. Be careful to not delete any placeholders that are used in configurations.*