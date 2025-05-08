[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAJVV71MiORD9zl/RN/eF2UKHAWrr1KKuVm8Vf66KC4plUZlMgGgmmUoyIp73v19nMrCoW94tHygmme5+/d7rJorgXDPDpOVyCsFRYSwQqeyMaTjGBwUzQh+YDjZrUQR/sQmXDFJmuGYpqMLmha0JZvGmPPpWnkD3o0w77wO+S04VZsXAwv8cu69ccWnNeKJVNjZWI8L6q7Bwx4H6YiDHGlgIdCEwCXuyTEsiUmIJcAMIAkyR50pbljZgxiRlQOCRaE4SwWDO7awMXwaCL7ZZAt0lhn3uHMqqr5vWYJH2Bk0ynBej65k43Itjmj3d3wzP1Kj/xdL2riHXF9OT4c2U9C6btHf6+WSxtbi5psWoJZqkN+Dp9Zmg2dljIi9FIi+Km9aWPWkeCSovbD/bL77vbV2NhmdXN+2jnPYun0/aR2IkTx/JwWA26p0+JsP9POFb5+nBTFC+xUfD/fuk1Smw1tPh15lIDp4e++3Bc3rwR3kW7EAUrbNS31PSoubbVafhbTCzNjfbUaTJfHOKhBRJYZim/r1NqrJol2m7cUTkedRntE81z62JNJuYaMZIaqKMcBl9c3pH96j3RiX+xoMTf8OLvxFv5iYO7jzn9YnSGbHdwD7ZoAF8KpVm+1wbe8mo0ml3nwjDvMp9y3KIt+GcaMOAOzkaYDWRRhDLIHfHKXzXAtBpxdJPRKaQFFykpb6+2Y+8CQlxaZQs3991kd5qV6VTJoWklivpnVFCSZfOSEqfjFNW2teqyrBr9gl31sIc0i6sXivxo+mzDCGPBU5ZfS19A4I5l6mamyC87dy9TWRVNUD/PT+rmCrHuxa7sJyxbUgXkmScNjzdS89UpyH8XQP8oARTFARcFWg69onWZDEWTE7tbJkshA2IUQAnYhn2ArlW94xaGDC9OFFyuqdEkcnVBtEsF4SyJXCKPNY5dLsQt5GO46BRpilPWi08eahOTJG87bVRQUIK2dNYTervmUMvObKWcG/5XRg2IHZfQYzeDCAIa/94zhDi+Q+63jJY/+lma/xELW/sKzSaX6SgJpXNgRIJgqNLP/BqA51t0afEuiVnlQJGzAI0n87sn7/BduiyY1XLcaPhnMyZ3i7xuxqxy/vFpy2z9sqk2M9ad7UXZBMdqfkz87XP1bx8CRmmxI5LWusZeWBjh7b+Mykdg4FvtUceyxny0398cdJAlU0hLA6qZs5JqcrQbbbsP2FVc34Y4yZ+gGqG456CxlnAxV7FA8kZ0rsJv7sjbh781Zzo1I9qPxfcDnGluL8Y4x7qOHqUCKLrH9HxAhabQx94B3j994s1l75zv8f5zu1u/eIyGhBRsHh98n9Au/UWdDTUQ/gEnfAO65YRrV+OaP9yROf/R3gevsr0gGRuBlaMvHJMSlWBkTyEZFE1vmxnCXJZGuPmSD1b8dNdk+y2eVcu8iUTr+7itbv2m7vW2l3nzV37rrYSZaXmK1vnaIHq58fgK3PUfqw0n3CnliOXFlZOqwgL/wWPpLxpdQkAAA==)

```kql
// Presenting "Just another Kusto hacker".
// Define desired output
let DesiredOutput = "Just another Kusto hacker";
let DesiredOutputUnicodes = unicode_codepoints_from_string(DesiredOutput);
// As per the rules externaldata is not supported, hence a variable with the external string.
let Base64Input = "Y2VydHV0aWwuZXhlIC11cmxjYWNoZSAtc3BsaXQgLWYgaHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0JlcnQtSmFuUC9TZWNTY3JpcHRzL3JlZnMvaGVhZHMvbWFpbi9PdGhlci9iZWFjb24ucHMxIEhlbGxvS3VzdG8ucHMx"; //externaldata(Content: string)["https://raw.githubusercontent.com/Bert-JanP/SecScripts/refs/heads/main/Other/just-another-kusto-hacker-1.ps1"] with (format="txt", ignoreFirstRecord=False);
// Step 1: Parse input, translate parsed Url to unicodes and build the string "Just another Kusto hacker" based on the BuildOutputTable function.
let ParsedInput = base64_decode_tostring(Base64Input);
let ParsedUrl = tostring(parse_command_line(ParsedInput, "windows")[4]);
let ParsedUrltoUnicode = unicode_codepoints_from_string(ParsedUrl);
let BuildOutputTable = (Desired: dynamic, inputContent:dynamic) {
    range i from 0 to array_length(Desired) - 1 step 1
    | project VeryLongColumnOutput = replace_string(case(i == 13, "K",
    i == 22, "k",
    substring(ParsedUrl, array_index_of(ParsedUrltoUnicode, toint(Desired[i])), 1)), "1", " ")
};
let OutPutTable = BuildOutputTable(DesiredOutputUnicodes, ParsedUrltoUnicode);
// The output of Step 1 can list "Just another Kusto hacker", but that is too easy right?! :)
// Partial answer:
let Step1JustAnotherKustoHacker = OutPutTable
| summarize KustoPower = strcat_array(make_list(VeryLongColumnOutput), "");
// Have fun with KQL, results are random, it can be that in the 10000 created rows no result apears. #no risk no reward.
let SplitWords = split(toscalar(Step1JustAnotherKustoHacker | take 1), " ");
let FunOutput = range i from 0 to 10000 - 1 step 1
    | extend Value1 = tostring(SplitWords[toint(rand() * 4)]), Value2 = tostring(SplitWords[toint(rand() * 4)]), Value3 = tostring(SplitWords[toint(rand() * 4)]), Value4 = tostring(SplitWords[toint(rand() * 4)]);
let EndGame = FunOutput
| summarize dcount(i) by Value1, Value2, Value3, Value4
| where Value1 == SplitWords[0] and Value2 == SplitWords[1] and Value3 == SplitWords[2] and Value4 == SplitWords[3]
| extend Output = strcat_array(pack_array(Value1, Value2, Value3, Value4), " ")
| project Output;
print toscalar(EndGame)
```