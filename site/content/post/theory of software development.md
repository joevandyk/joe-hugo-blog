---
title: Joe's Method for Software Development
date: 2018-10-27T19:23:51.312Z
description: What seems to work well.
---
When planning new features, write down a quick summary/overview of the problem you are solving, and what you think the solution should be. Work with others to clarify this as needed. Then sketch it out on paper or whiteboard. Then send it out for feedback. Then revise the sketches and written summary. When doing this, always do the ideal solution -- pretend existing things don’t exist. If you need to pare down or modify features to make them fit reality, that’s fine, but you might be surprised out how fast building the ideal feature is.

Organize the feature into small chunks. Each chunk of work should be able to be deployed separately from each other.  Chunks of work should take no more than a day or so at maximum.

When working on the chunks of work, do the ones that require training others or getting UI feedback first.  If it’s a complicated feature, write a fake UI and show them the UI as soon as possible. This shouldn’t take more than 30 minutes or so.

We plan a week’s worth of stuff at once, and make every effort possible to do what we say we’re going to do that week. If things popup mid-week that prevent us from finishing the scheduled work, make sure to communicate that to others immediately. Push back on mid-week changes -- they are disruptive to the flow.

When starting work on a feature, try to stick with it until it’s finished. If you are blocked by something (i.e. getting feedback or getting data), be very loud and annoying to everyone in the vicinity until you get unblocked.

Add a high level unit test for the happy path that exercises a good amount of the code if using a language like Ruby that doesn’t check anything automatically for you. If the feature has complicated logic, unit test those complicated things.

If a thing can happen once, make sure it can happen two or three or four times without problems. https://stripe.com/blog/idempotency is a good example. The codebase has historically done a great job of this -- for example, if you reschedule an order to the same day that it’s already scheduled on, it does nothing. If you send an email to someone who already has received that email, it does nothing.

For the love of God, do not use ActiveRecord callbacks like `before_save` or `after_save`. Avoid using ActiveRecord validations.

Log what happens in the system. Every business operation should be logged. We have a way to broadcast an event that automatically gets logged. That’s invaluable in figuring out who changed what or when this thing happened.

Try to not make code generic immediately. Prefer copy and paste for the first couple versions until the right abstraction becomes apparent.

Make code searchable. Instead of a method called “available”, consider `is_bid_item_available` or similar. That’s a bad example, but you know what I mean. We want to be able to easily find all usages of a method, object, or attribute (which is super hard in a dynamic language). More explicit naming can help here.

> Work on behalf of users, not by their request. When they bring you ideas for features, dig for the problems they’re trying to solve. Few users are experts at designing software, but most of them are very good at sharing where it hurts and why.

> &dash; <a href="https://twitter.com/dhh/status/972214873646972928">dhh</a>

Be consistent in naming. VerbNoun (CreateProduct) is what we’ve been moving towards for actions or operations.

Ask for help immediately if you aren’t happy with the way things are turning out, or if you suspect there’s a cleaner way to do something.

Disable Slack notifications. Use phone or text messaging if there’s urgent problems. Use email for starting bigger conversations.

Be consistent in the codebase. Encourage others to be consistent. Point out inconsistencies as you notice them. I'm personally bad at being consistent. This includes things like naming patterns and how the code is structured.

It is criticial to see how systems are used in the real world, and to use the systems you build. If you are writing orders that allow others to pick orders, go to the fulfillment center and pick orders for a day. If you are writing software to help do customer service, do customer service for a day.
