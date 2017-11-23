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

```javascript--node
var sheetsu = require('sheetsu-node')
// import sheetsu from 'sheetsu-node' for ES6
var client = sheetsu({ address: '020b2c0f' })
```

```javascript--node
// Adds single row to spreadsheet
client.create({ id: 7, name: "Glenn", score: "69" }).then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```javascript--node
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

```javascript--node
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

```php
<?php

require('vendor/autoload.php');
use Sheetsu\Sheetsu;

$sheetsu = new Sheetsu([
    'sheetId' => '020b2c0f'
]);


// Adds single row to spreadsheet
$sheetsu->create([['id' => '7', 'name' => 'Glenn', 'score' => 96 ]]);


// Adds single row to spreadsheet to sheet named "Sheet2"
$sheetsu->sheet('Sheet2')->create([['id' => '8', 'name' => 'Glenn', 'score' => 96 ]]);


// Adds bunch of rows to spreadsheet
$sheetsu->create([
  [ 'id' => '7', 'name' => 'Glenn', 'score' => '69' ],
  [ 'id' => '8', 'name' => 'Brian', 'score' => '77' ],
  [ 'id' => '9', 'name' => 'Joe', 'score' => '45' ]
]);

?>
```

```javascript--jquery
function successFunc(data) {
  console.log(data);
}

// Adds single row to spreadsheet
var url = "https://sheetsu.com/apis/v1.0/020b2c0f";
var params = { id: 7, name: 'Glenn', score: 96 };
$.ajax({ type: "POST", url: url, data: params, success: successFunc });


// Adds single row to spreadsheet to sheet named "Sheet2"
var url = "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2";
var params = { id: 7, name: 'Glenn', score: 96 };
$.ajax({ type: "POST", url: url, data: params, success: successFunc });


// Adds bunch of rows to spreadsheet
var url = "https://sheetsu.com/apis/v1.0/020b2c0f";
var params = JSON.stringify({
  rows: [
    { id: 7, name: 'Glenn', score: 96 },
    { id: 8, name: 'Brian', score: 77 },
    { id: 9, name: 'Joe', score: 45 }  
  ]
});
$.ajax(
  {
    type: "POST", url: url, data: params, success: successFunc,
    contentType: 'application/json', processData: false
  }
);
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
            string apiUrl = @"https://sheetsu.com/apis/v1.0/020b2c0f";
            string sheetsuResponse = string.Empty;

            HttpWebRequest httpWebRequest = (HttpWebRequest)WebRequest.Create(apiUrl);
            httpWebRequest.ContentType = "application/json";
            httpWebRequest.Method = "POST";

            StreamWriter streamWriter = new StreamWriter(httpWebRequest.GetRequestStream());
            string json = "{\"id\":\"6\", \"name\": \"Glenn\", \"score\": \"1000\"}";

            streamWriter.Write(json);
            streamWriter.Flush();
            streamWriter.Close();

            HttpWebResponse response = (HttpWebResponse)httpWebRequest.GetResponse();
            StreamReader reader = new StreamReader(response.GetResponseStream());

            sheetsuResponse = reader.ReadToEnd();
        }
    }
}
```

```swift
import Foundation

// Adds single row to spreadsheet
let url = String(format: "https://sheetsu.com/apis/v1.0/020b2c0f")
let serviceUrl = URL(string: url)
let parameterDictionary = ["id" : "6", "name" : "Glenn", "score": "44"]
var request = URLRequest(url: serviceUrl!)

request.httpMethod = "POST"
request.setValue("Application/json", forHTTPHeaderField: "Content-Type")

let httpBody = try? JSONSerialization.data(withJSONObject: parameterDictionary, options: [])

request.httpBody = httpBody

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

# Adds single row to spreadsheet
body <- list(id = 7, name = "Glenn", score = 96)
response <- POST("https://sheetsu.com/apis/v1.0/020b2c0f", body = body, encode = "json")
data <- content(response, "parsed")

# Adds single row to spreadsheet to sheet named "Sheet2"
body <- list(id = 7, name = "Glenn", score = 96)
response <- POST(
  "https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet2",
  body = body,
  encode = "json"
)
data <- content(response, "parsed")

# Adds bunch of rows to spreadsheet
body <- list(rows = list(
  list(id = 7, name = "Glenn", score = 96),
  list(id = 7, name = "Glenn", score = 96),
  list(id = 7, name = "Glenn", score = 96))
)
response <- POST(
  "https://sheetsu.com/apis/v1.0/020b2c0f",
  body = body,
  encode = "json"
)
data <- content(response, "parsed")
```


```jsx
// Display form, which will
// save record to the Google Spreadsheet
class SheetsuCreate extends React.Component {
  constructor(props) {
    super(props);
    this.state = { data: { id: '', name: '', score: '' } };

    this.handleInputChange = this.handleInputChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleInputChange(event) {
    var updatedData = this.state.data;
    updatedData[event.target.name] = event.target.value

    this.setState({
      data: updatedData
    });
  }

  handleSubmit(event) {
  	event.preventDefault();

    fetch("https://sheetsu.com/apis/v1.0/020b2c0f", {
      headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json'
      },
      method: "POST",
      body: JSON.stringify(this.state.data)
     }).then( (response) => {
        return response.json()
      }).then( (json) => {
        console.log(json);
      });
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input
          type="text"
          name="id"
          value={this.state.data.id}
          onChange={this.handleInputChange}
        />
        <input
          type="text"
          name="name"
          value={this.state.data.name}
          onChange={this.handleInputChange}
        />
        <input
          type="text"
          name="score"
          value={this.state.data.score}
          onChange={this.handleInputChange}
        />
        <input type="submit"/>
      </form>
    );
  }
}


// Display form, which will
// save record to the Google Spreadsheet
// to sheet "Sheet1"
class SheetsuCreate extends React.Component {
  constructor(props) {
    super(props);
    this.state = { data: { id: '', name: '', score: '' } };

    this.handleInputChange = this.handleInputChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleInputChange(event) {
    var updatedData = this.state.data;
    updatedData[event.target.name] = event.target.value

    this.setState({
      data: updatedData
    });
  }

  handleSubmit(event) {
  	event.preventDefault();

    fetch("https://sheetsu.com/apis/v1.0/020b2c0f/sheets/Sheet1", {
      headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json'
      },
      method: "POST",
      body: JSON.stringify(this.state.data)
     }).then( (response) => {
        return response.json()
      }).then( (json) => {
        console.log(json);
      });
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input
          type="text"
          name="id"
          value={this.state.data.id}
          onChange={this.handleInputChange}
        />
        <input
          type="text"
          name="name"
          value={this.state.data.name}
          onChange={this.handleInputChange}
        />
        <input
          type="text"
          name="score"
          value={this.state.data.score}
          onChange={this.handleInputChange}
        />
        <input type="submit"/>
      </form>
    );
  }
}
```

Add a row to Google Spreadsheet by sending a JSON object via `POST` request.

### Multiple rows
Send an array of objects wrapped in `{ "rows": YOUR_ARRAY_HERE }` JSON to add multiple rows in one request.

### Returns
An array of created objects.
