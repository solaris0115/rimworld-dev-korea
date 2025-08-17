# Hair Settings

All of the tags on this page, go in the tag `hairSettings`
```xml
        <hairSettings>

        </hairSettings>
```

First we define if the race even has Hair *(human: `true`)*
```xml
            <hasHair>true</hasHair>
```

You can also define at which age the hair of your pawns gets grey/gray. *(human: `true`)*
```xml
            <getsGreyAt>50</getsGreyAt> 
```

It is also possible to set custom `hairTags`. Set the respective tags in your `HairDefs`.  
*Note: this will overwrite faction `hairTags`*
```xml
            <hairTags>
                <li>exampleTagHair</li>
            </hairTags>
```

```xml
            <shader>Cutout</shader>
```

## Resulting HairSettings
```xml
        <hairSettings>
            <hasHair>true</hasHair>
            <getsGreyAt>50</getsGreyAt>
            <hairTags>
                <li>exampleTagHair</li>
            </hairTags>
        </hairSettings>
```