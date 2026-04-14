---
title: "Bug # 1729"
Space: Platform Engineering
created-by: atonal440
created-date: 2026-04-08T03:51:29Z
labels: 
	- under-investigation 
	- p3 
	- duplicate-content
	- updated
---
# Summary

Multiple user accounts appear post at the exact same millisecond with no obvious connection. 

# Impact

3,966 users across seven occurences

# Steps to Reproduce

Unknown 

# Observed Behavior

415 user accounts appear to have posted at exactly 2026-04-07T14:23:11.347Z. In and of itself this would not be too remarkable: a busy millisecond, but we can handle it. This happened again at 2026-04-07T22:08:44.891Z, this time with 533 user accounts (no overlap with the original list.) This is when I noticed the pattern, just a couple of weird spikes in the database graph, with no corresponding change in network traffic. I went and looked at the http proxy logs for those windows, and there's nothing there. Some of these accounts are posting regularly but none of them made any requests within 300ms on each side of the incidents. 

The posts themselves look mostly normal, broad mix of languages and content with no particular trends. The only interesting outlier is a single post with a timestamp 1ms later than the first incident, id p7xK2mQ9, that reads "It worked! maybe"

**UPDATE:**

Several more occurrences, I'll keep track of them here.

**2026-04-09T11:17:03.023Z** - 512 user accounts.

**2026-04-10T08:42:57.614Z** - 677. One delete in this batch: p7xK2mQ9, that weird post from the first one.

**2026-04-10T19:04:18.758Z** -  698. I checked the sequence_ids  in the database for these posts and they're all way ahead of the posts  before or after. I'd change them, but they're so far ahead it won't be a problem for a long while: I'll just leave it as evidence. 

**2026-04-12T00:33:52.102Z** - 502. One of our app servers tried to connect to the db during this millisecond, only one. It got back a `max_connections_exceeded` error. It retried a moment later and everything was fine. 

**2026-04-12T16:55:06.439Z** - 629. I have absolutely no clue what is causing this. We really should have gone with mysql.

The overall trend is upwards, but slow enough that this isn't a resource problem for a while yet. At least it's a nice boost to our monthly active user counts.

# Expected Behavior

Posts written to the database are associated with http traffic logged by the proxy. Timestamps are spread out by latency and queueing and don't cluster on a single millisecond.