---
layout: post
title: "Spring AI Series: #5 Observability: Spring AI and Beyond"
tags: spring-ai spring
author: "Pranjal Chakraborty"
published: false
---

> This blog is part of a series on [Spring AI](https://pranjal.net/blog/tag/spring-ai.html). Check out the previous article in this
> series: [Model Context Protocol (MCP) [and Tool Calling 2]](https://pranjal.net/blog/2025/12/10/spring-ai-mcp.html).

Observability is crucial for any user facing system, and the job gets even harder with microservices architecture and with high traffic. To make our lives easier,
we rely on various observability tools to monitor our systems so that we can take action before user experience takes a hit. LLM-driven AI systems introduce a unique 
problem here. AI hallucination is real, and since prompt engineering is more of an art than science, these GenAI based tools' behavior in the wild isn't deterministic. 
So, keeping a close eye on the system becomes even more important. Then there's the economic part of it too. If you're using the cutting edge LLMs provided by OpenAI or Google, you are
paying them by the every input and output token. So, now that's another thing to keep an eye on.

Fortunately, Spring AI makes our lives a lot easier in this regard. All we have to do is to have a observation pipeline up and running, and that's where you'll be spending 
most of your time. Configuration on the Spring AI side is very minimal to say the least.

There are 3 basic components to monitor when it comes to observability-
1. Metrics - Observing the system metrics, basically to monitor resource usage
2. Logs - Observing the application logs to keep an eye on errors and faults
3. Traces - Observing the application or system activity. Traces are much more detailed and gives a more granular picture of the system behavior.

What we'll do in this installment, is we'll set up a observability pipeline, covering each of these 3 components with Grafana in the center.

## Metrics Collector

