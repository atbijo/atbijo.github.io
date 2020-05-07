## 3.4 Transcribe with Language Model Customization

```batch
curl -X POST -u apikey:%APIKEY% --header "Content-Type: audio/flac" --data-binary @automotive.flac "%URL%/v1/recognize?language_customization_id=%AUTO_LM%" > automotive-flac-customized.json
```
