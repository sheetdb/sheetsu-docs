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

```javascript--node
var sheetsu = require('sheetsu-node')
// import sheetsu from 'sheetsu-node' for ES6
var client = sheetsu({ address: '020b2c0f' })
```

```javascript--node
// Read whole spreadsheet
client.read().then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```javascript--node
// Read first two rows from sheet "Sheet2"
client.read({ limit: 2, sheet: "Sheet2" }).then(function(data) {
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

```php
<?php

require('vendor/autoload.php');
use Sheetsu\Sheetsu;

$sheetsu = new Sheetsu([
    'sheetId' => '020b2c0f'
]);


// Read whole spreadsheet
$response = $sheetsu->read();
$collection = $response->getCollection();


// Read first two rows from sheet "Sheet2"
$response = $sheetsu->sheet('Sheet2')->read(2, 0);
$collection = $response->getCollection();

?>
```

```javascript--jquery
function successFunc(data) {
  console.log(data);
}

// Read whole spreadsheet
var url = "https://sheetsu.com/apis/v1.0/020b2c0f";
$.ajax({ url: url, success: successFunc });


// Read first two rows from sheet "Sheet2"
var url = "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2";
var params = { "limit": 2 };
$.ajax({ url: url, data: params, success: successFunc });

```

```csharp
using System;
using System.Net;
using System.IO;

namespace Sheetsu
{
    public class Example
    {
        public static void Main(string[] args)
        {
            string sheetsuResponse = string.Empty;
            string apiUrl = @"https://sheetsu.com/apis/v1.0/020b2c0f";

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(apiUrl);
            HttpWebResponse response = (HttpWebResponse)request.GetResponse();

            Stream stream = response.GetResponseStream();
            StreamReader reader = new StreamReader(stream);
            sheetsuResponse = reader.ReadToEnd();
        }
    }
}
```

```swift
import Foundation

// Read whole spreadsheet
let url = String(format: "https://sheetsu.com/apis/v1.0/020b2c0f")
let serviceUrl = URL(string: url)
var request = URLRequest(url: serviceUrl!)

request.httpMethod = "GET"
request.setValue("Application/json", forHTTPHeaderField: "Content-Type")

let session = URLSession.shared

session.dataTask(with: request) { (data, response, error) in
  if let data = data {
    do {
      let json = try JSONSerialization.jsonObject(with: data, options: [])
      print(json)
    } catch {
      print(error)
    }
  }
}.resume()
```

```r
library(httr)

# Read whole spreadsheet
response <- GET("https://sheetsu.com/apis/v1.0/020b2c0f")
data <- content(response, "parsed")


# Read first two rows from sheet "Sheet2"
query = list(limit = 2)
response <- GET(
  "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2",
  query = query
)
data <- content(response, "parsed")
```

```jsx
// Read whole spreadsheet
class SheetsuRead extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      data: [],
    };
  }

  componentDidMount() {
    fetch("https://sheetsu.com/apis/v1.0/020b2c0f")
      .then( (response) => {
        return response.json()
      }).then( (json) => {
        this.setState({data: json});
      });
  }

  renderData() {
    return this.state.data.map((row) =>
     <div key={row.id}>{row.name} {row.score}</div>
    );
  }

  render() {
    return (
      <div>
        {this.renderData()}
      </div>
    );
  }
}


// Read first two rows from sheet "Sheet1"
class SheetsuRead extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      data: [],
    };
  }

  componentDidMount() {
    fetch("https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet1?limit=2")
      .then( (response) => {
        return response.json()
      }).then( (json) => {
        this.setState({data: json});
      });
  }

  renderData() {
    return this.state.data.map((row) =>
     <div key={row.id}>{row.name} {row.score}</div>
    );
  }

  render() {
    return (
      <div>
        {this.renderData()}
      </div>
    );
  }
}

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

```javascript--node
var sheetsu = require('sheetsu-node')
// import sheetsu from 'sheetsu-node' for ES6
var client = sheetsu({ address: '020b2c0f' })
```

```javascript--node
// Get all rows where column 'score' is '42'
client.read({ search: { score: 42 } }).then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```javascript--node
// Get all rows where column 'score' is '42'
// and column 'name' is 'Peter'
client.read({ search: { score: 42, name: "Peter" } }).then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```javascript--node
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

```php
<?php

require('vendor/autoload.php');
use Sheetsu\Sheetsu;

$sheetsu = new Sheetsu([
    'sheetId' => '020b2c0f'
]);


// Get all rows where column 'score' is '42'
$response = $sheetsu->search([
    'score' => '42'
]);
$collection = $response->getCollection();


// Get all rows where column 'score' is '42'
// and column 'name' is 'Peter'
$response = $sheetsu->search([
    'name' => 'Peter',
    'score'      => '42'
]);
$collection = $response->getCollection();


// Get first two rows where column 'foo' is 'bar'
// from sheet "Sheet2"
$response = $sheetsu->sheet('Sheet2')->search([
    'foo' => 'bar',
], 2, 0);
$collection = $response->getCollection();


// Get all rows where column 'name' is contains string 'oi'
$response = $sheetsu->search([
    'name' => '*oi*',
]);
$collection = $response->getCollection();

?>
```

```javascript--jquery
function successFunc(data) {
  console.log(data);
}

// Get all rows where column 'score' is '42'
var url = "https://sheetsu.com/apis/v1.0/020b2c0f/search";
var params = { "score": 42 };
$.ajax({ url: url, data: params, success: successFunc });


// Get all rows where column 'score' is '42'
// and column 'name' is 'Peter'
var url = "https://sheetsu.com/apis/v1.0/020b2c0f/search";
var params = { "score": 42, "name": "Peter" };
$.ajax({ url: url, data: params, success: successFunc });


// Get first two rows where column 'foo' is 'bar'
// from sheet "Sheet2"
var url = "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2/search";
var params = { "foo": "bar" };
$.ajax({ url: url, data: params, success: successFunc });


// Get all rows where column 'name' contains string 'oi'
var url = "https://sheetsu.com/apis/v1.0/020b2c0f/search";
var params = { "name": "*oi*" };
$.ajax({ url: url, data: params, success: successFunc });
```

```csharp
using System;
using System.Net;
using System.IO;

namespace Sheetsu
{
    public class Example
    {
        public static void Main(string[] args)
        {
            string sheetsuResponse = string.Empty;
            string apiUrl = @"https://sheetsu.com/apis/v1.0/020b2c0f/search?score=42";

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(apiUrl);
            HttpWebResponse response = (HttpWebResponse)request.GetResponse();

            Stream stream = response.GetResponseStream();
            StreamReader reader = new StreamReader(stream);
            sheetsuResponse = reader.ReadToEnd();
        }
    }
}
```

```swift
import Foundation

// Get all rows where column 'score' is '42'
let url = String(format: "https://sheetsu.com/apis/v1.0/020b2c0f/search?score=42")
let serviceUrl = URL(string: url)
var request = URLRequest(url: serviceUrl!)
request.httpMethod = "GET"
request.setValue("Application/json", forHTTPHeaderField: "Content-Type")

let session = URLSession.shared

session.dataTask(with: request) { (data, response, error) in
  if let data = data {
    do {
      let json = try JSONSerialization.jsonObject(with: data, options: [])
      print(json)
    } catch {
      print(error)
    }
  }
}.resume()
```

```r
library(httr)

# Get all rows where column 'score' is '42'
query <- list(score = 42)
response <- GET(
  "https://sheetsu.com/apis/v1.0/020b2c0f/search",
  query = query
)
data <- content(response, "parsed")


# Get all rows where column 'score' is '42'
# and column 'name' is 'Peter'
query <- list(score = 42, name = "Peter")
response <- GET(
  "https://sheetsu.com/apis/v1.0/020b2c0f/search",
  query = query
)
data <- content(response, "parsed")


# Get first two rows where column 'foo' is 'bar'
# from sheet "Sheet2"
query <- list(foo = "bar")
response <- GET(
  "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2/search",
  query = query
)
data <- content(response, "parsed")


# Get all rows where column 'name' is contains string 'oi'
query <- list(name = "*oi*")
response <- GET(
  "https://sheetsu.com/apis/v1.0/020b2c0f/search",
  query = query
)
data <- content(response, "parsed")
```

```jsx
// Get all records where score is 42
class SheetsuSearch extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      data: [],
    };
  }

  componentDidMount() {
    fetch("https://sheetsu.com/apis/v1.0/020b2c0f/search?score=42")
      .then( (response) => {
        return response.json()
      }).then( (json) => {
        this.setState({data: json});
      });
  }

  renderData() {
    return this.state.data.map((row) =>
     <div key={row.id}>{row.name} {row.score}</div>
    );
  }

  render() {
    return (
      <div>
        {this.renderData()}
      </div>
    );
  }
}


// Get all records where score is 42
// from sheet "Sheet1"
class SheetsuSearch extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      data: [],
    };
  }

  componentDidMount() {
    fetch("https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet1/search?score=42")
      .then( (response) => {
        return response.json()
      }).then( (json) => {
        this.setState({data: json});
      });
  }

  renderData() {
    return this.state.data.map((row) =>
     <div key={row.id}>{row.name} {row.score}</div>
    );
  }

  render() {
    return (
      <div>
        {this.renderData()}
      </div>
    );
  }
}
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
