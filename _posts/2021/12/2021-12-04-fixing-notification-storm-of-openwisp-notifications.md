---
title: Fixing notification storm of OpenWISP Notification
---

[OpenWISP Notifications](https://github.com/openwisp/openwisp-notifications)
brought the notification functionality to OpenWISP.
It provided a handy abstraction to create notifications for different events
triggered in OpenWISP. Hence allowing users to stay updated on their networks.

But there existed a major shortcoming of OpenWISP Notifications, the
notification storm. Whenever there is an event that affects the whole network
(e.g. a power outage), the system will create an enormous amount of notification
due to which the UI becomes unusable.

If you are still wondering "What is a notification storm?", here's a demo video
for you:

<blockquote class="imgur-embed-pub" lang="en" data-id="a/beEsScN"  ><a href="//imgur.com/a/beEsScN">OpenWISP Notification Storm</a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>

To be able to handle a notification storm, the system should be able to
determine that a notification storm is underway. Therefore, preventing a
notification storm was a two-part job - adding the detection capability
and adding the throttling capability.


### Detection Mechanism

The detection mechanism contained a database query that counts
the number of notifications for a user in the last `X` seconds. While this simple
implementation was capable to trigger the throttling mechanism, it failed
to recognize notification storms that spanned over a longer time. To counter
this, we added another database query that checked notifications count
over a longer period of time.

Hence, the notification storm detection mechanism perform a short term check -
to handle sudden bursts of notifications - and a long term check -
to handle notifications that are a continuation of the notification storm.

It should be noted here that the system does not determine a notification
storm from the type of event that triggered it. Though, this will be a
cool thing to do.

### Throttling Mechanism

I added a throttling mechanism for the WebSocket consumer delivering
notifications to the frontend. It consists of a simple additive increase
back-off that skips sending notifications until a maximum upper limit
is reached, upon which the back-off gets reset.


Like everything else in OpenWISP, [the notification storm prevention
mechanism is configurable](https://github.com/openwisp/openwisp-notifications#openwisp_notifications_notification_storm_prevention).
