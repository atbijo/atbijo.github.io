## 4.3 Transcribe without Grammar

```batch
curl -X POST -u apikey:%APIKEY% --header "Content-Type: audio/flac" --data-binary @claim-number.flac "%URL%/v1/recognize" > claim-number.json
```
