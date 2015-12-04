---
layout: post
subtitle: null
date: "2015-12-04"
published: true
title: ISO8601 ServiceStack and Browsers
---

Carrying on from my previous [Understanding ISO8601 International Date Standard](http://kamalpreetsingh.com/2015-12-03-understanding-iso8601-date-standard/) Post.

#### What's the deal?
Well you will see that in a minute. Different settings in ServiceStack will result in different date being returned, specially when you are interested in ISO8601 format. 

> This whole post assumes that we are dealing with DateTime in England where it is GMT + 01:00 in summer and GMT+00:00 in winter.

#### Settings in ServiceStack
`JsConfig.DateHandler = DateHandler.ISO8601;`

The above setting will take dates that are being returned back by the service into ISO8601. But there is a catch. Say for example if you are getting your dates out of EF, they will have the `DateTimeKind` set to `DateTimeKind.Unspecified` so what do you think ServiceStack would return if the date was 2015-06-09?

1. "2015-06-09T00:00:00.0000000Z"
2. "2015-06-09T00:00:00.0000000"
3. "2015-06-09T00:00:00.0000000+01:00"

Well the correct answer is 2. Why? Because ServiceStack doesn't know what the DateTimeKind is so it doesn't send that information back to the browser.

> Browser does not talk ServiceStack

So now the browser has the date as `2015-06-09T00:00:00.0000000` so when you do `new Date("2015-06-09T00:00:00.0000000")` it goes on the some assumption and turns that date into `Tue Jun 09 2015 01:00:00 GMT+0100 (GMT Daylight Time)`. So it adds another hour to accommodate the offset to make it into a UTC date.

**Fun bit**: if the date was a winter date e.g. `2015-11-04T00:00:00.0000000` and you did `new Date("2015-11-04T00:00:00.0000000")` in the browser, the browser would then keep the date as is i.e. `Wed Nov 04 2015 00:00:00 GMT+0000 (GMT Standard Time)` because there is no offset to be added.

