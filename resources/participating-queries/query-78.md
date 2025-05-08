[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAMVVaY/bNhD9vr9iYKBYG1GC3SK9NtgCzTY9cjTpfWwDgxZHEmOKVEjKx7b97x2SkkXJu0CKFqg/GJY4b+bN45uxRAdPGpG/0ljDJVhncubmJ0Cf2TOhSq5rC7qAldT52mawrdAgML5B5VqDFlpVaMmz39UsiyjODOHgbYvWWRAKGGy1kRyshhWFPhhCb5BJ3VoomLLAtkw42ApXQSkRk4x7ZEb5nIU24CqEmpUi97/2FC8lWETKOgCQGgLJFLc5a5BY54YVDnnMnjOTZle4BUNEqE/cNVIb5BmscK8Vh1zXDUUnlK1jJvT3lOVreCzpO6MOSRV9aoGjFGXlkuyt2qCQHmAxNxgV8T00YoeSeVLKQ5ISnXJEH1bMOekbKIxAaqcSjQU3KSGx9GckrlF99kKKfI2BqJyk31JjaHq9Q7ywUBpfz3axQ/RLtWWGR63f6NYo3Gf0ZHRbVv4+DlRztiGiaeNUJXDxkh2c419ww0qtYGU8JGUWboeKsBJDTnqRxdIFyyO2VWult2pUSLjOHLmXiqKE8UZGVVK+ivnmCJIU2pGDzNpGdo32RcgBNvjZaSiE4iMR6r11JGZwuycts15njo2rbOTIxSb1FZPSI3wfhfbEeqkP08AkIRJapRR17a+G5q3SDQ5ViC0J7d8Hs6Q6r5HcTu3HXoQRIewwoD6FnTigy0qm8Y2Ltm6qeIUVoklSWx1HuSJ8FgdPbwT6/P7Bj+WD2cni0YmkJUIep25pgzRSuHm/UjKYUb4uBFWuOfJljdb6K76EUIecRw+CPK5rOPMXQCPG9ksZLnAeEi/gPpzTpWID5wH0Jw2row5CXcoUoq7F6/FhIYx1y7xihkKEKOYx+hJmM2IG9GXbFVmFugxHGZxlcL5YdFlsW5NRxA3SgrCtdIcFuQwM5zVb41IK6+ZDoQUlvqPhJa0jGag4HX/OJxEdjua8cMsNk22Q9BB9rNTHvSaHlrkohQsgodx8aG92/slHH5w9PHtITYvYZNrgpOTQWci3GBHr9Jxfn/pfp68vINbI4vkFec4t4I8gokcx2VRshW4p9RY9csZWOceirMSbtayVbt6Seu1mu9vfzB4dw9qmibDPHl99/uSLL7/6+umz5y++efnq2+++/+HHn37+5dffEhgNL+4OpcKTLuZjDhn03BdTYF/sCBgObgXSP0jqsZTAp5feUcMtTGmMgu9F/RbwHrz/ob+iOIe3fIYyke6dZTrSo+DjMkNTXVd9Ryd/xXvn6G16xdAycyWaKig0Ne/EBp2ZLoDvFatF/v85IrJP987xIBF12jdH83jn2ukV8yvhIPsE3Q3aGBi08ahEo2tBdzFaeunpYrLU/qHBbwO/s8nH4P/K6Pc7Fe6RAd/B7f/e8ncUTHx/tPGPTXPH6u9F6Re/TzQBj8cozXk8WFMTdX8a46GiMtMSfwMTCNjfyQsAAA==)

```kql
let EpicPoem = strcat(
    "Kingdoms of blocks, where adventures unfold,\n",
    "daring quests in a world so bold.\n",
    "zealous fans await with glee,\n",
    "yearning for the magic they will see.\n\n",
    "epic landscapes, crafted with care,\n",
    "new realms explored, beyond compare.\n",
    "starring Jack Black, a hero's delight,\n",
    "unveiling secrets in the pixelated night.\n",
    "quests and battles, friendships tight,\n",
    "legends born in the flickering light.\n",
    "wonders await in this grand sight.\n\n",
    "Onward they journey, through forests and caves,\n",
    "under the stars, where the dragon braves.\n",
    "with courage and wit, they face the unknown,\n",
    "uniting forces, their strength has grown.\n",
    "x marks the spot, treasures to find.\n\n",
    "mysteries unravel, in the depths they dive,\n",
    "allies and foes, in this world so alive.\n",
    "glimmers of hope, in the darkest of nights,\n",
    "keeping the spirit of adventure in sight.\n",
    "in the end, triumph and cheer,\n",
    "soaring high, the movie of the year."
);
let lines = split(EpicPoem, "\n");
let encoded_message = 
    range i from 0 to array_length(lines) - 1 step 1
    | extend line = lines[i]
    | extend first_char = iif(line == "", " ", substring(line, 0, 1))
    | summarize result = strcat_array(make_list(first_char), "");
let encoded_message_scalar = toscalar(encoded_message);
let shift_values = toscalar(range i from 0 to 8 step 1
| extend digit = toint(substring("19750404", i, 1))
| summarize shift_values = make_list(digit));
let shift_char = (['char']: string, shift: int) {
    let alphabet_lower = "abcdefghijklmnopqrstuvwxyz";
    let alphabet_upper = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    let index_lower = indexof(alphabet_lower, ['char']);
    let index_upper = indexof(alphabet_upper, ['char']);
    let new_char = iif(index_lower >= 0, substring(alphabet_lower, (index_lower + shift) % 26, 1),
                       iif(index_upper >= 0, substring(alphabet_upper, (index_upper + shift) % 26, 1), ['char']));
    new_char
};
let decodeCaesarCipher = (encoded_message: string, shift_values: dynamic) {
    let alphabet_lower = "abcdefghijklmnopqrstuvwxyz";
    let alphabet_upper = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    let decoded_message = range i from 0 to strlen(encoded_message) - 1 step 1
    | extend ['char'] = substring(encoded_message, i, 1)
    | extend shift = shift_values[i % array_length(shift_values)]
    | extend index_lower = indexof(alphabet_lower, ['char'])
    | extend index_upper = indexof(alphabet_upper, ['char'])
    | extend new_char = iif(index_lower >= 0, substring(alphabet_lower, (index_lower - shift + 26) % 26, 1),
                            iif(index_upper >= 0, substring(alphabet_upper, (index_upper - shift + 26) % 26, 1), ['char']))
    | summarize decoded_message = strcat_array(make_list(new_char), "");
    decoded_message
};
let decoded_message = decodeCaesarCipher(encoded_message_scalar, shift_values);
decoded_message

```