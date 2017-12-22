# UPDATE
```shell
# Update all rows where value of column name is Peter
# Update only score colum
curl "https://sheetsu.com/apis/v1.0db/020b2c0f/name/Peter" \
-X PATCH \
-H "Content-Type: application/json" \
-d '{ "score": "1337" }'
```

```shell
# Update all rows where value of column name is Lois
# Update whole row
curl "https://sheetsu.com/apis/v1.0db/020b2c0f/name/Lois" \
-X PUT \
-H "Content-Type: application/json" \
-d '{ "id": "2", "name": "Loo1z", "score": "99999" }'
```

```shell
# Update all rows from sheet "Sheet2"
# where value of column foo is bar
# Update only baz colum
curl "https://sheetsu.com/apis/v1.0db/020b2c0f/sheets/Sheet2/foo/bar" \
-X PATCH \
-H "Content-Type: application/json" \
-d '{ "another column": "quux" }'
```

```ruby
require 'sheetsu'
sheetsu = Sheetsu::Client.new("https://sheetsu.com/apis/v1.0dr/020b2c0f")
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

```javascript--node
var sheetsu = require('sheetsu-node')
// import sheetsu from 'sheetsu-node' for ES6
var client = sheetsu({ address: 'https://sheetsu.com/apis/v1.0dn/020b2c0f' })
```

```javascript--node
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

```javascript--node
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

```javascript--node
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
client = SheetsuClient("https://sheetsu.com/apis/v1.0dy/020b2c0f")
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

```php
<?php

require('vendor/autoload.php');
use Sheetsu\Sheetsu;

$sheetsu = new Sheetsu([
    'sheetId' => 'https://sheetsu.com/apis/v1.0dp/020b2c0f'
]);

// Update all rows where value of column name is Peter
// Update only score column
$sheetsu->update('name', 'Peter', ['score' => '120']);


// Update all rows where value of column name is Peter
// Update whole row
$sheetsu->update('name', 'Peter', ['id' => 2, 'name' => 'Loo1z', 'score' => '99999'], true);

?>
```

```javascript--jquery
function successFunc(data) {
  console.log(data);
}

// Update all rows where value of column name is Peter
// Update only score column
var url = "https://sheetsu.com/apis/v1.0dq/020b2c0f/name/Peter";
var params = { score: 120 };
$.ajax({ type: "PATCH", url: url, data: params, success: successFunc });


// Update all rows where value of column name is Peter
// Update whole row
var url = "https://sheetsu.com/apis/v1.0dq/020b2c0f/name/Peter";
var params = { id: 2, name: 'Loo1z', score: '99999' };
$.ajax({ type: "PUT", url: url, data: params, success: successFunc });
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
            httpWebRequest.Method = "PATCH";

            StreamWriter streamWriter = new StreamWriter(httpWebRequest.GetRequestStream());
            string json = "{\"score\": \"9999\"}";

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

// Update all rows where value of column name is Peter
let url = String(format: "https://sheetsu.com/apis/v1.0ds/020b2c0f/name/Peter")
let serviceUrl = URL(string: url)

// Update only score column
let parameterDictionary = ["score": "1337"]
var request = URLRequest(url: serviceUrl!)

request.httpMethod = "PATCH"
request.setValue("Application/json", forHTTPHeaderField: "Content-Type")

let httpBody = try? JSONSerialization.data(
  withJSONObject: parameterDictionary,
  options: []
)

request.httpBody = httpBody

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
library(httr)

# Update all rows where value of column name is Peter
# Update only score column
body <- list(score = 120)
response <- PATCH(
  "https://sheetsu.com/apis/v1.0dl/020b2c0f/name/Peter",
  body = body,
  encode = "json"
)
data <- content(response, "parsed")

# Update all rows where value of column name is Peter
# Update whole row
body <- list(id = 2, name = 'Loo1z', score = '99999')
response <- PUT(
  "https://sheetsu.com/apis/v1.0dl/020b2c0f/name/Peter",
  body = body,
  encode = "json"
)
data <- content(response, "parsed")
```

Send `PATCH` (or `PUT`) request to update value(s) of a row(s). To identify the row(s) you want to update you need to add `/{column_name}/{value}` to the API URL. Then you need to pass JSON object with new values. Updates only rows where `{column_name}` match `{value}`.

### Difference between `PUT` and `PATCH`
* `PUT` request updates whole row. If you do not provide all fields in the JSON object, some fields might get emptied. `PUT` returns whole updated row(s).
* `PATCH` request updates only values passed in JSON. Returns only updated fields.

### Returns
An array of updated objects. If a request is sent via `PATCH` method returns only updated values. If a request is sent via `PUT` method returns only updated values.
