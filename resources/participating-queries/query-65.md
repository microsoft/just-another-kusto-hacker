[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAM1U7W7aMBT9n6e4yp8kEg4wus+qL7KqikxwS8CJPcdpYerDz/a9JmEa1Sa16hwBPvfjnGPnCikstMr0oqrVRsANpCVjDMrSf0pgMAe3ZW7noiFWgntcYO4eVk5LfcmcSnyP7/JJX55eJ/IkxaXe8rWDN7Dh1j1rKXKXtsJ8g96apnuA2cRWDBbJbQJuZTybeaPpLKC1R8zJepzViBiiDeVCaSZCn9sjzX2AsfQhlDIq3WKOSBtEJLhDecZOTHsSxV6JeeptkZd6O6wkpDA3EmmixtYfZCk0Z4ZoUaQngyFlQ+GJZaCDYeUjVSLLEylg7kD3g7kjHWNk+k4OUGYZD+4Lsg+kgmgVVQK6itc3Un2MIc+VfYovLaDPUSagL3QriL4SYuOLW8SQZ0/Bf83T5O460W5MpgOdPIM4WNFtzoe817Kx+RgKJIUr1kbtRG0Zf+JHCGTVwoXbRyYOmp/TWAX2qIW6z+N0PoNUaj/o38dcdeeW+qFtuWl+Cmj5XlSy6S2N/8QD7Ph+67z62a+5zcPJ/7Qob9WgtTB5P6zRT26ElrwWFUGraIOnx7aKG8OPubdQoQW8C//tfm4Xd8XMX3DqQ4sZLIuCXsJL6w09LP9G3hoputfWLtxfnD/+RfkwiBfWxabXMLmcXNCL7t5nhlb/wQyt3nGGVv84Q286K1ejmUs6xS9pHmuwFQgAAA==)

```kql
let morse_code = ".--- ..- ... - / .- -. --- - .... . .-. / / -.- ..- ... - --- / .... .- -.-. -.- . .-.";
let morse_alphabet = datatable(letter: string , morse_code: string)
[
    'a', ".-",    'b', "-...",  'c', "-.-.",  'd', "-..",   'e', ".", 
    'f', "..-.",  'g', "--.",   'h', "....",  'i', "..",    'j', ".---", 
    'k', "-.-",   'l', ".-..",  'm', "--",    'n', "-.",    'o', "---", 
    'p', ".--.",  'q', "--.-",  'r', ".-.",   's', "...",  't', "-", 
    'u', "..-",   'v', "...-",  'w', ".--",   'x', "-..-",  'y', "-.--", 
    'Z', "--..",  '1', ".----", '2', "..---", '3', "...--", '4', "....-", 
    '5', ".....", '6', "-....", '7', "--...", '8', "---..", '9', "----.", 
    '0', "-----", " ", "/"
];
print morse_code
| extend morse_code = split(morse_code, " ")
| project-away print_0
| mv-expand morse_code to typeof(string)
| lookup morse_alphabet on morse_code
| summarize make_list(letter)
| project jakh =  strcat(
                        strcat(toupper(substring(replace_string(tostring(split(strcat_array(list_letter, " "), "  ")[0])," ",""), 0, 1)), 
                                substring(replace_string(tostring(split(strcat_array(list_letter, " "), "  ")[0])," ",""), 1, 
                                strlen(replace_string(tostring(split(strcat_array(list_letter, " "), "  ")[0])," ","")) - 1)),
                        " ",                        
                        replace_string(tostring(split(strcat_array(list_letter, " "), "  ")[1])," ",""),
                        " ",
                        strcat(toupper(substring(replace_string(tostring(split(strcat_array(list_letter, " "), "  ")[3])," ",""), 0, 1)), 
                                substring(replace_string(tostring(split(strcat_array(list_letter, " "), "  ")[3])," ",""), 1, 
                                strlen(replace_string(tostring(split(strcat_array(list_letter, " "), "  ")[3])," ","")) - 1)),
                        " ",
                        replace_string(tostring(split(strcat_array(list_letter, " "), "  ")[4])," ","")
                       )
```