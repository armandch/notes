- Put the following script in
`~/Library/Containers/BBEdit/Data/Library/Application Support/BBEdit/Text Filters/FormatJSON.sh` (on MacOS 11 Big Sur, or above).

- For MacOS 10.15 Catalina and below, use this location: `~/Library/Application Support/BBEdit/Text Filters/FormatJSON.sh`.

- `FormatJSON.sh`:
```
#!/bin/bash
python -m json.tool
```

- Open a JSON file in BBEdit. There is no need to restart BBEdit because BBEdit rocks!
Select `Text` > `Apply Text Filter` > `FormatJSON`.