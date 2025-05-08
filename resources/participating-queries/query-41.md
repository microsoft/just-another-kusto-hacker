[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAI1T226jMBB95ytGPIFEtviCgVaR9rnNH6xWkUPc4AbsyHbapurH7zjJJkGrlWIkYGbO3M6BQQXoeuk8PuegPoOTXVjKYch+ptmPPC0ghecX2al+a6zzYZ/mT8kQk+y40kYGbY2HeQJ4nDQbBRpenR2BQLB480HtgBzD37G8MmtYEGx1blrAgk4sNrH4xKqu1rni+D5Tnzt5KooNw2Gn7Gvmg9Nmk/8LoveA2D0gfg+o+i9o5+yb6gJ8WLfGrTDYyZAtSOQjshB3jxvnU+p66fvluxwwJb5mMf0syDE0ytD1ZznWMuC1GhRkf9MeYbBmU8DOeh2VewRtQg6/jvh4ZlyUtGG1qEjd0KalosRRygLg4QHS570PkF7ADWlZy6tStIJyWtdlXUQ37hDB0tjQX8EzQWvBOBEtoYwRQSkVBdBzZeXgZX8DbsqK1mXbUlZywbFRHIGdCnvkdFKYVDUVNScNKxnjNW9wDg6nwrLbKncC/35Kbj/a5BverDaw1WY918bgCDcUWnPhOpmqdWUPA2hj3upw8YH0Hfr9fhyl018KvDKoXKcuIi+lc/KQjXKrloP24aQh/mdpnvwB9Vfc2o4DAAA=)

```kql
let charset = extract_all(@"(.)", " JKacehknorstu");
let combinations =
    range i from 1 to 1 step 1
    | extend L1 = charset, L2 = charset, L3 = charset, L4 = charset, L5 = charset
    | mv-expand L1 to typeof(string)
    | mv-expand L2 to typeof(string)
    | mv-expand L3 to typeof(string)
    | mv-expand L4 to typeof(string)
    | mv-expand L5 to typeof(string)
    | project word = strcat(L1, L2, L3, L4, L5)
    | extend hash_val = hash(word);
let hash_match =
    datatable (hash_val: long, position: int) [
        -4602837651782892603, 0,  // "Just "
        819394506962427707,    1, // "anoth"
        -6276341691233162226, 2,  // "er Ku"
        -805270992304648190,  3, // "sto h"
        -6157267418303347487, 4   // "acker"
    ];
combinations
| join kind=inner hash_match on hash_val
| project word, position
| order by position asc
| summarize sentence = strcat_array(make_list(word), "")

```