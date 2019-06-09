## jquery对象和DOM对象的互相转换

1. jq转换为dom对象:

   ```js
   var domObj = $("#div")[0];
   ```

   

2. dom转换为jq对象:

   ```js
    var domObj = document.getElementById("div");
    var $obj = $(domObj);
   ```

   

