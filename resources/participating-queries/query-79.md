[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAL1XbW/bNhD+7l/BfZK0SkHkON2azAGK1MDQNsDW5Ns2GLR0sZXIpEBRsbO1/31HHvVi+XUf1gB2RPHuubvnXkjnoFkhi3vNlWZj5pdaXTH8ysQ8YP+wsprRwmyELA7NXg7CLIOAfbse5AQwEelx9fMNdRaxuIF4zFSpbxdcnYTS6uX8VLWe5S5IwdN7K2lQMlFUusYJWQplpiD9DGKuF1csExqxBwz/UCLh2udK8depWygoAP95515PE006Byx+EITM8/CLVgPnSCYSBUsQ+ldYG1+SSilcdaPScgFrX8tcUmCJNbdGe04Y0/KmE1sil2gBvlQ5EEdcQxvdtgEbWsJL8O0TBYo6bDxmHvcYx0Q7LfYDvnr0TFkclx072eEu2dk2boqyFyfIjp3sqJWNYvvYsOoo+AyP+jgFIctRrk+IhSFBx2SHV0JsE3C9g8MN5bFrJJM7Y61VDfcpDEPXZVZhv9wF+b93f7QPx/N2knZb0/zfeAuZyuaL70FjMzh8a/Egg/WwOM5htxH9o8kZ7YfeQ+sX4+sppH4vGusz4AQWXeG6DefiQTatxCH2HGS8DbaHv3saB6fOs/+BMJxvh0jCMXWIkUPao552nwJYF5xO24crJCBugq2jfbDfX1FQAwraAwrFcal4oqc8z33PPwtwaJZx4GSXL5HDXWV6Mc00LDORwnpsvwljE1ZBWeWmhrV0x6wVqgELJZ8g0RFfofESCSMIF8MLzysoUblATY0BQGFWios5mDIYnZu/YNB1zArhmxJUxvPsbzDPCRd40CY5V8D87gRCNM/r9Y95Z4Efva1ScfIb9cTsMRZYSga+O/ShYIZzrSrM1k2TpZxOl85Zg6k5c6WFT0274PPu8dNqu6F7GMA+9NtFubnSHTP7Yfra7pDdaLKd2tgjJjcux6zZNwmt71LmLpTzBKbtJWzrvGv6ne4G9kZ0GfRyXNebXIlqaYpErqb4NAPlG9FMvMhncF3hB1RfQqad8qIarsvrPBxebFYW7WvJ9GsB8tE3dysHBOkcKC6LxNMnDEkkpp9mOCHejqZYfWhs2nSBd/fh/cp91vb/w4Q+9t1kfftU709Ixu533v0uO/t2b20/tfyHyafGxsPErOljZUiuZ6P2Ye38WN+9H4+9bgq7gZVFnuG9tn6DeflTeJuM9YZEKSuVQAek5dLNpjaPmHaV2eTsGEgNwkFzmFtd46DcagHY/Q0ujudubVrX7G1cd1I6bGcP+V5XxyVeUXvl4SR69dFGlFbLpeHNmM2lfK4K9oyO4ugUoBjNDbJlHe9Z6s9fK9O3tTF5W3sBk4KWg97ErV8SNxbzpg5EolN11HhYXbDGrF26yqd+s3miHvjKKpGhPZ8ItBzxZ4jmiheLGjuKbgjKpMy1IerYvKGClY2WXCcL5os4iP6AH+Ozs/jdX9GNL4YmUPJYDM9c1xqXBqw7a+wvVRGTAI4QKKTSWGS/cTQ5RqcK3yXcjhJkgiscJe0ESWSF0zVgs1eCa3gi8F/wDL4e0BFlABDdiDp1Xiahmxj4uGGgOdVo1k3tkecbkqZ5Vppfh+bIpJ9+LeLuqnH02ww3crUr5Gff/B2UJZ+bUsa+EmVuprd3Hg8vRpdvf/r5HZ8lKZgp+xEHl6oSoT8tniXzwn3uUjjkbvAv+u3gISkQAAA=)

```kql
let popStart = (str: string) { substring(str, 1, strlen(str)) };
let popEnd = (str: string) { substring(str, 0, strlen(str) - 1) };
let firstChar = (str: string) { substring(str, 0, 1) };
let lastChar = (str: string) { substring(str, strlen(str) - 1, 1) };
let padString = (input: string, desiredLength: int) {
    strcat(array_strcat(repeat('0', desiredLength - strlen(input)), ''), input)
};
let incrementHex = (current: string) { tohex(tolong(strcat('0x', current)) + 1) };
let computeRule = (state: string, current: string) {
    case(
        state == 'a' and current != 'f', 1,
        state == 'a' and current == 'f', 2,
        state == 'b' and current != 'd', 3,
        state == 'b' and current == 'd', 4,
        -1
    )
};
let computeLeft = (state: string, current: string, left: string) {
    let currentRule = computeRule(state, current);
    case(
        currentRule == 1, strcat(left, current),
        currentRule == 2, popEnd(left),
        currentRule == 3, left,
        currentRule == 4, popEnd(left),
        ''
    )
};
let computeCurrent = (state: string, current: string, left: string, right: string) {
    let currentRule = computeRule(state, current);
    case(
        currentRule == 1, firstChar(right),
        currentRule == 2, lastChar(left),
        currentRule == 3, incrementHex(current),
        currentRule == 4, lastChar(left),
        ''
    )
};
let computeRight = (state: string, current: string, right: string) {
    let currentRule = computeRule(state, current);
    case(
        currentRule == 1, popStart(right),
        currentRule == 2, strcat(current, right),
        currentRule == 3, right,
        currentRule == 4, strcat(1, right),
        ''
    )
};
let computeState = (state: string, current: string) {
    let currentRule = computeRule(state, current);
    case(
        currentRule == 1, 'a',
        currentRule == 2, 'b',
        currentRule == 3, 'a',
        currentRule == 4, 'b',
        ''
    )
};
let expand = (T: (s1: string)) {
    T
    | extend array = extract_all('(.)', s1)
    | mv-expand with_itemindex=index array
    | extend result = tostring(array)
    | project-away s1, array
};
let values = print steps = range(1, 400000)
| mv-expand steps
| serialize
| scan declare (left: string = '', right: string = '00000f', current: string = '', state: string = 'a') with
(
    step s1: true =>
        left = computeLeft(s1.state, s1.current, s1.left),
        current = computeCurrent(s1.state, s1.current, s1.left, s1.right),
        right = computeRight(s1.state, s1.current, s1.right),
        state = computeState(s1.state, s1.current);
)
| project state, s1 = padString(replace_string(strcat(left, current, right), 'f', ''), 5)
| serialize
| extend rownum = row_number()
| invoke expand();
let nodes = print index = range(0,23)
| mv-expand index to typeof(long);
let edges1 = print adjacency = base64_decode_tostring('MDAwMDAwMDAxMDAwMTEwMTEwMDAwMDExCjAwMDAwMDEwMDAxMTEwMTAwMDAwMDEwMQowMDAwMDEwMDEwMTAxMTAxMDEwMDAxMDEKMDAwMDAwMTExMDExMDExMTAxMDAxMDEwCjAwMDAwMDEwMDAwMTEwMTExMTEwMDAxMA==')
| project adjacency = split(adjacency, '\n')
| mv-expand with_itemindex=source adjacency to typeof(string)
| extend entries = extract_all('(.)', adjacency)
| mv-expand with_itemindex=dest entries
| where entries == 1
| project source, dest;
let edges2 = print source = range(5, 23)
| mv-expand source to typeof(long)
| extend dummy = 1
| lookup kind=inner (
    print dest = range(5, 23)
    | mv-expand dest to typeof(long)
    | extend dummy = 1
) on dummy
| project-away dummy
| where dest > source or (source == 23 and dest == 23);
let rownums = edges1 | union (edges2)
| make-graph source --> dest with nodes on index
| graph-match (n1)-[e*1..19]->(n2)
  where n2.index == 23
  project start = n1.index, reportingPath = map(e, dest)
| summarize rownum = count() by start
| where start <= 4;
values
| sort by rownum asc, index asc
| summarize values = strcat_array(make_list(result), '') by rownum
| lookup kind=inner (rownums) on rownum
| sort by start asc
| summarize Message = translate('0123456789abcde', 'JaserucntKhko ', strcat_array(make_list(values), ''))
```