# Seemli Litium MediaMapper
Documentation site for Seemlis Litium Media mapper. The mapper that is fully flexible with Litiums datamodel, and is 100% configurable by you, the user.
No need to ask a developer to add a specific configuration to suite your changing needs.

*Note:*

*Mapping is triggered by uploading of new files. If you happen to upload to the wrong folder, a mapping will **not** be triggered by simply moving the files to the correct folder. Instead remove the files and upload them again.*


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

The configuration id is required and must be in your schema. This is how the mapper will know what configuration to use for the importing file.

Example:

I have a configuration with `id = disp`

I have a schema like `{id}_{variantid}_{name}`

I have a file that i have renamed to fit the schema `disp_variant1_a nice name.jpg`

The mapper will now match the `{id}` placeholder with the importing file and use that configuration.

## Delimiter
The delimiter is simply the character that is put in between the schema placeholders.

Example:

I have a delimiter like `_`

Then my schema will look like `{id}_{variantid}_{name}`

And the name of the file again, could look like: `disp_variant1_a nice name.jpg`

## Schema
The reason for having the schema builder, is so that you have 100% flexibility in how you name your files to match the mapping to be made.

The schema is build using placeholders. There are pre existing placeholders called system placeholders, and then there are user placeholders. Read about them [here](#placeholders)

## Root folder
The root folder, is the folder in which the configuration is active. Only in this folder will the mapping for the configuration take place. So make sure that you upload your files in the correct folder.

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

**Root folder:** `Product images`

**Path:** `{variantid}/{id}/temp/{myplaceholder}`

**Schema:** `{id}_{variantid}_{myplaceholder}_{name}`

**file name on import:** `disp_variant1_123_nice file name.jpg`

The file will then end up in the folder:
```
- root
-- Product images
--- variant1
---- disp
----- temp
------ 123
------- nice file name.jpg
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

An import runs on a file with name `nice file name.jpg`, it will therefore be renamed to `nice file name2.jpg`

## Media template

Select the media template for which you want the imported file to have

## Media fields

If you want any mapping of placeholders to fields in the media template, this is where you will do that.

As of today the mapper only supports fields of types:

`Text`, `LimitedText`, `MultirowText`, `MultiField`

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

## User placeholders

The user placeholders are created by you and mapped by you. Maybe you need to map a ceratin value to a specific field in a multi field, or a field on the field template, or maybe use it in the destination folder path.

Example:
You have created a new placeholder `{myplaceholder}`

You have included the placeholder in the schema `{id}_{variantid}_{myplaceholder}_{name}`

Now you configure a media template field to map to your new placeholder
*Insert image of the mapping of placeholder*

*Note:*

*You are in control of the user placeholders. Be careful to not delete any placeholders that are used in configurations.*