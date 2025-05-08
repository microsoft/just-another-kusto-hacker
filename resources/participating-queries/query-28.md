[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAI2Sa2/aMBSGv/MrokrV2qkruQAJk9DkMMgFwpIACTBNlZ2Y3BNwnEDQfvzMtGkfV1u2bJ33OfZ57e9BngQZRyuONOWPp5jSU/253w8hhfh6yiuCySu8NQS/BlXRD/KmppjU/awNPo2VIsyEa4dgcEaEtMf4FbIwgXkCMazp7yQI1rjuW93XP+sv5waTbqIPagP8bQPRsf1HcT51QKeF0mieQx9YrdvxU/6rOdazs+UCb5Z0lU3Xy3RjukHmns8VQ/R0JSyXhuLrg+OjqMo7ucIDBU2BttiiG01PpBpexAMLjbV0JJz1wjnUNzPVb+TYMt7M/FHOr4Yef9f45mpxKkidLuPk2Hp8ZpP6OvS2G78r0VGxNwODl0laKOPt0bko3kaySO65x8bE6GYkU7VE7nxYLr+ZkbKr51J1TQFkeUeZrEdiOaNjvZK9gzzlG+AsHdUCRqvNU6ZYyGFiRfFsc7F3s/VYi9Lham1fmSuqkHRszuzRxRMtpQK2Zy1tzSldR4mZBeocULktWC3g5l2BA8Bzr3ciSUk5wE24u+ejwVuIgyrEb7Ri75OU0dPDeq3GaK0uwt2KN7RZFOhme5DMGPlCHiRqtd8dckObN0hyq8POiPZiHKNilRu6d4P+sDRmVAgktzX08IS0S7Qvtmx4KRIFxsXxXqQsD5g8PPd+cidIasxlSRlOCM7hFYfsbpeExtxHjnuAxQOnCtwH1tn2v/IYtpgB4ruBpmYVM0J6N4GYW8X9kME/hP2kFAeUYwYGkD6pwgu7w4sqvdxVz71f1Lohf0gDAAA=)

```kql
print A = base64_decode_tostring("SSBhbSBKdXN0IGEgcHJvZ3JhbW1lciBoYXZlIGFub3RoZXIgY2hhbmNlIHVzaW5nIEt1c3RvIHdpbGwgYmUgYmVjb21lIGhhY2tlciA=")
| parse kind=relaxed A with *  "am" B1 ' ' *  
| parse kind=relaxed A with *  "have" B2 ' ' *  
| parse kind=relaxed A with *  "using" B3 ' ' *  
| parse kind=relaxed A with *  "become" B4 ' ' *  
| project strcat(B1, B2,B3, B4 )

```