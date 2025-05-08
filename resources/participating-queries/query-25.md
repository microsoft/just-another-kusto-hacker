[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAH2QzW6DMBCE73kK3wwSrcpfbzkUVDWRuEU5o41tJW4hINuJDOrDd01bER/A0iKL+Wa0417JqyFFTLaEHqS9VB9HzQZ7odGGTKdInMQP9lbt9pqX9nOWUichfa/KN30arJqlbHKV9qV613pf2maWcifhr67aHTWUdqBk802ENeLKCXebnECL16zmgnVc1KbTBrc8B0Uc/ofg4ckKmXhkukKmHpmtkJlH5itkHs6FwBXCuwJmamiagAbPIY2w6GMcJAuUVwTSBcorAdkC5RWAfIF6XH4kCI2yDyCOcEecFCfDmaj2/iRsDw6cPbqRTKANH4MBRisFQzBGhFJn0be2BSVHQVp9RkqJvgEm6r+n80wtfIm6kdoEU2Y4ZeAnor9pP5cvL7O8AgAA)

```kql
print B1 = 'SixhLGUscyxh',
      B2 = 'dSxuLHIsdCxj',
      B3 = 'cyxvLCAsbyxr',
      B4 = 'dCx0LEssICxl',
      B5 = 'ICxoLHUsaCxy' 
| extend d1 = base64_decode_tostring(B1),
         d2 = base64_decode_tostring(B2),
         d3 = base64_decode_tostring(B3),
         d4 = base64_decode_tostring(B4),
         d5 = base64_decode_tostring(B5)
| extend a1 = extract_all('(.)', d1),
         a2 = extract_all('(.)', d2),
         a3 = extract_all('(.)', d3),
         a4 = extract_all('(.)', d4),
         a5 = extract_all('(.)', d5)
| extend z  = zip(a1, a2, a3, a4, a5)
| mv-expand z
| extend slice = strcat_array(z, '')
| summarize msg = replace_string(strcat_array(make_list(slice), ''), ',', '')

```