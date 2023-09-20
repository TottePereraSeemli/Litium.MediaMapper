# Example of a multi field configuration

Lets say that we have a multi field that includes two other fields:
```
{
    FileName: string
    TheActualFile: MediaPointerFile
}
```

#### And that we have a schema like:
`{id}_{variantid}_{name}`

#### And an importing file name like:
`disp_variant1_very cool file name.jpg`


If we want our mapping to work for this specific example we create field -> placeholder mappings like the following:

``` 
FileName : {name}
TheActualFile : {file}
```

That is all we need, and the mapper will take care of the rest.