[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAK2QQU+DMBiG7/yK3ihmGlcXE7PsojHLri5Z4okU+k06S0vKx4TFH28pdDITPckFWt4+z/dWAZKKW5yTFSnird6dxNNjkZUPt3y96+IlidSYYD6xecZ5fvdy3KyL4pWhyuViFS99SEBuBIielPEa7hfpsJOiqdFK/Ua9KLlIs7/TbExza3nXk+tKSaRBNSNxPE2wnwk2SUgtoB3mi4h7KmdBgm450v3uJymP19BWXAv3Dw3BrgKzp8NQSQjVYCVX8gREitYhrPlIdVNmYOmljv2iY/+sOxipQQRZo6XR58az72ECz1gkWedpvM4HxF5qrrZeHDgjNZxqypLbfgoLdaP6Lm7OnGPqK9GSv0OqZI0Uk8nFmwarBgNyahm50CK4/u5leY6+xfhNY3pzlcQz4joMzvOVVNYcIMfvU8toEEVfg2YjptQCAAA=)

```kql
let part1 = h'SnVzdCBhbm90aGVy'; 
let part2 = h'IEt1c3RvIGhhY2tlci4=';
let decoded1 = base64_decode_tostring(part1);
let decoded2 = base64_decode_tostring(part2);
let array1 = split(decoded1, '');
let array2 = split(decoded2, '');
let indexed1 = 
    print t = array1 
    | mv-expand t to typeof(string) 
    | serialize idx = row_number();
let indexed2 = 
    print t = array2 
    | mv-expand t to typeof(string) 
    | serialize idx = row_number();
let joined = 
    union indexed1, indexed2 
    | sort by idx asc;
let finalString = 
    joined 
    | summarize result = strcat_array(make_list(t), '');
let output = 
    finalString 
    | extend extracted = extract('(.*)', 1, result) 
    | project extracted;
output

```