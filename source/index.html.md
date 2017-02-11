---
title: Sheetsu Documentation

language_tabs:
  - shell: cURL
  - ruby: Ruby

toc_footers:
  - <a href="https://sheetsu.com/your-apis">Your APIs</a>
  - <a href="https://sheetsu.com/pricing">Pricing</a>
  - <a href="https://sheetsu.com/get-month-free">Refer a friend!</a>

search: true
---

# Introduction

# Welcome

The Sheetsu API is meant to provide a RESTful way to interact with a Google Spreadsheets. Our API uses HTTP response codes to indicate API errors. We use built-in HTTP features, like HTTP Basic authentication and HTTP verbs, which are understood by off-the-shelf HTTP clients. We support cross-origin resource sharing, allowing you to interact securely with our API from a client-side web application. JSON is returned by all API responses, including errors, although our API libraries convert responses to appropriate language-specific objects.

The requests in the right sidebar are designed to work as is. The sample requests are performed using our test API and test spreadsheet, which you can find here.

If you are looking for quick start guides and tutorials, head over to the Guides and tutorials section.

# SDKs & Client libraries
Official libraries for the Sheetsu API are available in Ruby and JavaScript.

* Node: [https://github.com/sheetsu/sheetsu-node](https://github.com/sheetsu/sheetsu-node)
* Ruby: [https://github.com/sheetsu/sheetsu-ruby](https://github.com/sheetsu/sheetsu-ruby)

API Endpoint
https://sheetsu.com/apis/v1.0

# Core

# READ
## Read all data

```shell
curl "https://sheetsu.com/apis/v1.0/020b2c0f"
```

```ruby
require 'sheetsu'

sheetsu = Sheetsu::Client.new("020b2c0f")
sheetsu.read
```

> The above command returns an array structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

API can return whole Google Spreadsheet via a `GET` method to `https://sheetsu.com/apis/v1.0/{id}`.

### Request Parameters
You can optionally limit results, or start with offset.

Parameter | Description
----------|------------
limit | Number of how many rows should be returned
offset | Number from which row response should start (default is 0)

### Returns
An array of objects. Each object is a row from the Google Spreadsheet.

## Search spreadsheet
```shell
# Get all rows where column 'id' is 'foo'
# and column 'value' is 'bar'
curl "https://sheetsu.com/apis/v1.0/020b2c0f?id=foo&foo=bar"
```

```shell
# Get all rows where column 'First name' is 'Peter'
# and column 'Score' is '42'
curl "https://sheetsu.com/apis/v1.0/020b2c0f?First%20name=Peter&Score=42"
```

```shell
# Get first two rows where column 'First name' is 'Peter',
# column 'Score' is '42' from sheet "Sheet2"
curl "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2?First%20name=Peter&Score=42&limit=2"
```

```ruby
require 'sheetsu'
sheetsu = Sheetsu::Client.new("020b2c0f")
```

```ruby
# Get all rows where column 'id' is 'foo'
# and column 'value' is 'bar'
sheetsu.read(search: { id: "foo", value: "bar" })
```

```ruby
# Get all rows where column 'First name' is 'Peter'
# and column 'Score' is '42'
sheetsu.read(search: { "First name" => "Peter", "Score" => 42 })
```

```ruby
# Get first two rows where column 'First name' is 'Peter',
# column 'Score' is '42' from sheet "Sheet2"
sheetsu.read(
  # search criteria
  search: { "First name" => "Peter", "Score" => 42 }
  limit: 2        # first two rows
  sheet: "Sheet2" # Sheet name
)
```

Search Google Spreadsheet for particular records. Pass params in a `column_name=value` as params to the `GET https://sheetsu.com/apis/v1.0/{id}/search` request.

### Request Parameters
You can optionally limit results, or start with offset.

Parameter | Description
----------|------------
limit | Number of how many rows should be returned
offset | Number from which row response should start (default is 0)


Returns
An array of objects. Each object is a row from the Google Spreadsheet.

# CREATE
```shell
# Adds one row to spreadsheet
curl "https://sheetsu.com/apis/v1.0/020b2c0f" \
-X POST \
-H "Content-Type: application/json" \
-d '{ "id": "6", "name": "Glenn", "score": "69" }'
```

```shell
# Add multiple rows in one request
curl "https://sheetsu.com/apis/v1.0/020b2c0f" \
-X POST \
-H "Content-Type: application/json" \
-d '
{
  "rows": [
    { "id": "6", "name": "Glenn", "score": "69" },
    { "id": "7", "name": "Joe", "score": "98" }
  ]
}'
```

```shell
# Adds single row to sheet "Sheet2"
curl "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2" \
-X POST \
-H "Content-Type: application/json" \
-d '{ "foo": "bar", "baz": "quux" } }'
```

```ruby
require 'sheetsu'
sheetsu = Sheetsu::Client.new("020b2c0f")
```

```ruby
# Adds single row to spreadsheet
client.create({ id: 7, name: "Glenn", score: "69" })
```

```ruby
# Adds bunch of rows to spreadsheet
rows = [
  { id: 7, name: "Glenn", score: "69" },
  { id: 8, name: "Brian", score: "77" },
  { id: 9, name: "Joe", score: "45" }
]

client.create(rows)
```

```ruby
# Adds single row to sheet named "Sheet2"
client.create({ "foo" => "bar", "baz" => "quux" }, "Sheet2")
```

Add a row to Google Spreadsheet by sending a JSON object via `POST` request. To add multiple rows in one request, send an array of objects wrapped in `{ "rows": YOUR_ARRAY_HERE }` JSON.

### Returns
An array of created objects.

# UPDATE
```shell
# Update all rows where value of column name is Peter
# Update only score colum
curl "https://sheetsu.com/apis/v1.0/020b2c0f/name/Peter"
-X PATCH \
-H "Content-Type: application/json" \
-d '{ "score": "1337" }'
```

```shell
# Update all rows where value of column name is Lois
# Update whole row
curl "https://sheetsu.com/apis/v1.0/020b2c0f/name/Lois" \
-X PUT \
-H "Content-Type: application/json" \
-d '{ "id": "2", "name": "Loo1z", "score": "99999" }'
```

```shell
# Update all rows from sheet "Sheet2"
# where value of column foo is bar
# Update only baz colum
curl "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2/foo/bar"
-X PATCH \
-H "Content-Type: application/json" \
-d '{ "baz": "quux" }'
```

```ruby
require 'sheetsu'
sheetsu = Sheetsu::Client.new("020b2c0f")
```

```ruby
# Update all rows where value of column name is Peter
# Update only score column
client.update(
  "name",          # column name
  "Peter",         # value to search for
  { score: 1337 }, # hash with updates
)
```

```ruby
# Update all rows where value of column name is Lois
# Update whole row
client.update(
  "name", # column name
  "Lois", # value to search for
   # hash with updates
  { "id": 2, "name" => "Loo1z", "score": 99999 },
  true # nullify all fields not passed in the hash above
)
```

```ruby
# Update all rows from sheet "Sheet2"
# where value of column foo is bar
# Update only baz colum
# Empty all cells which are not 'score' or 'last name'
# (in other words, send PUT)
client.update(
  "foo", # column name
  "bar", # value to search for
  # hash with updates
  { "baz" => "quux" },
  false, # update only passed columns
  "Sheet2"
)
```

Send `PATCH` (or `PUT`) request to update value(s) of a row(s). To identify the row(s) you want to update you need to add `/{column_name}/{value}` to the API URL. Then you need to pass JSON object with new values. Updates only rows where `{column_name}` match `{value}`.

### Difference between `PUT` and `PATCH`
* `PUT` request updates whole row. If you do not provide all fields in the JSON object, some fields might get emptied. `PUT` returns whole updated row(s).
* `PATCH` request updates only values passed in JSON. Returns only updated fields.

### Returns
An array of updated objects. If a request is sent via `PATCH` method returns only updated values. If a request is sent via `PUT` method returns only updated values.

# DELETE
```shell
# Deletes all rows where name is Lois
curl "https://sheetsu.com/apis/v1.0/020b2c0f/name/Lois"
-X DELETE
```

```shell
# Delete all rows from sheet "Sheet2"
# where value of column foo is bar
curl "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2/foo/bar"
-X DELETE
```

```ruby
require 'sheetsu'
sheetsu = Sheetsu::Client.new("020b2c0f")
```

```ruby
# Delete all rows where value of column name is Lois
sheetsu.delete(
  "name", # column name
  "Lois", # value to search for
)
```

```ruby
# Delete rows from sheet "Sheet2"
# where value of column foo is bar
sheetsu.delete(
  "foo",   # column name
  "bar",   # value to search for
  "Sheet2" # sheet name
)
```

Send DELETE request with a `/{column_name}/{value}` path added at the end of the URL to delete row(s). Deletes row(s) where `{column_name}` match `{value}`.

### Returns
On success, returns `204 No Content` HTTP status code, without a body.

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
