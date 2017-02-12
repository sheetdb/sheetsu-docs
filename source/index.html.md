---
title: Sheetsu Documentation

language_tabs:
  - shell: cURL
  - ruby: Ruby
  - html: HTML Snippet

toc_footers:
  - <a href="https://sheetsu.com/your-apis">Your APIs</a>
  - <a href="https://sheetsu.com/pricing">Pricing</a>
  - <a href="https://sheetsu.com/get-month-free">Refer a friend!</a>

search: true
---

# Introduction

# Welcome

You can view code examples in the area on the right. You can switch the programming language with the tabs in the top right. We provide examples in cURL, Ruby and some of them with our Snippet - which is pure HTML.

<aside class="success">
For quick start guides and tutorials go to Guides and tutorials section.
</aside>

Follow [@sheetsuhq](https://twitter.com/sheetsuhq) on Twitter for latest updates and news.

# SDKs & Client libraries
Official libraries for the Sheetsu API are available in Ruby and JavaScript.

* Node: [https://github.com/sheetsu/sheetsu-node](https://github.com/sheetsu/sheetsu-node)
* Ruby: [https://github.com/sheetsu/sheetsu-ruby](https://github.com/sheetsu/sheetsu-ruby)

# How to prepare spreadsheet

Every spreadsheet should have the first row populated with column names. There are no mandatory fields or values you _need_ to have in your spreadsheet. The structure of the spreadsheet it's totally up to you. Just keep in mind, that the first row (row #1) is treated as there are column names.

Column names can be anything. Strings, numbers, symbols, emojis 🙉 , anything.

You can [check example spreadsheet here](https://docs.google.com/spreadsheets/d/1WTwXrh2ZDXmXATZlQIuapdv4ldyhJGZg7LX8GlzPdZw/edit#gid=0). It looks like this:

id | name | score
---|------|------
1 | Peter | 43
2 | Lois | 89
3 | Meg | 10
4 | Chris | 43
5 | Stewie | 72

# Google Spreadsheet URL

To properly use Sheetsu, please paste Google Spreadsheets URL. Just copy the URL from the browser address bar. There's no need for sharing the Google Spreadsheet.

### Google Chrome
![Spreadsheet URL in Google Chrome](images/chrome.png)

### Safari
![Spreadsheet URL in Safari](images/safari.png)

# About the API

The Sheetsu API is meant to provide a RESTful way to interact with a Google Spreadsheets. Our API uses HTTP response codes to indicate API errors. We use built-in HTTP features, like HTTP Basic authentication and HTTP verbs, which are understood by off-the-shelf HTTP clients.

We support cross-origin resource sharing, allowing you to interact securely with our API from a client-side web application. JSON is returned by all API responses, including errors, although our API libraries convert responses to appropriate language-specific objects.

The requests in the right sidebar are designed to work as is. The sample requests are performed using our test API and test spreadsheet, which you can find [here](https://docs.google.com/spreadsheets/d/1WTwXrh2ZDXmXATZlQIuapdv4ldyhJGZg7LX8GlzPdZw/edit#gid=0).

# Core

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

# Snippet

The snippet is our "we are here for you" for all those, who don't want to play with any programming languages or development but want to have all the Sheetsu super powers on their websites.

Snippet allows you to interact with a Google Spreadsheet from your website with just HTML.

# Installation
Add below code before closing `</body>` tag.

`<script src="//load.sheetsu.com?i=d0c5"></script>`

# Read data from Spreadsheet
```html
<!--
  This code will get 3 first rows from
  Google Spreadsheet and display them
  in a table on a website
-->
<table>
  <thead>
    <th>Id</th>
    <th>Name</th>
    <th>Score</th>
  </thead>
  <tbody sheetsu="https://sheetsu.com/apis/v1.0/020b2c0f" sheetsu-limit="3">
    <tr>
      <td>{{id}}</td>
      <td>{{name}}</td>
      <td>{{score}}</td>
    </tr>
  </tbody>
</table>

<script src="//load.sheetsu.com?i=d0c5"></script>
```

<blockquote>
  <p>Above HTML will produce this result:</p>
  <table class="snippet-example-table">
    <thead>
      <th>Id</th><th>Name</th><th>Score</th>
    </thead>
    <tbody>
      <tr><td>1</td><td>Peter</td><td>42</td></tr>
      <tr><td>2</td><td>Lois</td><td>89</td></tr>
      <tr><td>3</td><td>Meg</td><td>10</td></tr>
    </tbody>
  </table>
</blockquote>

```html
<!--
  This code will get all rows from
  Google Spreadsheet where role is parent
  and display them with picture, name, email
-->
<div sheetsu="https://sheetsu.com/apis/v1.0/44317ab1d587" sheetsu-search='{"role": "parent"}'>
  <img src="{{picture_url}}">
  <p>
    Name: {{name}}
    <br>
    Email: {{email}}
  </p>
</div>

<script src="//load.sheetsu.com?i=d0c5"></script>
```
<blockquote>
  <p>Above HTML will produce this result:</p>
  <div class="snippet-example">
    <div class="character-card">
      <div class="char-details">
        <img src="images/peter.png">
        <p>
          <strong>Name:</strong>Peter Griffin
          <br/>
          <strong>Email:</strong>peter@griffin.com
        </p>
      </div>
    </div>
    <div class="character-card">
      <img src="images/lois.png">
      <div class="char-details">
        <p>
          <strong>Name:</strong>Lois Griffin
          <br/>
          <strong>Email:</strong>lois@griffin.com
        </p>
      </div>
    </div>
  </div>
</blockquote>

1. Add `sheetsu="YOUR_API_URL"` to the parent element.
2. Add handlebars ( `{{` and `}}` ) with column name to any child element, with column name.

### Search
You can use an additional `sheetsu-search` attribute to show only results which are matching your search criteria.

The value of the `sheetsu-search` attribute should be a key-value object ([JSON](http://json.org/example.html)) with column name and value you want to use for search.

Remember to use single quote `'` around JSON and double quote `"` with JSON key, value names.

### Limit & offset

Attributes you can use to manipulate results are `sheetsu-limit` and `sheetsu-offset`.

*(We add a little bit of CSS styling to the results on the right)*

# Save data to Spreadsheet
```html
<!--
  This code will display form, which will
  save record to the Google Spreadsheet
  (check it here: )
-->
<form sheetsu="https://sheetsu.com/apis/v1.0/1c3c0ff33">
  <input type="text" name="full_name">
  <input type="text" name="email">
  <textarea name="message"></textarea>

  <input type="submit">
</form>

<script src="//load.sheetsu.com?i=d0c5"></script>
```

<blockquote>
  <p>Above HTML will produce this result:</p>
  <div class="snippet-example">
    <div class="column-50" style="margin-right: 10px;">
      <input type="text" name="full_name" placeholder="Your name">
      <input type="text" name="email" placeholder="Email address">
    </div>
    <div class="column-50">
      <textarea name="message" placeholder="Your message" rows="3" style="position: relative;"></textarea>
    </div>
    <div class="button-wrapper">
      <input class="button" type="submit" value="Send" onclick="alert('It is just an example. Copy the code above to your website to make it work ;)')">
    </div>
  </div>
</blockquote>


1. Add `sheetsu` attribute to the `<form>` element.
2. Add `<input>` (or `<textarea>`) tags, where `name` attribute is column name from a spreadsheet.

### After submit redirection
Optionally you can add `sheetsu-after-submit` attribute with the URL you want to redirect your users after they submit the form. Without this attribute, they get redirected to [`https://sheetsu.com/thank-you.html`](https://sheetsu.com/thank-you.html).

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
