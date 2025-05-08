[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAG2TUW/aMBSF3/kVR32pI7E1aUszNO2hRWzTVqpJRVslhJBJDLkisTPbEaXqj6+DA1VCn8+55577OenlwmJLMlVbM6FcGKukMPiGdCd5QQmb9YD4ug/g4gL/vBHDAdivwClRFPfbyhewyiuDtvIwBTNeuWkrT3/AbK1cXTZ7HkueCLCD4TIMw1ofxp0ekzEY95mhz/z8MJ7iu+aF2Cq9AZNejbz6tFTPyHklkwxMfVjmLxnLmz5ReN0WY7DMC03gKKey3EELS9phY8JndsYcE316Xw120DkoCsF+fwg2ipCRtF26ty+VFl2wE0q0MmplMRW8MMeLbQvGY6VXNeaf1bKBcdLvCOAH2drGk/8VGbKkZEPi+CTjdC0wyrQqqCqaVxkOG3GkSsqVRSqWlTsh8Qzjbtt7pUqwTYvw4f6rm8E7Xp96R3LtVnK7xzsPvvY0l64FYeVqIIRV4Frz3SIXcm0zdvKdB58iGCtKRL1XiGcrZApuEqKRSoX7CU4GZjR/d87Ok4zr87kzFnwjFsZq14g5dpvFfi87ZgWBGzNVUXBNLwITYQxf1xvcTMJtY9+n5O4DZIfooI+zs+ANunb356UDAAA=)

```kql

let windowsMilestones = dynamic([
  74,   // Windows 95 (J)
  117,  // Windows 98 (u)
  115,  // Windows NT (s)
  116,  // Windows XP (t)
  32,   // Space (Windows 2000)
  97,   // Windows ME (a)
  110,  // .NET Framework (n)
  111,  // Xbox launch (o)
  116,  // Windows Vista (t)
  104,  // Windows 7 (h)
  101,  // Clippy retires (e)
  114,  // Windows 8 (r)
  32,   // Space
  75,   // Windows 10 (K)
  117,  // Windows 11 hint (u)
  115,  // Azure (s)
  116,  // Microsoft Teams launch (t)
  111,  // Surface Hub (o)
  32,   // Space
  104,  // GitHub acquisition (h)
  97,   // Edge Chromium (a)
  99,   // Copilot debut (c)
  107,  // Microsoft Loop (k)
  101,  // Windows 365 (e)
  114   // Bing Chat (r)
]);
range i from 0 to array_length(windowsMilestones)-1 step 1
| extend asciiCode = windowsMilestones[i]
| extend ['char'] = make_string(pack_array(asciiCode))
| summarize Message = strcat_array(make_list(['char']), "")
```