[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAH2STW+cMBCG7/kVIy7Y6oayLAvmECn3HHLY5VRVXgPTQBYwwt5mW/HjOwbUfEmZgxl5nnf8eswwNr0FBXdwOp1uhBBAcRBHWoODcPEYAKz7ACuxAFQ/euDlxHwkFuD/rvu+I0j6AF8S89FfEgD5grg8Xz18dLogbg0IIcOfiBVx13Dhzf3mgBv4HPniyoWb2ATd71u8Dqqv5imaoW0sUxtf+JyKLzWOSIVO2bJGAyM+4RXu/Ycpnw7TcXr0CcKrRZIXJLe60peiRTbi0KoS5SxgtTK1NLXaMquNpSd7YorzDfg/1O2vnz4lPufwHQb9woaG8U0c8tfGzlfRWINWlvrSW6l7NNSJXp4VpPsGUUS0uXSdGpu/OAs6dUbZNoYuQwcV73aKN83PVKF0VKWVqm3Zvc+CgJMlb79NM5FluzBK4zQWsdiJMMmybbiNdyKmWiJ2YZzu9yJJ0n0SicjjyzzVMLR/qLPugb26Or+1sLg/c+4kw6ifsVx+40vflLpC6ZbBQUZaLdehGRwbNFJVFT0RkPofniwePP8CAAA=)

```kql
print a = ```
888    S8T   .S88888O.  888      
888   S8T   S88T" "U88O 888      
888  S8T    888     888 888      
888S88K     888     888 888      
8888888O    888     888 888      
888  U88O   888 U8O 888 888      
888   U88O  U88O.U8O88T 888      
888    U88O  "U888888"  88888888 
                   U8O        ```
| mv-expand a = split(a,'8')
| where a matches regex @'K|U|S|T|O'
| extend b = todouble(replace_regex(hash_sha1(tostring(a)), '[a-f]', '')) / pow(pi(),40)
| extend a = bitset_count_ones(toint(b)) + 22
| summarize a = make_list(a), b = make_list(b)
| extend k = extract_all(@'(..)', "51798993027474848380699101438479868304755866756282")
| mv-apply k on (summarize k= make_list(toint(k)))
| project a = unicode_codepoints_to_string(series_add(a, k))
```