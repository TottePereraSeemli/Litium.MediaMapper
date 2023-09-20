## Name to media field example:

The files that we are importing with this configuration will later be used on the product page for customers to download. In that case we can't let the file name stay like the name that I use when I imported the file.

Let's use the example that we had earlier above.

#### Schema 
`{id}_{variantid}_{myplaceholder}_{name}`

#### File name on import
`disp_variant1_123_nice file name.jpg`

Now we only need to make sure that the name field is present on the selected Media template, so that we can create the mapping. (hint, you to that in Litium BO)

And then we select the name field and map it to the name placeholder `{name}`

*insert image of mapping to the name field*