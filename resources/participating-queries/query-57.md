[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAI1TTW/UMBC951dYOSXgSp582abigNQDgr31WK1WbmLRQJKNEhdYPv47M5PspkCF0K6ixH7z5r3nceeDuPH1sfHitUiaV6I5Da5v6zT6Hgkh7t3sq+LQMOIQjnOY2uFD8ji0vECP8dgOYca9w7rZpGn08zrqkPnW15MPM1I3LuDvvvPUYwGm0R21ELEpJCgtSy0NSFNKU0ldSFylF0VPo+lZWMQV0ir6pgrcrLioMNJkjM14A5SSOpcmJzoA3KqIr7LMAVpaI0uQVSUhU9LSGhYY4qFSY6gJAkCB1ESJcJRjqbEmtRUBNJAqUJbRisVRM6t5EQA3oaReKLGifyzFapmNIlXFylEYeQV6Zw0FJ5AvZpBHa86jlCVaUlyr2C87RFNYSDlVrJU92DU1UkSExrIqbZh0CRGf5BwFa1gqIacvMpMp7mwNl5Wkw1JUGA5FkGVLytyXza+JFaSRggOV/+m62mJS3FyVfAh4Ilu4oM6HwFEbOkl9LoOlzDKEymkzW3xqkqcXt5Ax8hJ8tF8m8sZ3be+Dn3Am46v4vEiD3KzTesvTifuXcceX2nVuSqIVEv0Q/mvwQyPmsWvDOvk05/ydNFLEMk4R1n++cuPYnYTvfO+HcIZcSo6DSDid+bHv3dR+88JNkzshsHef/KFr54AC8I4lKwVeL2L+8uCnM/bBzZva/AXol6DSTeRyfRukXJwmXEWArenut4ZrBUHG6fjR10/vMvapXTgwSbKTW6Zpmj4X6A4ZL9E8l/VTiutoxKUg3r15/5bOYHLD3Lngl5AuJv/ucKf26Tpo/0LBf6GyPYb8C2CyelgcBQAA)

```kql
let Decode = (d: dynamic)
{
   base64_decode_tostring(unicode_codepoints_to_string(d))
};
let Secrets = datatable(d: string)
[
    "84,107,57,81,85,86,74,84,86,70,86,87,86,49,104,90,87,107,70,67,81,48,82,70,82,107,100,73,83,85,112,76,84,69,49,117,98,51,66,120,99,110,78,48,100,88,90,51,101,72,108,54,89,87,74,106,90,71,86,109,90,50,104,112,97,109,116,115,98,81,61,61", 
    "81,85,74,68,82,69,86,71,82,48,104,74,83,107,116,77,84,85,53,80,85,70,70,83,85,49,82,86,86,108,100,89,87,86,112,104,89,109,78,107,90,87,90,110,97,71,108,113,97,50,120,116,98,109,57,119,99,88,74,122,100,72,86,50,100,51,104,53,101,103,61,61", 
    "86,50,104,110,90,105,66,117,89,87,74,110,100,88,74,108,73,70,104,111,90,109,100,105,73,72,86,117,99,72,104,121,90,81,61,61"
];
let Delimeter = "-";
let DecodedSecretsString = tostring(toscalar(
Secrets
| extend split_strings = split(d, ",")
| mv-apply element = split_strings on (
    summarize array = make_list(toint(element))
)
| where array has tostring(3*17+10)
| extend decoded = Decode(array)
| summarize L = make_list(decoded)
| project Secrets = strcat_array(L, Delimeter)));
let DecodedSecretsList = split(DecodedSecretsString, Delimeter);
print JAKH = translate(
    tostring(DecodedSecretsList[0]), 
    tostring(DecodedSecretsList[1]), 
    tostring(DecodedSecretsList[2])
)
```