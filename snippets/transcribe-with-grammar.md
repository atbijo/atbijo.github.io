## 4.4 Transcribe with Grammar

```batch
curl -X POST -u apikey:%APIKEY% --header "Content-Type: audio/flac" --data-binary @claim-number.flac "%URL%/v1/recognize?language_customization_id=%AUTO_LM%&grammar_name=claimnumber" > claim-number-grammar.json
```
