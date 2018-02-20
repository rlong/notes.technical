


https://stackoverflow.com/questions/13315131/enforcing-the-type-of-the-indexed-members-of-a-typescript-object


```
var stuff: { [s: string]: string; } = {};
stuff['a'] = ''; // ok
stuff['a'] = 4;  // error
```


-------------------------------------------------------------------------------
