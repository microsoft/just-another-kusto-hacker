[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAE1PW2rDMBD89ykG/1guVlJ/ptAcoDlCCEVWFiv1Q0Za0wZ6+K4SQY00aHdm9qGrYTndSFDxLXK4zX2DkKO6OJe2bMpBcBKsglngcxyzRps8COR+ZIoyBYH7j4uHlzN8ruVsPG0KU5FJmsskw2zWQH4522x5KX5BP0zzFSPeEdfu+RkVG7w2aGvRJzOQ7oNZnHi0PiII+cj1ZNg6qFqf6aXFbofD4aKPqsYS/BdZRpSmk1kUNYip15aXSdbwpwnB3NO8qkqOb0eBRHcmohrWyL4Slv2CFt09FY00K2lW7PfPLWCdCYzbjP4WGdZPE838B9Fe3/esAQAA)

```kql
datatable (s:string, r:string)
["c","k","K","u","n","o","u","s","k","e","u","s","r","","J","u","e","r"," ","h","r"," ",
"s","t","t","o","s","t"," ","K","e","r","h","a","th","e","t a","n","o"," ","o","t","a","c"]
| extend l = substring(s, 0, 1)
| make-graph l --> r
| graph-match ()-[e*1 .. 99]->() project s = map(e, s)
| project s = strcat_array(s, '')
| where s has 'kusto'
| top 1 by strlen(s)

// graph chart in gist comment
```