[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAE2NPW7DMAxGr0J4ioFvEB1HP0OukKEXMJxYMIQakmHLKXKTbF16wB6hlJOhAEVCfN8D5yXETB/h9rmkaQpxpDPlpY/r1Gd/qH6/f54VqLr4u19oTDH2NIa7p0faaJtB/8Hk874f0lcU6dqvXrfd4G9p8F1Oa5Zb42GLYV+UNie5vgrr3tAewaxgNbhpwEpBG2j5qRbOynA4GbQWzsDwK8cwR2gnokbr4CQiRGy2hUis2OVZQWrPsbIlyEpMlqrr+g//Zl4LCgEAAA==)

```kql
print Rickrolling = translate("🤘", "Never gonna give you up, Never gonna let you down", base64_decode_tostring(unicode_codepoints_to_string(83,110,86,122,100,67,66,104,98,109,57,48,97,71,86,121,73,69,116,49,99,51,82,118,73,71,104,104,89,50,116,108,99,103,61,61)))
```