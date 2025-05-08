[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAA9VU7W7aMBT936ewUCUSKW0JG9W%2BmEYhQOhogQYoX0KGuJASEmrMCKh%2F%2B0J7jj7UrhND0xK28bNUsRv7%2BN57Ts61TRjKoDSaz2yLSQM8J%2Bcf%2ByYZuibpM3fOqOWMJJiGmElH6IDf2dlRrJzLLINHE0%2FGKxvw8DWYYwrHaF6wrm3W4dGWAU4LMIZ%2F3n8P9mC%2BXY6q9VKupjUKHFNLjEs3E1Y26qlKPZ%2B%2Fqau1RsM2W83GbNyaXk04pt1sO7hgP%2BCkxwbTz8vhbWltFhtJ88M4RZxlIsgFedcih6F7Iu%2FKXze0lI9Zi1ruOa4u9gXWKHsCkwhibM5O1GDWw7zEXkbE0kRu3bvO6eE4fG8daLTN5b%2B%2FjqPD66FfKR2TZQXFHmPy1yMb7HABdjAxg7%2BBTST9S2ACGXUOjRzvPD89%2Fz7mg8QHlQ9JPnzig7zd7T0%2FxQ8N3kOPiHiMOCYqQcEUOyMiJRSEKcWrvk2cERtLGflEVZAqA3b664R4MwzwLMAzCsrBVELMRWw1I%2B6dZLtAMlCAIyA2xUPWx7YtxaVTOa4Adj7ENqbSBcRbjgklPEgaJeF1Rt17MmRItEqWp7StqcUgu4iae2%2B6%2FtyrazZK10uAZ0OCCn4KxHmjslAmmToPlNHgZG6rKXM5SLqU0XekvlRjhKvZYiLqMPane4lWh2iJIHse%2Ft1%2B2qgyvqX9OjafuO7jxSawU%2FzSEoBYOJbrAJtHNHcpQ4MVUMfzIQfAxJcX0ymm1pqgJhyZ4gnp29acSXWFVyeHklAys%2FGQ9CkZEU%2Fa3sRNSPgj3ul2urGu0u31wJWxWNhrAaUCRH9j0kQouM4v%2FJBRhSatXdvDjztfl%2Fd0m5rakb8VZYGdRgtV01JQ25d0DExLAC6m1YBGMbKgTVF5IPuu%2Bmn%2FPVWM8vEVwIv%2FK%2Ba9azloYjlm2iZ3zF0wQtHbeyps4kq0BarRN18lBCnvZVEVLECiMI9qFIfyXwxR5dvbfNdbb5ShS15ztRyHUOi6hwVBUmF3CxZlBC1ZjGYOzmupUEyoH9pgRsFg08M6b14%2FzDHX9vSaa3lMrdGYneqh9avQegXOu9SECiBA6R%2FdXw3ybQo0xqRGHhYWJeaNLxcX%2FJDr4A8Ot1yP1AkAAA%3D%3D)

```kql
let A = split(base64_decode_tostring(strcat(
                                            //
"MDAwMDAwMDEwMDEwMDAxMTAxMDAwMTAx",
"MDExMDAxMTExMDAwMTAwMTEwMTAxMDEx",
"MTEwMDExMDExMTEwMTExMXwgQUJDREVG",
"R0hJSktMTU5PUFFSU1RVVldYWVphYmNk",
"ZWZnaGlqa2xtbm9wcXJzdHV2d3h5enw0",
"MTAxMzEwMTExMTIxMDExMDEyMTAxMTE5",
"MzExMDExMjEwMTUxMDEyMTIxMDExMTMx",
"MzE0MTExMTEyMTAxMTk1MTAxMTIxMDEx",
"MTEyMTAxMTAxMjEwMTExMzEwMTIxODIx",
"MzE0MTEwMTEzMTExMDEyMTIxMDEzMTEx",
"MTEyMTAxMTI",
                                            //
"=")), "|");
let B = datatable(I:string) [
                                            //
'[̲̅$̲̅(̲̅1̲̅2̲̅8̲̅)̲̅$̲̅]̅'
                                            //
] | extend J = range(0, array_length(A)-1, 1) | mv-expand C = A, D = J to typeof(long);
let C = extract_all('(.)', toscalar(B | where D == 2 | project strcat(C) | limit 1));
let D = datatable(I:string) [
                                            //
'[̲̅$̲̅(̲̅1̲̅2̲̅8̲̅)̲̅$̲̅]̅'
                                            //
] | extend L = range(0, array_length(C)-1, 1) | mv-expand K = C to typeof(string), L to typeof(long) limit 256;
let E = D | where tolong(K) > 1 | extend T = range(0, tolong(K)-1, 1) | mv-expand T to typeof(long) limit 256 | extend U = 0;
let F = toscalar(D | where tolong(K) <= 1 | project U = tolong(K), L, T = 0 | union E | sort by L asc, T asc | summarize W = make_list(U, 256) | project replace_regex(tostring(W), @'[\[\"\,\]]', "") | limit 1);
let G = B | where D == 0 | project I = strcat(C) | extend Y = extract_all('(....)', I) | extend J = range(0, 15, 1) | mv-expand Y to typeof(string), J to typeof(long) | project Y, Z = tohex(J), H=1;
let H = extract_all('(........)', F);
datatable(I:string) [
                                            //
'[̲̅$̲̅(̲̅1̲̅2̲̅8̲̅)̲̅$̲̅]̅'
                                            //
] | extend J = range(0, array_length(H)-1, 1) | mv-expand N = H to typeof(string), J to typeof(long) | join kind=leftouter (B | where D == 1 | project P = strcat(C) | extend Q = extract_all('(.)', P) | extend M = range(0, array_length(Q)-1, 1)
  | mv-expand Q to typeof(string), M to typeof(long) | project Q, M | extend O = tohex(M, 2) | join kind=innerunique (G | join kind=inner (G) on H | project P = strcat(Y, Y1), I = strcat(Z, Z1)
  | sort by I asc) on $left.O == $right.I) on $left.N == $right.P | order by J asc | summarize W = make_list(Q)
  | project TheRequiredString = replace_regex(tostring(W), @'[\[\"\,\]]', "")
```