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

```xml
<!-- Read whole spreadsheet -->
<div sheetsu="https://sheetsu.com/apis/v1.0/020b2c0f">
  <p>Name: {{name}}</p>
  <p>Score: {{score}}</p>
</div>

<script src="//load.sheetsu.com"></script>
```

```xml
<!-- Read first two rows from sheet "Sheet1" -->
<div sheetsu="https://sheetsu.com/apis/v1.0/020b2c0f" sheetsu-limit="2" sheetsu-sheet="Sheet1">
  <p>Name: {{name}}</p>
  <p>Score: {{score}}</p>
</div>

<script src="//load.sheetsu.com"></script>
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

```javascript
var sheetsu = require('sheetsu-node')
// import sheetsu from 'sheetsu-node' for ES6
var client = sheetsu({ address: '020b2c0f' })
```

```javascript
// Read whole spreadsheet
sheetsu.read().then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```javascript
// Read first two rows from sheet "Sheet2"
sheetsu.read({ limit: 2, sheet: "Sheet2" }).then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```


```html
<head>
  <script src="//script.sheetsu.com/"></script>
</head>
<body>
  <script>
    function successFunc(data) {
      console.log(data);
    }
    Sheetsu.read("https://sheetsu.com/apis/v1.0/020b2c0f/", {}, successFunc);
  </script>
</body>
```

```python
from sheetsu import SheetsuClient
client = SheetsuClient("020b2c0f")
```

```python
# Read first two rows from sheet "Sheet2"
client.read(sheet="Sheet2", limit=2)
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
# Get all rows where column 'score' is '42'
curl "https://sheetsu.com/apis/v1.0/020b2c0f/search?score=42"
```

```shell
# Get all rows where column 'score' is '42'
# and column 'name' is 'Peter'
curl "https://sheetsu.com/apis/v1.0/020b2c0f/search?score=42&name=Peter"
```

```shell
# Get first two rows where column 'foo' is 'bar',
# column 'another column' is '1' from sheet "Sheet2"
curl "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2/search?foo=bar&another%20column=1&limit=2"
```

```shell
# Get all rows where column 'name' is starting with 'p'
curl "https://sheetsu.com/apis/v1.0/020b2c0f/search?name=p*&ignore_case=true"
```

```shell
# Get all rows where column 'name' is contains string 'oi'
curl "https://sheetsu.com/apis/v1.0/020b2c0f/search?name=*oi*"
```

```xml
<!-- Get all records where score is 42 -->
<div sheetsu="https://sheetsu.com/apis/v1.0/020b2c0f" sheetsu-search='{"score": "42"}'>
  <p>Name: {{name}}, score: {{score}}</p>
</div>

<script src="//load.sheetsu.com"></script>
```

```xml
<!--
  Get all records where score is 42
  from sheet "Sheet1"
-->
<div sheetsu="https://sheetsu.com/apis/v1.0/020b2c0f" sheetsu-search='{"score": "42"}' sheetsu-sheet="Sheet1">
  <p>Name: {{name}}, score: {{score}}</p>
</div>

<script src="//load.sheetsu.com"></script>
```

```ruby
require 'sheetsu'
sheetsu = Sheetsu::Client.new("020b2c0f")
```

```ruby
# Get all rows where column 'score' is '42'
sheetsu.read(search: { score: 42 })
```

```ruby
# Get all rows where column 'score' is '42'
# and column 'name' is 'Peter'
sheetsu.read(search: { score: 42, name: "Peter" })
```

```ruby
# Get first two rows where column 'foo' is 'bar',
# column 'another column' is '1' from sheet "Sheet2"
sheetsu.read(
  # search criteria
  search: { "foo" => "bar", "another column" => "1" },
  limit: 2,       # first two rows
  sheet: "Sheet2" # Sheet name
)
```

```javascript
var sheetsu = require('sheetsu-node')
// import sheetsu from 'sheetsu-node' for ES6
var client = sheetsu({ address: '020b2c0f' })
```

```javascript
// Get all rows where column 'score' is '42'
client.read({ search: { score: 42 } }).then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```javascript
// Get all rows where column 'score' is '42'
// and column 'name' is 'Peter'
client.read({ search: { score: 42, name: "Peter" } }).then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```javascript
// Get first two rows where column 'foo' is 'bar',
// column 'another column' is '1' from sheet "Sheet2"
client.read({
  limit: 2, // first two rows
  // search criteria
  search: { "foo": "bar", "another column": "1" },
  sheet: "Sheet2" // Sheet name
}
).then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```html
<head>
  <script src="//script.sheetsu.com/"></script>
</head>
<body>
  <script>
    function successFunc(data) {
      console.log(data);
    }
    // Get all rows where column 'score' is '42'
    var searchQuery = {
      score: 42,
    };
    Sheetsu.read("https://sheetsu.com/apis/v1.0/020b2c0f/", {
      search: searchQuery
    }, successFunc);
  </script>
</body>
```

```python
from sheetsu import SheetsuClient
client = SheetsuClient("020b2c0f")
```

```python
# Get all rows where column 'score' is '42'
client.search(score="42")
```

```python
# Get all rows where column 'score' is '42'
# and column 'name' is 'Peter'
client.search(score="42", name="Peter")
```

```python
# Get first two rows where column 'foo' is 'bar'
# from sheet "Sheet2"
client.search(sheet="Sheet2", foo="bar", limit=2)
```

```python
# Get all rows where column 'name' is contains string 'oi'
client.search(name="*oi*")
```

Search Google Spreadsheet for particular records. Pass params in a `column_name=value` as params to the `GET https://sheetsu.com/apis/v1.0/{id}/search` request.

### Wildcard searching
You can search using wildcards (`*`). Asteriks (`*`) can represent any characters or empty string.

### Request Parameters
You can optionally limit results, or start with offset.

Parameter | Description
----------|------------
limit | Number of how many rows should be returned
offset | Number from which row response should start (default is 0)
ignore_case | Ignore letter case sensitivity. Both column names and values


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
# Adds single row to sheet named "Sheet2"
curl "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2" \
-X POST \
-H "Content-Type: application/json" \
-d '{ "foo": "6", "another column": "quux" }'
```

```xml
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

<script src="//load.sheetsu.com"></script>
```

```xml
<!--
  Display form, which will
  save record to the Google Spreadsheet
  to sheet "Sheet1"
-->
<form sheetsu="https://sheetsu.com/apis/v1.0/1c3c0ff33" sheetsu-sheet="Sheet1">
  <input type="text" name="full_name">
  <input type="text" name="email">
  <textarea name="message"></textarea>

  <input type="submit">
</form>

<script src="//load.sheetsu.com"></script>
```

```ruby
require 'sheetsu'
sheetsu = Sheetsu::Client.new("020b2c0f")
```

```ruby
# Adds single row to spreadsheet
sheetsu.create({ id: 7, name: "Glenn", score: "69" })
```

```ruby
# Adds bunch of rows to spreadsheet
rows = [
  { id: 7, name: "Glenn", score: "69" },
  { id: 8, name: "Brian", score: "77" },
  { id: 9, name: "Joe", score: "45" }
]
sheetsu.create(rows)
```

```ruby
# Adds single row to sheet named "Sheet2"
sheetsu.create({ "foo" => "bar", "another column" => "quux" }, "Sheet2")
```

```javascript
var sheetsu = require('sheetsu-node')
// import sheetsu from 'sheetsu-node' for ES6
var client = sheetsu({ address: '020b2c0f' })
```

```javascript
// Adds single row to spreadsheet
client.create({ id: 7, name: "Glenn", score: "69" }).then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```javascript
// Adds bunch of rows to spreadsheet
var rows = [
  { id: 7, name: "Glenn", score: "69" },
  { id: 8, name: "Brian", score: "77" },
  { id: 9, name: "Joe", score: "45" }
]
client.create(rows).then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```javascript
// Adds single row to sheet named "Sheet2"
client.create({ "foo": "bar", "another column": "quux" }, "Sheet2").then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```html
<head>
  <script src="//script.sheetsu.com/"></script>
</head>
<body>
  <form id="myForm">
    <input type="text" name="first_name">
    <input type="text" name="score">
    <button type="submit">Save</button>
  </form>
  <script>
    document.querySelector("#myForm").addEventListener("submit", function (e) {
      e.preventDefault();
      saveData();
    });
    function saveData() {
      var first_name = document.getElementsByName("first_name")[0].value,
        score = document.getElementsByName("score")[0].value;
      var data = {
        name: first_name,
        score: score
      };
      Sheetsu.write("https://sheetsu.com/apis/v1.0/020b2c0f/", data, {}, function (result) {
        console.log(result);
      });
    }
  </script>
</body>
```

```python
from sheetsu import SheetsuClient
client = SheetsuClient("020b2c0f")
```

```python
# Adds single row to spreadsheet
client.create_one(id="7", name="Glenn", score="96")
```

```python
# Adds single row to spreadsheet to sheet named "Sheet2"
client.create_one(sheet="Sheet2", foo="quux")
```

```python
# Adds bunch of rows to spreadsheet to sheet named "Sheet1"
client.create_many(
  sheet="Sheet1",
  *[
    dict(id="8", name="Brian", score="42"),
    dict(id="9", name="Joe", score="201")
  ]
)
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
-d '{ "another column": "quux" }'
```

```ruby
require 'sheetsu'
sheetsu = Sheetsu::Client.new("020b2c0f")
```

```ruby
# Update all rows where value of column name is Peter
# Update only score column
sheetsu.update(
  "name",          # column name
  "Peter",         # value to search for
  { score: 1337 }, # hash with updates
)
```

```ruby
# Update all rows where value of column name is Lois
# Update whole row
sheetsu.update(
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
sheetsu.update(
  "foo", # column name
  "bar", # value to search for
  # hash with updates
  { "another column" => "quux" },
  false, # update only passed columns
  "Sheet2"
)
```

```javascript
var sheetsu = require('sheetsu-node')
// import sheetsu from 'sheetsu-node' for ES6
var client = sheetsu({ address: '020b2c0f' })
```

```javascript
// Update all rows where value of column name is Peter
// Update only score column
client.update(
  "name",          // column name
  "Peter",         // value to search for
  { score: 1337 } // hash with updates
).then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```javascript
// Update all rows where value of column name is Lois
// Update whole row
client.update(
  "name", // column name
  "Lois", // value to search for
   // hash with updates
  { "id": 2, "name": "Loo1z", "score": 99999 },
  true // nullify all fields not passed in the hash above
).then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```javascript
// Update all rows from sheet "Sheet2"
// where value of column foo is bar
// Update only baz colum
// Empty all cells which are not 'score' or 'last name'
// (in other words, send PUT)
client.update(
  "foo", // column name
  "bar", // value to search for
  // hash with updates
  { "another column": "quux" },
  false, // update only passed columns
  "Sheet2"
).then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```python
from sheetsu import SheetsuClient
client = SheetsuClient("020b2c0f")
```

```python
# Update all rows where value of column name is Peter
# Update only score column
client.update(column="name", value="Peter", data=dict(score=120)))
```

```python
# Update all rows where value of column name is Peter
# Update only score column
client.update(column="name", value="Peter", data=dict(score=120)))
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

```javascript
var sheetsu = require('sheetsu-node')
// import sheetsu from 'sheetsu-node' for ES6
var client = sheetsu({ address: '020b2c0f' })
```

```javascript
// Delete all rows where value of column name is Lois
client.delete(
  "name", // column name
  "Lois" // value to search for
).then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```javascript
// Delete rows from sheet "Sheet2"
// where value of column foo is bar
client.delete(
  "foo",   // column name
  "bar",   // value to search for
  "Sheet2" // sheet name
).then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```python
from sheetsu import SheetsuClient
client = SheetsuClient("020b2c0f")
```

```python
# Delete all rows where value of column name is Peter
client.delete(column="name", value="Peter")
```

```python
# Delete all rows from sheet named Sheet1
# where value of column name is Meg
client.delete(sheet="Sheet1", column="name", value="Meg")
```

Send DELETE request with a `/{column_name}/{value}` path added at the end of the URL to delete row(s). Deletes row(s) where `{column_name}` match `{value}`.

### Returns
On success, returns `204 No Content` HTTP status code, without a body.
