---
title: "Programmer's Guide to Dealing With Different Time Zones"
permalink: /2019/03/programmers-guide-to-deal-with.html
published: true
---

All programmers have to deal with times and time zones at some point. 

When your product gets wider, it gets more and more difficult to handle and synchronize time between multiple time zones. Being well-informed beforehand might save some pain in the "head" later.

I've compiled a few most important tips to take care of when dealing with time zones. The actual list is definitely much bigger. But consider this a start.

## Store Time in UTC
Storing local time in the database is okay when your product is small and deals with just one time zone. But when you start dealing multiple time zones and [DST(Daylight Saving Time)](https://en.wikipedia.org/wiki/Daylight_saving_time), it gets weirder. Now you have to convert your time to different time zones for different users and you have to maintain all upcoming DST changes. 

Storing time in UTC can save many headaches in the future. The important reason being that the UTC timezone is never affected by DST. So always remember to store time in UTC, and apply the user's timezone when retrieving it from the database.

## Store Time Zone (NOT Offset)
When you are storing time in UTC, you'll definitely need to store user's time zone too, so that you can convert it to the user's time zone before displaying it to the user. But make sure to not confuse with time zone and offset.

Time zone and offset are related but different. An offset is just a constant time (eg:+5:30 hours) which can be added or subtracted from UTC time. A time zone(eg: Asia/Kolkata), on the other hand, may or may not have an offset. The offset of a specific time zone might change depending on what the respective governments decide. A time zone also may or may not have a DST setting and can change from time to time

Conclusion: Store time zone (eg: Asia/Kolkata) and not offset (eg: +5:30), because people follow a time zone, not an offset.

## Keep your timezone database updated
All this care is useless if you forget to update your time zone database frequently. A time zone database has details about all time zone changes, like when a DST starts for a specific time zone or if the offset is going to change for a time zone and so on. If you delay updating the timezone database, It can lead to irreversible data errors in your database depending on the use case.

## UTC is not the ultimate solution!
Yes. You heard it right! UTC is not going to save you everywhere. Say you want to design a birthday reminder. You calculate the UTC timestamp of the next birthday 12 AM and store it in the DB. Works perfect right? Tomorrow the government announces a change in DST, and phew! Your stored time stamp is now wrong.

Do not store time in UTC for:
- Future date and time
- Date-only values

## More reading
This post is just a tip of the iceberg when dealing with time and time zones. Like I said, consider this a start. There are deeper things to consider. Make sure to do your research before getting your hands dirty.
- <https://stackoverflow.com/questions/2532729/daylight-saving-time-and-time-zone-best-practices>
- <https://www.moesif.com/blog/technical/timestamp/manage-datetime-timestamp-timezones-in-api/>

Here is a video about Timezones by Computerphile. I hope you'll find it useful and entertaining. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/-5wpm-gesOY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" style="display:block;margin:0 auto" allowfullscreen></iframe>