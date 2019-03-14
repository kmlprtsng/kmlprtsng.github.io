---
layout: post
title: Understanding ISO8601 International Date Standard
published: true
subtitle: The three musketeers
date: '2015-12-03'
---




#### What is ISO8601 again?
ISO8601 is a well established International Standard and a valid standard in all EU Countries.  

YYYY = year e.g. 2005  
MM = month e.g. 10  
DD = day e.g. 31 

**Representing date:**  
YYYY-MM-DD or YYYYMMDD (skipping hyphens is allowed)  

**Representing Week:**  
YYYY-W01 or YYYYW01 (skipping hyphens is allowed)  
or  
Day in a week: YYYY-W01-2 or YYYYW012

**Representing Time:**  
YYYY-MM-YYYY**Thh:mm:ss** or  
YYYY-MM-YYYY**Thh:mm** or  
YYYY-MM-YYYY**Thh:mm:ss.1234** (1234 are milliseconds)

You can skip the hypens. You get the gist.

ISO8601 suggests to separate the date from time with latin capital letter **T**.

**Fun fact:** seconds can be between 00 to 60 to allow for the leap second.


#### Time Zone
**What's a time zone dude?**  
Different geographical locations have different time offset to universal time so while in England it is 14:00 o'clock in summer, it is 16:30 in India. 

There are different ways to represent a time zone:

- UTC (Universal Time)
- GMT (Greenwich Mean Time)
- EST (Central European Time)
- and so on.

Out of all, UTC is the best way to handle time as it is internationally recognized whereas other time zones are not.

**How does ISO8601 represents time zone**

Well there are three ways to represent it.

1st way is to append **Z** at the end of time, which means that the date is represented in universal time and the client should then do the necessary calculation to convert the time to their time zone. e.g. 2015-08-10T12:00Z would equate to 2015-08-10T17:30 in India which is GMT + 5:30. **Z** is pronounced as Zulu (Zulu is represented as Z in radio communications).

2nd way is to calculate the time with certain offset and append that offset information at the end i.e. 2015-08-10T17:30+05:30 would mean that GMT+5:30 has already been calculated.

The third would be to not supply either the "Z" or the offset (e.g. +05:30) and it would be assumed as local time zone.

**Another fun fact:** Because of daylight saving a time might never occur in a location or occur twice e.g. brazil's daylight saving happens on midnight. So 00:00 time never happens at that day. (Courtesy of [Sakis Koltadis](https://twitter.com/sakisk))

#### References
[https://www.cl.cam.ac.uk/~mgk25/iso-time.html](https://www.cl.cam.ac.uk/~mgk25/iso-time.html)
