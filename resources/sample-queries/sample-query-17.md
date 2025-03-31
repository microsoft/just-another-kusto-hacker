[Click to run](https://dataexplorer.azure.com/clusters/help/databases/ContosoSales?query=H4sIAAAAAAAAA1WRTU7DMBCF95V6h2lWtkiltPQX1BU7EHCAKKBpMk5dHKc4jogK3J1xS4qIF5HG7828b2zIw4462ECUTKbXs%2FliuVrjNi9IRbfDgeFrdF4rzH3Q3Ndt48lBvkNtR71C6a5sdcECUd5A4522pYRPcHQwmNOro5I6UcYQpWqcRfyPJHyzuUDPZ2tIBH9vjeFIrr4Bbb2EFCKVTK%2FVbInjfDJT4%2FVcLcbLYqnWqFaqmC%2B4XwLZcPAF1HmyBTj84CjeoW0MehLMF18o4j7taaSUwXdw9Z4Y8MCihq3cx7H0FY0RkUhfRtmV5CncV56zBdO%2B1hbetC022lpyrdXvLYEYDoC%2FP7AHXtiZJYa3C1Pymzlov6Ak3%2BQ7qrAvNG1VodNHAosVcaJKW3FXm7ayT1zgFLz28A58g93%2Fm5Av4HM8L%2F58z67QFk0ABpBQ2wtIT%2F9ITYNlmMbPkKMXp3WkSRafUsTn9aSTrJ%2FeV6aZ%2FAHd3LnGRwIAAA%3D%3D)

```
let hex = "0123456789abcdef";
let artifact = "Jouster chain!";
let fixguid = (g: string) { replace_regex(g, "[f-]", "") };
datatable(guid: string, zero: int) [ "f023f47a-c14f-95f6-7d7f9af8fd56", 0 ]
| extend raw = translate(hex, artifact, fixguid(guid))
| project parts = extract_all("([^!]+)", raw), zero
| join kind=innerunique (
    datatable(Kusto: int, k: int) [ 0, 0 ]
    | getschema
    | summarize name = min(ColumnName), letter = max(ColumnName), zero = toint(min(ColumnOrdinal))
  ) on zero
| project Message = strcat(parts[0], name, parts[1], letter, parts[2])
```