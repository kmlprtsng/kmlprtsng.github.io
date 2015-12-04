---
layout: post
subtitle: null
date: "2015-12-04"
published: true
title: ISO8601 ServiceStack and Browsers
---

Carrying on from my previous [Understanding ISO8601 International Date Standard](http://kamalpreetsingh.com/2015-12-03-understanding-iso8601-date-standard/) Post.

#### What's the deal?
Well you will see that in a minute. Different settings in ServiceStack will result in different date output being returned, specially when you are interested in ISO8601 format. 

> This whole post assumes that we are dealing with DateTime in England where it is GMT + 01:00 in summer and GMT+00:00 in winter.

#### Settings in ServiceStack
```
JsConfig.DateHandler = DateHandler.ISO8601;
JsConfig.AssumeUtc = false;
```

The above setting will take dates that are being returned back by the ServiceStack service into ISO8601. But there is a catch. Say for example if you are getting your dates out of EF, they will have the `DateTimeKind` set to `DateTimeKind.Unspecified` by default so what do you think ServiceStack would return if the date was 2015-06-09?

1. `2015-06-09T00:00:00.0000000Z` (with Zulu)
2. `2015-06-09T00:00:00.0000000`
3. `2015-06-09T00:00:00.0000000+01:00` (with date already having calculated the offset)

Well the correct answer is 2. Why? Because ServiceStack doesn't know what the DateTimeKind is so it doesn't send that information back to the consuming client (which we will assume is a chrom browser for this post).

> Browser does not talk ServiceStack

So now the browser has the date as `2015-06-09T00:00:00.0000000` so when you do `new Date("2015-06-09T00:00:00.0000000")` it goes on the assumption that the DateTime is UTC and turns that date into `Tue Jun 09 2015 01:00:00 GMT+0100 (GMT Daylight Time)`. So it adds another hour to accommodate the offset to make it into a UTC date.

**Surprise Surprise**: if the date was a winter date e.g. `2015-11-04T00:00:00.0000000` and you did `new Date("2015-11-04T00:00:00.0000000")` in the browser, the browser would then keep the date as is i.e. `Wed Nov 04 2015 00:00:00 GMT+0000 (GMT Standard Time)` because there is no offset to be added.

**How about we just add `JsConfig.AssumeUtc = true;`**  
Well we could do that but you have to be aware of how the browser would handle it. You see with the AssumeUtc flag turned on ServiceStack would return the following: `2015-06-09T00:00:00.0000000Z` output. So in our browser when we do `new Date("2015-06-09T00:00:00.0000000Z")` what we get back is `Tue Jun 09 2015 01:00:00 GMT+0100 (GMT Daylight Time)`, which again results in an added hour in the browser to convert the date to local date.

#### Is there anything else we can do?
The problem is really that the browser is assuming that the date time without a given TimeZone (i.e. `2015-06-09T00:00:00.0000000`) is UTC and hence it is appending another hour onto it. It should really assume that the date is in local time zone and not do what it is currently doing but hey, they are making that assumption so we have to deal with it.

There are couple of solutions though:

1. In the browser apply the [following solution](http://stackoverflow.com/a/15568516). Decorating the date with UTC timezone (e.g. `DateTime.SpecifyKind(waitingListEntry.DateAddedToList, DateTimeKind.Utc);`) will not have any impact on the browser's behavior as discussed earlier.
2. Apply the following code which would return the date with the offset applied and also return the offset that was applied e.g. `2015-06-09T00:00:00.0000000+01:00`. This might again cause problems if dealing with territories with different times. 

{% highlight C#%}
JsConfig<DateTime>.SerializeFn = time => new DateTime(time.Ticks, DateTimeKind.Local).ToString("o");

JsConfig<DateTime?>.SerializeFn = time => time != null ? new DateTime(time.Value.Ticks, DateTimeKind.Local).ToString("o") : null;
{% endhighlight%}