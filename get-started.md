---
title: Get started
layout: get started
---

Quick start.

Universal API facilitates swift integration of third-party services into your website with ease. This guide walks you through the step-by-step process to set it up on your HTML page, initialize the required script, and make authenticated calls to the Universal API.

## Step 1: Add Script Link
Insert the following script link at the end of the body tag in your HTML page. This link references the required JavaScript file for the Universal API.

```html
<script src="./public/js/index.js"></script>
```

## Step 2: Initialize the Script
Upon page load, initialize the script using the following snippet. This snippet also demonstrates how to set up a callback function to handle the token received from the Universal API, which is essential for authenticated communication with third-party services.

```javascript
$(document).ready(function(){
    var onTokenReceived = function(token) {
        localStorage['uapi_token'] = token; // Save Universal API token
    }

    var plugin = new window.WidgetPlugin({ onTokenReceived: onTokenReceived });

    plugin.init();
});
```

## Step 3: Add Button to HTML
Add a button to your HTML which will trigger the Universal API widget when clicked.

```html
<a id="open-widget" href="#" class="btn btn-primary">Open widget</a>
```

## Step 4: Add Button Handler
Implement a click event handler for the button to show the Universal API widget as shown below.

```javascript
var btn = $('#open-widget');

btn.click(function(e){
    e.preventDefault();
    plugin.showWidget();
});
```

## Step 5: Make a call Universal API
Once authenticated, you can make calls to the Universal API to manage your third-party services. Utilize the token saved earlier to authorize your requests.

The example below demonstrates the creation of product assets in a third-party platform where the user has been authenticated.

```javascript

var title = $('#title').val();
var description = $('#description').val();
var imageUrl = $('#image-url').val();

var data = {
    title: title,
    description: description,
    imageUrl: imageUrl
};

var uapiToken = localStorage['uapi_token'];
$.ajax(
    {
        url: `https://localhost:7250/api/v1/products`,
        data: JSON.stringify(data),
        method: 'POST',
        contentType: "application/json; charset=utf-8",
        dataType: "json",
        headers: {
            'UNIVERSAL-API-ACCESS-TOKEN': uapiToken
        },
        success: function (data, status){
            alert(`Saved ${data.title} successfully`);
        }
    }
);
```

That's it! You have now successfully set up and utilized the Universal API on your website.