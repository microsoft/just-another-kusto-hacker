[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAH1V207jSBB95ytq/WJba0BcBo2CInELLFp2iEJYHkZs1LErcS92t7e7neAI8e1T1TaQoJnlJaRTferUqVPVu7vQ78M4R3hAsUATWrjRuuzBtXJo3FIqqeZwO53VNhUOMwo1KDJLt7Z2d+EGHTi6bMQygZkR8xIVR9WObguVooUpwlxQjKHjmdGlj0c+2NnZ2SoIYCSWD7m0FRqCheCyg3kdpLneexmKptAi64+bCntnR4evF8KJ3p36e5Wd9vvHsBG+vxk+Hp1+u2svrFRxYhfmU/zBr+APCP7q62f4w1/C21X6tDDBMYvCaj5hA05DrQqdPvmSHelhC6/h8q3ayNRKpiAVKW+lVjZmTQji/HY0GpyPr2+/welweHM9uIA/BqNBD/4SLs0JIhSaQEPOEa64shBSbQymrmhaUWuFf2IzuctFppesqw8LjoHgr4qmyi3lZWbSgJ7atPYN0qaEaJVAkcBJAjaBRbwBdyPnuWM0n79FG3sMZ2rqq7VIXQeDCxQFAUYiAZ2ASyBPAGOubWiwEga9KAV5jdKgc2wzLxMqVoJ1qIxU3h1UNBopiv6aUxjpzmEFe+RVq1lYQJHmb+J6t7WtA6EykM4CUdMZJ6oE+1NtvQA+U8IMLnWtsmF7yiakYyNSNxFFEZ0Eke92RO548S2P49fIdz36/s/x4+9xHCTrNON3bvs9uFeG5qrwtVVvCbSivkmVyYXMasE/+qFKyDZYMUGL/9UsJDEsF9v4XHEJS+nyiXRY0k187t91Mdf8DTpdmBbx36yHkjmqQM+irFGilOkHw4MeXEibUphnqIQjH3jBUiLJ4ulZq2vL8UOyQScma0MZnZFlFEJIvdaFXqKJnLZ0qObRGrXve49xHLNpwunRYQjaQOgHI4RtT6AUcxoIZvspE2bnHaH1XLaedkl+mm3/MU7gS5tw/LamsIWDjKVqLyVk2FIvWPnANzaAyuBMPr/rdNiD06oqGk9SVJXR5E72nGfPYyMc2RaMdL6huhuBbvRpNJbarKk36gbkgU6polRYjLaA/jZlpUEjncheUwo4OpxkyNwn78VuSkPFEt9RS4H6duYvkQUXKAsK/3kCXwGleF9Q0ebuSDaHP4H/TzryK23cgbEm0b1lZbv9RMrTcrSxJxNsb2/zrrsfjgcX9H/AWMNCpJjrIkPDCwlmQvIqaaW1dO/Dvl967bvVPkJvS4elpodH0Ob9WHFGzqViioZwqRH+E6YNbM6RsOk7+lEPrvzT5eFn/vpSL1BBlRvSllBsXZbCyBW9nwQ4FhVSZxrqaCmecFJI66L1Vnvmlx6IM/R4GVo2NSdIdVnRrm0LeCJwctm/pBiblB7fiTBGNNF6ngQCCLy7z7xg7ZYxRNFMf/sBPve5DNsHAAA=)

```kql
// == The Weaver's Loom: Intertwining Obfuscated Threads ==
// Let the raw, fragmented utterances be gathered from the ether...
let RawWhispers = "Fragment~Echo1|Payload=Type:B64~Data:SnVzdA==; Fragment~Echo2|Payload=Type:TRANS~Data:znl@svr; Fragment~Echo3|Payload=Type:B64~Data:S3VzdG8=; Fragment~Echo4|Payload=Type:TRANS~Data:szckvr";
// The key to unlock the translated whispers (runic inversions)...
// CORRECTION APPLIED HERE: Matched 'aothe' to 'zl@sv' correctly
let RuneKey_Shadow = "zl@sv"; // Glyphs in their obscured form (z, l, @, s, v)
let RuneKey_Light = "aothe"; // Their true essence revealed (a, o, t, h, e)
// Prepare the loom, setting the tension...
print RawMaterial=RawWhispers
// Step 1: Isolate each whispered fragment and its encoding pattern
| extend FoundPatterns = extract_all(@"(Type:(B64|TRANS))~(Data:([^;]+))", RawMaterial)
// Step 2: Unravel the patterns onto individual threads, keeping sequence
| mv-expand with_itemindex=SequenceIndex WhisperData = FoundPatterns to typeof(dynamic)
// Step 3: Discern the nature and content of each thread
| extend EncodingType = trim(' ', tolower(tostring(WhisperData[1]))) // 'b64' or 'trans' - the magic type
| extend EncodedContent = trim(' ', substring(tostring(WhisperData[2]), 5)) // The raw, encoded data string, removing "Data:" prefix
// Step 4: Apply the appropriate transformation ritual to reveal the true word
| extend RevealedWord = case(
    EncodingType == "b64", base64_decode_tostring(EncodedContent), // Ritual of Base64 Unveiling
    EncodingType == "trans", translate(RuneKey_Shadow, RuneKey_Light, EncodedContent), // Ritual of Runic Translation (Using corrected keys)
    "---CORRUPTED---" // Placeholder for failed rituals
  )
// Step 5: Weave the revealed words back in their original order
| order by SequenceIndex asc
// Step 6: Gather the final woven phrase
| summarize WordTapestry = make_list(RevealedWord)
// Final Step: Present the completed work
| project strcat_array(WordTapestry, " ") // Behold the proverb!
```