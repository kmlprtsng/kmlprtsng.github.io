---
layout: post
title: Handlebars Split Strings Helper
---

[Handlebars](http://handlebarsjs.com/) is great.

**What is Handlebars I hear you say?**

Doh!! Do you embed your HTML code in JS code. Bad….Handlebars to the rescue.

**String Splitter**

While using Handlebars I came across a scenario where I had to split a string using a delimiter and then push the contents into the DOM individually.

**Show me Code**

~~~
Handlebars.registerHelper("splitString", function(context, options){
    if(context){
      var ret = "";
      
      var tempArr = context.trim().split(options.hash["delimiter"]);

      for(var i=0; i < tempArr.length; i++)
      {
        ret = ret + options.fn(tempArr[i]);
      }

      return ret;
    }
  });
~~~

**Usage**

~~~
<div></div>
<script id="template" type="text/x-handlebars">
     <ul>
     {{#splitString sillyString delimiter=" "}} 
       <li>{{this}}</li>
     {{/splitString}}
     </ul>
</script>

<script type="text/javascript">
      var context = {sillyString: "big gray box"};
  
      var templ = Handlebars.compile($("#template").html());
      var html = templ(context);
       $("div").html(html);
</script>
~~~

**Results**
~~~
<ul>
       <li>big</li>
       <li>gray</li>
       <li>box</li>
 </ul>
~~~
