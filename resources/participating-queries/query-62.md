[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAI1TTW+bQBC9+1eMUKSASiND0sRN5VNOvedWVWgD45gYL3RZrKTqD+ih5/7A/pLusB8ebFQVyfb6zcybx5vZBjWgLNsKq8+yGzSsoVO11FAJLWAB5llDlC2z5dJ88mwJ+XjK6AscOp4JHwMjno8VFs/C2fzmjmrEj2deawlDzrGXbz3HT3//Sxvvy3lO+zLcvvnytNestujTojGekqOP4qlBYx9Zqekc12TxvbE3hU5ojUre99rY/Zwsvoxe335MASJGHaV2CHc5BZhGH7i9cwEvMlR88FROsQ+srlkFp1q5iuChD1y75sGs0Jz3mMhdBbnZNHBjA0FwaM5e0BrpK46WTKlWN16uGy0Fvlr7FR5Q9fjAphAmsvhhVrx9wVL7IaQwDsaWOuxhO8hdb+r47TCl+KpRVj6LEvquqXVMQ04hgigBMGn7w3t87QTP1C3otw7bTexmDv96mMpyK1ThaOh+OkIrt8Lp5eXqDcdLW0vY1bJa11KiOjemlXDR4EZfTbus4ULVz1t95RAmh3nlmj8aU2jPcc4p4hWl4TAZg6wppaCvzijTfaHbwtphL0diCvthvxeq/o6wx74XzzQ9k1MKXQilxFu8FzssmrrXcSBPjPdRYlUd6n4QzYwZTpGNM0cVdo0o0QsZt2sOm8G5a0YC7SDtgFtReqKMsD+/fwU0yi3yM0qOor4NrcaKibJvHF9Gl+mJ4hQMODVqMzTNWe2ZW9MeZBm8A3JtfseDj7rtS9EIFVuEqXYjL46DCrlsNxK2PScV/t3+AhXuWjyIBgAA)

```kql
let encodedInput = print data 
    = "10100010210 20001010010 10001020010 20000101010 10201000010 20101000010 10020100010 20100100010 20000101010 10020010010 20100010010 10020001010 10201000010 20101001000 20001010010 10001020010 20000101010 20100100010 10201000010 10020010010 20101000010 10001021000 20101001000 20100010010 10020001010";
let codeTable = datatable(input:int, pattern:string)
[
    69,  "20100010010", 
    72,  "10020010010", 
    67,  "10001021000", 
    75,  "20101001000", 
    83,  "10001020010", 
    85,  "20001010010", 
    32,  "10201000010", 
    65,  "20101000010", 
    78,  "10020100010", 
    74,  "10100010210", 
    82,  "10020001010", 
    79,  "20100100010", 
    84,  "20000101010", 
];
let reverseCodeTable = codeTable
| project pattern, input;
let patternChunks = encodedInput
| extend patterns = split(data, " ")  
| mv-expand patterns to typeof(string)                             
| project char_pattern = patterns;
let decodedInput = patternChunks
| join kind=inner reverseCodeTable on $left.char_pattern == $right.pattern
| project input;
let decodedText = decodedInput
| extend character = unicode_codepoints_to_string(input)
| summarize message = strcat_array(make_list(character), "");
let visual = patternChunks
| extend visual_pattern = replace_string(
    replace_string(
        replace_string(char_pattern, "0", " "), 
        "1", "▌"), 
    "2", "█")
| extend quoted_pattern = strcat('"', visual_pattern, '"')
| summarize full_pattern = strcat_array(make_list(quoted_pattern), " + ");
encodedInput
| extend visual = toscalar(visual)
| extend decoded_message = toscalar(decodedText)
| project decoded_message, visual
```