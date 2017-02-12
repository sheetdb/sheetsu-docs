# Other

# Multiple sheets
```shell
curl "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2"
```

```ruby
require 'sheetsu'

sheetsu = Sheetsu::Client.new("020b2c0f")
sheetsu.read(sheet: "Sheet2")
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

# Rate Limits
Every API has a rate limit. You can check your rate limit for your APIs here. After hitting the limit for the particular API, you receive `429 Rate limit exceeded` status code.

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
