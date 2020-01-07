# How to manage google analytic events

![How to manage google analytic events](/assets/how-to-manage-google-analytics-events/head.png "How to manage Google Analytic events")

Google Analytics is a helpful platform for understanding how your customers are using your website.
Out of the box you get some fairly useful functionality such as, what pages customers are arriving on, what pages they go to after they've landed and if they're a new or returning user.
These standard metrics are great, what they don't cover is the smaller actions, like clicking a button, buying a product or interacting with your site.

To track these small interacts it's best to use the events in Google Analytics.
Before you begin setting up the events, it's important to think about what you're going to be reporting on.
This will inform how you create your events.

Here's some examples of things you might want to track:

- A customer buying a product
- When somone signs up to your mailing list
- How far someone gets through a form on your website
- When someone logs in

## Event Categories, Event Actions and Event Labels

Now you have your goal it's important to understand the 3 main abstractions in Google Analytic events.
There's three types of events

- Event Categories
- Event Actions
- Event Labels

They are layed out in a hierarchy

![Google analytics event hierarchy](</assets/how-to-manage-google-analytics-events/event heigharchy.png> "Google analytics event hierarchy")

Simply put, an event category has many event actions which have many event labels. To put this into practice let's use a YouTube video as an example. A YouTube Video can be paused, made fullscreen and liked.

The events for these interactions might look like

| Event Category | Event Action | Event Label |
| -------------- | :----------: | ----------: |
| Video          |    Pause     | 8PTDv_szmL2 |
| Video          |  Fullscreen  | 8PTDv_szmL2 |
| Video          |     Like     | 8PTDv_szmL2 |

All the actions the user has performed has been put into the Video Event category, this is because the interactions were happening on the video page specifically with the video. If we wanted to track user comments, we might add a new event category for that called 'comments'.

The event actions are all different based on the type of action the user performed on the video. Finally the Event Label is the video id, this allows us to report on the actions of users on a particular video. If you had an ecommerce store this could be your product id, enabling you to see how people are interacting with a specific product.

## Reporting on events

The inbuilt reporting on events in Google Analytics is really difficult to get any valuable information out.
To make the most of your events you're better off making a `custom report`.

![Google analytics event hierarchy](</assets/how-to-manage-google-analytics-events/New customreport.png> "Google analytics event hierarchy")

To create the event report add the following settings

![Google analytics event custom report](/assets/how-to-manage-google-analytics-events/customreportsetup.png "Google analytics event custom report")

With this report you can now see how often events are occuring on certain assets on you're site. You can also aggregate the results by removing the event label measure. This will show you all the times a video was paused using our YouTube example.

Additionally you can share your custom report with the rest of your team, or even get it e-mailed to you every day. The daily email can really help, at The Big Crunch we have a few daily reports that I use.

## Google Analytics API

After creating a custom report you'll quickly run into a bunch of limitations with it, where it's really limited is in the `grouping` functionality. It doesn't have great pivot table support.
To get around this issue I've created a custom report, then called the Google Analytics API using a terminal program on my laptop to get access to all the data. Once I've exported it all I can visualise it and group it however I like. When calling the API lots be aware of the API limits, it's not great if Google cuts you off from their API. I try to do it sparingly and only run these reports weekly or monthly.

## DNT (do not track) policy

The final thing to consider when using Google Analytics is the DNT policy setting in modern browsers.
Hidden deep within the depths of most browsers today is a DNT setting which is switched off by default, however, if someone does turn it on it's best practice to honour the setting and not enable Google Analytics. About 10% of the world's internet users have the DNT switch flipped to the on position, the problem being that the browser doesn't automatically remove the Google Analytics tracking script if it's switch to on. It's up to you to not run Google Analytics and respect the privacy of your customers.

Medium has done a lot of work pushing DNT into the main stream and I recomend you have a read of their policy if you would like to learn more. [Medium DNT policy](https://medium.com/policy/how-we-handle-do-not-track-requests-on-medium-f2b4b4fb7c5e)
