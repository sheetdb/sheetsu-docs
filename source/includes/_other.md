# Other
<a href="//github.com/sheetsu/docs/tree/master/source/includes/_other.md" target="_blank" class="gh-button"><i class="fa fa-github"></i> Edit on GitHub</a>

# Multiple sheets
```shell
# Get whole spreadsheet from sheet named Sheet2
curl "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2"
```

```shell
# Adds single row to sheet named "Sheet2"
curl "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2" \
-X POST \
-H "Content-Type: application/json" \
-d '{ "foo": "6", "another column": "quux" }'
```

```ruby
require 'sheetsu'
sheetsu = Sheetsu::Client.new("020b2c0f")
```

```ruby
# Get whole spreadsheet from sheet named Sheet2
sheetsu.read(sheet: "Sheet2")
```

```ruby
# Adds single row to sheet named "Sheet2"
sheetsu.create({ "foo" => "bar", "another column" => "quux" }, "Sheet2")
```

By default, always the first sheet (aka worksheet aka tab) is accessed. To access other sheets within a spreadsheet add `/sheets/{sheet_name}` path to the URL if using cURL, or pass appropriate param when using a lib.

# Authentication
```shell
curl "https://sheetsu.com/apis/v1.0/020b2c0f" \
-u 'your_api_key:your_api_secret'
```

```ruby
# Create new client object with HTTP Basic Auth keys
sheetsu = Sheetsu::Client.new(
  "020b2c0f",
  api_key: "YOUR_API_KEY",
  api_secret: "YOUR_API_SECRET"
)
```

You can secure your API with HTTP Basic authentication. It can be turned on in the API settings.

You have to send `api_key` and `api_secret` when you have authentication turned on.

# Creating API programmatically

```shell
# Creates new API
curl "https://sheetsu.com/apis/v1.0/api_sheets" \
-X POST \
-H "Content-Type: application/json" \
-d '{ "email": "your@email.com", "api_key": "api_key", "google_spreadsheet_url": "your_doc_url" }'
```

API can be created by sending `POST` request to `https://sheetsu.com/apis/v1.0/api_sheets`. This feature is not available in all plans - check [pricing page](https://sheetsu.com/pricing) to know more.
Please contact
<a href="#creating-api-programmatically" onclick='Intercom("showNewMessage", "Hello there! 👋 I need my api_key so I could create my API programmatically")'>support</a>
 to get your `api_key`.

# Rate Limits
Every API has a rate limit. You can check rate limitś for APIs on the [pricing page](https://sheetsu.com/pricing). After hitting the limit for the particular API, you receive `429 Rate limit exceeded` status code.

# HTTP Status Codes
Every response from the API is a JSON encoded string with a significant HTTP status code.

Code | Description
-----|------------
`200 OK` | Standard response for successful GET, PUT and PATCH requests
`201 Created` | Successful response for POST requests
`204 No Content` | Successful response for DELETE requests
`400 Bad Request` | Error response when creating (`POST`) or updating (`PUT`, `PATCH`) row(s)
`401 Unauthorized` | Error response when wrong authorization credentials provided
`402 Payment Required` | Returned if pro feature ([multiple sheets](#multiple-sheets)) is tried to be accessed from free account
`403 Forbidden` | Error response when action is forbidden by the user (API owner)
`404 No such route` | Error response when route doesn't exist
`429 Rate limit exceeded` | Error response when API hits quota exceeded
`500 Server error` |

Each API URL has an `id`, which identifies it. It is part of the URL which is after `https://sheetsu.com/apis/v1.0/`.
