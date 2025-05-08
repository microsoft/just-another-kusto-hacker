[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAF2Sz04bMRDG7/sUI58SaSUKRJUatAfoH8SBC1RIVYWQY0+yRl47siekQRxQ71Uv7aEIiRMSL1DB8+QF4BEYexNIu3vx2jPf983Pa5HAGXcqtwNBBVoSvwOLnUg47oNxVIJUZLzrQ6Rg3KhbfC2An/USxAdUXiNQjRBRBdZqMEY5Qni6+f338eHn/PLH/M93XogyN21w0+cgXRz60IAhmBqq2wDQyJFR3Hh7P7++W9Rvcv221jA0GGYwtNIErvh1uzju8fEBnqG0OcPEkmkkcaAwYdmnm6tLURxvFZaDtfn2F/EqEIfu6Fy/36kHzbs3cvdotveR1tXmwdnebl1/2SCrRlUltmBtDXZkxLc9QJeG1csRs6rOAPSr7CDXnrT7J+RbZp1/3LtZdYXdqmJmsZ9RVIm4ktQRCUoaG0T5nyUDyEBShWiFE6+WaOZVLK+3uAD8Rug0BIyMivUVp803DVWVYL6aly/eh+lYpG8cs1s/rds/ottNdiv8h8bxyk9oPCGQlFugx77TGgPCi1Fq+2QsYQDyEGs/Be/sbEWjTcid4+BPUdFy4xmGnZjFrwIAAA==)

```kql
let ninjaArt = datatable(step: int, action: string)
[
    1, "Decode the secret message 🕵️‍♂️",
    2, "Transform it with ninja magic 🥷✨",
    3, "Add fiery flair 🔥",
    4, "Reveal the ultimate truth 🚀"
];
let secretMessage = "SnVzdCBhbm90aGVyIEt1c3RvIGhhY2tlcg=="; // Base64 encoded message
let decodedMessage = base64_decode_tostring(secretMessage); // Decode the message
let ninjaMagic = strcat("🥷🔥 ", decodedMessage, " 🔥🥷"); // Add ninja flair
ninjaArt
| extend result = case(step == 4, ninjaMagic, strcat("Step ", step, ": ", action)) // Reveal the final output at step 4
| where step == 4 // Filter to show only the final result
| project result

```