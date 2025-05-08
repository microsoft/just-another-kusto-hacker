[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAGWSP2+DMBDFdz7FiSlIDA2pOqRi7NKq6pKtqqIDToFibMs+lFD1w/f4q0DtxXc/+96TnhUxvKNuUZ0wUwQpFMiy5bxjuvHRs6v0JYZTZ2kpPlxB7lhpjoLPAGSFqA2X5MIYwrr1bOSQxCPSdH3R7Lp9D7V5G/HDhiYrup8o3bCxioang0Bv4x9ONnhWRmVLXM09TKTEvF65fZzAq5R37VkoI14PeprABZsGN/KzSEGKt2xxbn2ljF7NnD1M5WLiEHw9B3chBb9wlYE0ZAJpOl+UvumDgawbEwL0OUjXOvNNOUMfqJS+Fc+u+iFw5K3Rvo9dos2Rz+gcdrsGazqryvPwByKxAmH0BzCUn8QrAgAA)

```kql
let ManualTable = datatable(text:string, Type:string, Order:int)
[
    "another", "kusto", 2,
    "newEntry1", "noKusto",0,
    "newEntry2", "noKusto",1,
    "example1", "otherType",1,
    "example2", "otherType",2,
    "alpha", "noKusto",3,
    "hacker", "kusto",4,
    "Just", "kusto",1,
    "beta", "noKusto",6,
    "gamma", "otherType",3,
    "delta", "otherType",1,
    "epsilon", "noKusto",4,
    "Kusto", "kusto",3
];
ManualTable
| where Type == "kusto"
| order by Order asc 
| project text
| summarize response = strcat_array(make_list(text), " ")
```