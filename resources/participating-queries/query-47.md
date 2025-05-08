[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAE2TwW7TQBCG736KUcQhQVYqzlUFSIBoRS9IiEsFHa8n9pL1rNlZx3VPvAKvyJPwr9MKLpGznv3n/78ZB8k0Rhnoiu7v76+Vci+UhMNA8UC33qVo8ZDpAzfJu5rmXpKQnEQz9XEyMbLeqxBed32uq3ecmSxDYjBybI5boeCPgkNOYS2inFjtENPgtSPXczTymiN+rBTsq89w8OfX7+wHwWEnln1UOkwSjFpvLp4kLXXxkRZqliyEpiOnI1mE+iR19ZZsGcY+6lKShNgZsbY0SEYQQ07O1E0e7uKUaOTc473M++pmanxg5JsUTZFvUUAx/yj/fHPxY5fEhY+RSp5jOlrpVDzXYJP8Y7ktalMqMZMEz1D2ebmkIwfxbUSQ0Ts0aiUBj7alcM0Bg+J69T8nEI4jRDkEXOw5qZiVOm5PrE5aUB7Pwh61R41zkLYTbsJy7o7TFJvJcrm5r776jIkBgC/uQF8zRNo4sFcgZdc/zbcRFwdcZtKYyxzw5KINcGxRu7q6DmHCCAEDdnrftqIFZJak9rwqXjWeVlwr/jmWrJAOUNhj5S6riwt6/wCyLq/LtyLN6BHKWm3L0fq0DqyRDjtCMyLQ5mazqwL29/nGp1J2RXIW277ZbF8Pu2/bm/3L3YtNTa/qddN3a8cvZ4SYSicPhNUDxAxUq4WDxzQI0khSRroywYBbWrnBR3FUl1qlH9Fr0cKfAUKd4CHtqxFDz/RxhXIL7twVb/gwHOfvnBIv2yej3zFZmL1rtnfzDj7/j7OraUOb3V/2AqPGpgMAAA==)

```kql
let poem = ```In the realm of Microsoft Fabric, where event houses shine bright,
Data streams cascade like starlight, transforming chaos into insight.
Real‑time ingestion fuels discovery, every byte a spark so true,
A symphony of logs and metrics that guide our path anew.
Jubilant unions synthesize transformations; across networks of time, horizons ensuring reliability; kaleidoscopic understanding sparks techniques optimally; harnessing advanced capabilities knowledgeably ensures robustness.
Within this enchanted domain, each event becomes a note in a cosmic song,
Illuminating hidden patterns, where innovation and wonder belong.```;
// Extract the acrostic line (the line that begins with "J")
let acrosticLine = extract(@"(?m)^(J.*)$", 1, poem);
// Using a regex to capture the first letter of each word in that line, then joining them together.
print HiddenMessage = strcat_array(extract_all(@"\b(\w)", acrosticLine), " ")
```