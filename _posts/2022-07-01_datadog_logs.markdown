---
layout: post
title: 'Ruby on Rails: Searching DataDog Logs'
tags: []
type: post
published: false
---

This post is meant as a cheat sheet for using the [DataDog](https://docs.datadoghq.com/getting_started/application/) observability app in conjunction with Ruby on Rails.

Observability of web applications (logging, metrics, monitoring etc.) remains an area of growth for me. At my day job, we use DataDog. I often go a month at a time without needing to look anything up in the logs. But when I need DataDog for diagnosing an issue I suddenly _really_ need it, and I'm never as fluent as I'd like to be. This post is meant as a refresher for myself and others.

<!--more-->


## DataDog configuration

The DataDog Agent and `ddtrace` gem run on your server and report events to DataDog. You may want to consult your app's initializers to confirm how DataDog is configured. Read up on that in the official [documentation for Ruby integration](https://docs.datadoghq.com/tracing/setup_overview/setup/ruby/).


## Facets

I can never remember the ["facets"](https://docs.datadoghq.com/logs/explorer/facets/) (attributes) of log messages used to narrow down searches. Among many, many other things, facets can be used to find only requests to a specific Rails controller or action, to find only messages from a specific environment (e.g. staging vs. production), etc. But my company has over 300 facets enabled, and the important ones can easily get lost in the noise.

I'm going to skip most facets, and focus on the ones I view as essential.

* [`service`](https://app.datadoghq.com/logs?query=service%3Amyapp-staging): Can be used to split logs up by the microservice that logged them, but at my company separate environments (qa, staging, production, etc.) are separate "services". Enter `service:myservicename` in the search box.
* [`status`](https://app.datadoghq.com/logs?query=status%3Aerror): Usually corresponds to log levels: (`error`, `warn`, `info`, `debug`, or `ok`). Enter `status:mystatusname` in the search box. DataDog [query syntax](https://docs.datadoghq.com/tracing/trace_explorer/query_syntax/) supports _excluding_ a facet, so e.g. you could find all records where status is _not_ `ok` with `-status:ok`.
