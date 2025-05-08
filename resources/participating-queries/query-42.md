[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAI1S3WqDMBS+9ymCMFCo0Vh1duB7bIwhUWObtTElxk3HHn4n0Yoru5i5kJzv75wkYYhOWl/7pzA8cn0aKlxLEQpeK9nLVofvQ68D2kl9Yio4w0YGJ1qfmQq1YiwUlHdOQzWs6sK8Wjbs+anXinfHHTK7l2XnvzouwREmGY7cHbKfmxCcPuKDLTluikmeYxIlC8PAWQwai8Y4zUAd3eRzIY7yGSaYPOY4Wc0BjpObluB9hqNNcGq0WbJx3qJQOKxd2abjfGMcxThJMCHxTDBdbvUu5JJ0NrX2e2zGOsTrWJCOs1trQIaZ78ZaOiMQtc9hkCX+rmAIewwOyylYwrbgvDnfSHwEbLzSrkFn3jUFVYpOaCyOTJa8a2XZKilKfi1p0yjW914rlaAaKh/JfJ++v0PT//kvvg+p/SAEVfyLQZSW8xvwBD2z8sJ77Y3+K3mzvn+AkwVRNdkX9Lw8JGPKFKcXY8qbQvCulK2n5GfZDaJiygM/EvkPJEIBQUBno2Yw9lj0Q7WErGkjkHkDAtvEH4RpJdxNsx3CaLd9A/Wq5DurNYKzGS66ALeaam/+lfbwvXHnuiB1EVzZL2AygP8DYBEOnJMDAAA=)

```kql
// https://github.com/microsoft/just-another-kusto-hacker/tree/main
datatable(codeX:string, codeY:string)[
"1.0.16.0",      "41.57.96.0",
"5.188.104.0",   "41.62.0.0",
"2.56.160.0",    "2.56.208.0",
"1.178.4.0",     "2.24.0.0",
"1.36.0.0",      "5.56.64.0",
"2.56.0.0",      "2.59.96.0",
"1.0.128.0",     "202.44.112.0",
"41.66.0.0",     "24.152.56.0",
"23.88.192.0",   "45.5.60.0",
"14.1.100.0",    "2.56.4.0",
"102.38.248.0",  "102.38.248.0",
"103.14.208.0",  "103.14.208.0",
]
| mv-expand kind=array x=geo_info_from_ip_address(format_ipv4(codeX)), y=geo_info_from_ip_address(format_ipv4(codeY))
| summarize x=tostring(make_list(x)[1]), y=tostring(make_list(y)[1]) by codeX, codeY
| serialize id=min_of(row_number(), 10)%10 -1 
| extend x=substring(tostring(x), id, 1), y=substring(tostring(y), id, 1)
| summarize x=make_list(x), y=make_list(y)
| project result=strcat(strcat_array(x,""), " ", strcat_array(y,""))
```