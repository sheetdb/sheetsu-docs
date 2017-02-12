# Snippet
<a href="//github.com/sheetsu/docs/tree/master/source/includes/_snippet.md" target="_blank" class="gh-button"><i class="fa fa-github"></i> Edit on GitHub</a>

The snippet is our "we are here for you" for all those, who don't want to play with any programming languages or development but want to have all the Sheetsu super powers on their websites.

Snippet allows you to interact with a Google Spreadsheet from your website with just HTML.

# Installation
Add below code before closing `</body>` tag.

`<script src="//load.sheetsu.com?i=d0c5"></script>`

# Read data from Spreadsheet
```xml
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

```xml
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
```xml
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
