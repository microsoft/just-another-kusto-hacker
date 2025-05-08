[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAEVQXW+DMAx851dYfQItkcrHClO1X1JNUZR6EAoJSoy6TfvxcwpTX2yf7845ZUKCSDoQvMPxnE0JYrAYGS/a3JQOQX/nbSOgqQXISkDJrWvE6ZXH+gF5kmUlZL1tZFeJJG6qpyFJ2jfRplUrgFvH0ykZinMWtOsRLHwGP8MRyMPjWTWh62nIt0SFLDkqLlBmv4BfhO4KI8fc4r/suS/240mbgfng78qsc1znfCyYW4If0dBGrs4af0WVyuKto6jIq0jBuj43Q9KzcdbB/mAKBeyZ9Q3VZCPtgv+D7DKa9h/jKuBwKP4AhWsERGEBAAA=)

```kql
let start = 0;
let series = pack_array(74, 43, -2, 1, -84,65, 13, 1, 5, -12,-3, 13, -82,43, 42, -2, 1, -5, -79,72, -7, 2, 8, -6, 13);
range i from 0 to array_length(series)-1 step 1
| extend j = start + series[i]
| extend ch = row_cumsum(j)
| project ch = unicode_codepoints_to_string(ch)
| summarize arr  = make_list(ch)
| project strcat_array(arr, "")
```