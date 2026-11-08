# Data format

The three datasets published on 7 November 2026 share one layout.

## JSON

One file per dataset under `data/`, with top-level keys `name`, `title`, `description`, `as_of`, `license`, `source`, `languages` and `blocks`. Each block has:

| Key | Type | Notes |
|---|---|---|
| `id` | string | Stable key, also used for CSV file names |
| `kind` | `table` or `list` | Decides whether `rows` or `items` is present |
| `title` | object | `en`, `ru`, `uk` |
| `url` | object | Source page per language |
| `header`, `rows` | object of arrays | Tables only, per language |
| `items` | object of arrays | Lists only, per language |

## CSV

`data/csv/<lang>/<block-id>.csv`, one file per block and language, UTF-8, header in the first line, with a `source_url` column on every row.

## Loading example

```python
import json, urllib.request

url = ("https://raw.githubusercontent.com/ctmakc/company-structure-tax-tables/"
       "main/data/company-structure-tax-tables.json")
data = json.load(urllib.request.urlopen(url))
for block in data["blocks"]:
    print(block["id"], "-", block["title"]["en"])
```

The compliance calendar is older and simpler: one CSV and one JSON file with the columns listed on its page.
