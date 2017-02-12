# Core
<a href="//github.com/sheetsu/docs/tree/master/source/includes/_core.md" target="_blank" class="gh-button"><i class="fa fa-github"></i> Edit on GitHub</a>

# READ
## Read all data

```shell
# Read whole spreadsheet
curl "https://sheetsu.com/apis/v1.0/020b2c0f"
```

```shell
# Read first two rows from sheet "Sheet2"
curl "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2?limit=2"
```

```ruby
require 'sheetsu'
sheetsu = Sheetsu::Client.new("020b2c0f")
```

```ruby
# Read whole spreadsheet
sheetsu.read
```

```ruby
# Read first two rows from sheet "Sheet2"
sheetsu.read(sheet: "Sheet2", limit: 2)
```

```html
<!-- Read whole spreadsheet -->
<div sheetsu="https://sheetsu.com/apis/v1.0/020b2c0f">
  <p>Name: {{name}}</p>
  <p>Score: {{score}}</p>
</div>

<script src="//load.sheetsu.com?i=d0c5"></script>
```

```html
<!-- Read first two rows from sheet "Sheet2" -->
<div sheetsu="https://sheetsu.com/apis/v1.0/020b2c0f" sheetsu-limit="2" sheetsu-sheet="Sheet2">
  <p>Name: {{name}}</p>
  <p>Score: {{score}}</p>
</div>

<script src="//load.sheetsu.com?i=d0c5"></script>
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
curl "https://sheetsu.com/apis/v1.0/020b2c0f/search?id=foo&foo=bar"
```

```shell
# Get all rows where column 'First name' is 'Peter'
# and column 'Score' is '42'
curl "https://sheetsu.com/apis/v1.0/020b2c0f/search?First%20name=Peter&Score=42"
```

```shell
# Get first two rows where column 'First name' is 'Peter',
# column 'Score' is '42' from sheet "Sheet2"
curl "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2/search?First%20name=Peter&Score=42&limit=2"
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

```html
<!-- Get all records where score is 42 -->
<div sheetsu="https://sheetsu.com/apis/v1.0/020b2c0f" sheetsu-search='{"score": "42"}'>
  <p>Name: {{name}}, score: {{score}}</p>
</div>

<script src="//load.sheetsu.com?i=d0c5"></script>
```

```html
<!--
  Get all records where score is 42
  from sheet "Sheet2"
-->
<div sheetsu="https://sheetsu.com/apis/v1.0/020b2c0f" sheetsu-search='{"score": "42"}' sheetsu-sheet="Sheet2">
  <p>Name: {{name}}, score: {{score}}</p>
</div>

<script src="//load.sheetsu.com?i=d0c5"></script>
```

Search Google Spreadsheet for particular records. Pass params in a `column_name=value` as params to the `GET https://sheetsu.com/apis/v1.0/{id}/search` request.

### Request Parameters
You can optionally limit results, or start with offset.

Parameter | Description
----------|------------
limit | Number of how many rows should be returned
offset | Number from which row response should start (default is 0)


### Returns
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

```html
<!--
  Display form, which will
  save record to the Google Spreadsheet
-->
<form sheetsu="https://sheetsu.com/apis/v1.0/1c3c0ff33">
  <input type="text" name="full_name">
  <input type="text" name="email">
  <textarea name="message"></textarea>

  <input type="submit">
</form>

<script src="//load.sheetsu.com?i=d0c5"></script>
```

```html
<!--
  Display form, which will
  save record to the Google Spreadsheet
  to sheet "Sheet2"
-->
<form sheetsu="https://sheetsu.com/apis/v1.0/1c3c0ff33" sheetsu-sheet="Sheet2">
  <input type="text" name="full_name">
  <input type="text" name="email">
  <textarea name="message"></textarea>

  <input type="submit">
</form>

<script src="//load.sheetsu.com?i=d0c5"></script>
```

Add a row to Google Spreadsheet by sending a JSON object via `POST` request. 

### Multiple rows
Send an array of objects wrapped in `{ "rows": YOUR_ARRAY_HERE }` JSON to add multiple rows in one request.

### Returns
An array of created objects.

# UPDATE
```shell
# Update all rows where value of column name is Peter
# Update only score colum
curl "https://sheetsu.com/apis/v1.0/020b2c0f/name/Peter" \
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
curl "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2/foo/bar" \
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
curl "https://sheetsu.com/apis/v1.0/020b2c0f/name/Lois" \
-X DELETE
```

```shell
# Delete all rows from sheet "Sheet2"
# where value of column foo is bar
curl "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2/foo/bar" \
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
