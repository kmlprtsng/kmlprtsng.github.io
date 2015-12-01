---
layout: post
title: Query String Parameters 
subtitle: For Asp.net Web Forms
---

One of the things that I always used to hate was the query string parameters in a ASP.NET page 
because you had to reference the query string code in different parts of the page and that caused 
a bit of repeated code and also made it difficult for other developers (and myself) to know which 
Query Strings the page expected but there is a better way and that is to access query string is by 
creating a property on a page.

~~~
private int? _courseId;
protected int CourseIdQs
{
        get { return (_courseId ?? (_courseId = Request.QueryString["cid"].ToIntOrDefault(-1))).Value; }
}
~~~