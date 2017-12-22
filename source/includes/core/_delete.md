# DELETE

## Clear
```shell
# Clear all rows where name is Lois
curl "https://sheetsu.com/apis/v1.0db/020b2c0f/name/Lois" \
-X DELETE
```

```shell
# Clear all rows from sheet "Sheet2"
# where value of column foo is bar
curl "https://sheetsu.com/apis/v1.0db/020b2c0f/sheets/Sheet2/foo/bar" \
-X DELETE
```

```ruby
require 'sheetsu'
sheetsu = Sheetsu::Client.new("https://sheetsu.com/apis/v1.0dr/020b2c0f")
```

```ruby
# Clear all rows where value of column name is Lois
sheetsu.delete(
  "name", # column name
  "Lois", # value to search for
)
```

```ruby
# Clear rows from sheet "Sheet2"
# where value of column foo is bar
sheetsu.delete(
  "foo",   # column name
  "bar",   # value to search for
  "Sheet2" # sheet name
)
```

```javascript--node
var sheetsu = require('sheetsu-node')
// import sheetsu from 'sheetsu-node' for ES6
var client = sheetsu({ address: 'https://sheetsu.com/apis/v1.0dn/020b2c0f' })
```

```javascript--node
// Clear all rows where value of column name is Lois
client.delete(
  "name", // column name
  "Lois" // value to search for
).then(function(data) {
  console.log(data);
}, function(err){
  console.log(err);
});
```

```javascript--node
// Clear rows from sheet "Sheet2"
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
# Clear all rows where value of column name is Peter
client.delete(column="name", value="Peter")
```

```python
# Clear all rows from sheet named Sheet1
# where value of column name is Meg
client.delete(sheet="Sheet1", column="name", value="Meg")
```

```php
<?php

require('vendor/autoload.php');
use Sheetsu\Sheetsu;

$sheetsu = new Sheetsu([
    'sheetId' => '020b2c0f'
]);


// Clear all rows where value of column name is Peter
$sheetsu->delete('name', 'Peter');


// Clear all rows from sheet named Sheet1
// where value of column name is Meg
$sheetsu->sheet('Sheet1')->delete('name', 'Meg');

?>
```

```javascript--jquery
function successFunc(data) {
  console.log(data);
}

// Clear all rows where value of column name is Peter
var url = "https://sheetsu.com/apis/v1.0dq/020b2c0f/name/Peter";
$.ajax({ type: "DELETE", url: url, success: successFunc });


// Clear all rows from sheet named Sheet1
// where value of column name is Meg
var url = "https://sheetsu.com/apis/v1.0dq/020b2c0f/sheets/Sheet1/name/Meg";
$.ajax({ type: "DELETE", url: url, success: successFunc });
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
            string apiUrl = @"https://sheetsu.com/apis/v1.0dc/020b2c0f/name/Peter";
            string sheetsuResponse = string.Empty;

            HttpWebRequest httpWebRequest = (HttpWebRequest)WebRequest.Create(apiUrl);
            httpWebRequest.ContentType = "application/json";
            httpWebRequest.Method = "DELETE";

            HttpWebResponse response = (HttpWebResponse)httpWebRequest.GetResponse();
            StreamReader reader = new StreamReader(response.GetResponseStream());

            sheetsuResponse = reader.ReadToEnd();
        }
    }
}
```

```swift
import Foundation

// Clear all rows where value of column name is Peter
let url = String(format: "https://sheetsu.com/apis/v1.0ds/020b2c0f/name/Peter")
let serviceUrl = URL(string: url)
var request = URLRequest(url: serviceUrl!)

request.httpMethod = "DELETE"
request.setValue("Application/json", forHTTPHeaderField: "Content-Type")

let session = URLSession.shared

session.dataTask(with: request) { (data, response, error) in
  if let data = data {
    do {
      let json = try JSONSerialization.jsonObject(
        with: data,
        options: []
      )
      print(json)
    } catch {
      print(error)
    }
  }
}.resume()
```

```r
# Clear all rows where value of column name is Peter
response <- DELETE("https://sheetsu.com/apis/v1.0dl/020b2c0f/name/Peter")
data <- content(response, "parsed")


# Clear all rows from sheet named Sheet1
# where value of column name is Meg
response <- DELETE("https://sheetsu.com/apis/v1.0dl/020b2c0f/sheets/Sheet1/name/Meg")
data <- content(response, "parsed")
```

Send DELETE request with a `/{column_name}/{value}` path added at the end of the URL to delete row(s). Clear row(s) where `{column_name}` match `{value}`. Clear doesn't change the number of rows.

### Returns
On success, returns `204 No Content` HTTP status code, without a body.

## Destroy

```shell
# Destroy all rows where column 'name' is 'Lois'
curl "https://sheetsu.com/apis/v1.0db/020b2c0f" \
-X DELETE \
-H "Content-Type: application/json" \
-d '{ "name": "Lois" }'
```

```shell
# Destroy all rows where column 'score' is '42'
# and column 'name' is 'Peter'
curl "https://sheetsu.com/apis/v1.0db/020b2c0f" \
-X DELETE \
-H "Content-Type: application/json" \
-d '{ "score": "42", "name": "Peter" }'
```

```shell
# Destroy all rows from sheet 'Sheet2'
# where column 'score' is '42' and column 'name' is 'Peter'
curl "https://sheetsu.com/apis/v1.0db/020b2c0f/sheets/Sheet2" \
-X DELETE \
-H "Content-Type: application/json" \
-d '{ "score": "42", "name": "Peter" }'
```

```shell
# Destroy all rows where column 'name' is starting with 'p' or 'P'
curl "https://sheetsu.com/apis/v1.0db/020b2c0f" \
-X DELETE \
-H "Content-Type: application/json" \
-d '{ "name": "p*", "ignore_case": "true" }'
```

```shell
# Destroy all rows where column 'name' contains string 'oi'
curl "https://sheetsu.com/apis/v1.0db/020b2c0f" \
-X DELETE \
-H "Content-Type: application/json" \
-d '{ "name": "*oi*" }'
```

```javascript--jquery
function successFunc(data) {
  console.log(data);
}

// Destroy all rows where column 'name' is 'Lois'
var url = "https://sheetsu.com/apis/v1.0dq/020b2c0f";
var params = { name: "Lois" }
$.ajax({ type: "DELETE", url: url, data: params, success: successFunc });


// Destroy all rows where column 'score' is '42'
// and column 'name' is 'Peter'
var url = "https://sheetsu.com/apis/v1.0dq/020b2c0f";
var params = { score: 42, name: "Peter" }
$.ajax({ type: "DELETE", url: url, data: params, success: successFunc });


// Destroy all rows from sheet 'Sheet2'
// where column 'score' is '42' and column 'name' is 'Peter'
var url = "https://sheetsu.com/apis/v1.0dq/020b2c0f/sheets/Sheet2";
var params = { score: 42, name: "Peter" }
$.ajax({ type: "DELETE", url: url, data: params, success: successFunc });


// Destroy all rows where column 'name' is starting with 'p' or 'P'
var url = "https://sheetsu.com/apis/v1.0dq/020b2c0f";
var params = { name: "p*", ignore_case: true }
$.ajax({ type: "DELETE", url: url, data: params, success: successFunc });


// Destroy all rows where column 'name' contains string 'oi'
var url = "https://sheetsu.com/apis/v1.0dq/020b2c0f";
var params = { name: "*oi*" }
$.ajax({ type: "DELETE", url: url, data: params, success: successFunc });
```

```r
# Destroy all rows where column 'name' is 'Lois'
body <- list(name = "Lois")
response <- DELETE(
  "https://sheetsu.com/apis/v1.0dl/020b2c0f",
  body = body,
  encode = "json"
)
data <- content(response, "parsed")

# Destroy all rows where column 'score' is '42'
# and column 'name' is 'Peter'
body <- list(score = "42", name = "Peter")
response <- DELETE(
  "https://sheetsu.com/apis/v1.0dl/020b2c0f",
  body = body,
  encode = "json"
)
data <- content(response, "parsed")

# Destroy all rows from sheet 'Sheet2'
# where column 'score' is '42' and column 'name' is 'Peter'
body <- list(score = "42", name = "Peter")
response <- DELETE(
  "https://sheetsu.com/apis/v1.0dl/020b2c0f/sheets/Sheet2",
  body = body,
  encode = "json"
)
data <- content(response, "parsed")

# Destroy all rows where column 'name' is starting with 'p' or 'P'
body <- list(name = "p*", ignore_case = "true")
response <- DELETE(
  "https://sheetsu.com/apis/v1.0dl/020b2c0f",
  body = body,
  encode = "json"
)
data <- content(response, "parsed")

# Destroy all rows where column 'name' is starting with 'p' or 'P'
body <- list(name = "*oi*")
response <- DELETE(
  "https://sheetsu.com/apis/v1.0dl/020b2c0f",
  body = body,
  encode = "json"
)
data <- content(response, "parsed")
```

Send DELETE request to destroy all matched rows, move up below rows and decrease number of rows. Pass params in a `column_name=value` as params to the request.

### Wildcard matching

You can match rows to destroy using wildcards (`*`). Asteriks (`*`) can represent any characters or empty string.

### Request Parameters
You can optionally ignore letter case sensitivity.

Parameter | Description
----------|------------
ignore_case | Ignore letter case sensitivity. Both column names and values

### Returns
On success, returns `200 OK` HTTP status code, with all destroyed rows at body.
