---
layout: post
title: "Spring AI Series: 'Hello World'"
tags: HIDS Spark ADFA-LD Review
author: "Pranjal Chakraborty"
---

> Disclaimer: Most of what I am writing in this series, you’ll find (in one form or another) in the Spring AI official reference guides. I myself have struggled to make a lot of their examples work — hence, this series. Also, no LLM tools were used to write these posts.

I started working with this project from a feeling that a lot of people do not realize how fun working with Spring is. The intuitive abstraction that we have enjoyed for so long in so many components, is now also available for AI if you are looking to involve Agentic workflows into your Spring Boot architecture. Spring AI has production ready versions available already, ready to be deployed in real world projects. In this series, we’ll be building one such project, block by block. Yes, there will be full stack development components involved, since we’re trying to build something “real-world”, but priority is to explore the Agentic aspects of the development.

Let’s dive in!

> Repository: https://github.com/pranjalcborty/spring-ai-agentic-starter

## Setting up your build script

Since this is our “Hello World” project, we’ll be starting with the bare minimum, without sacrificing what Spring AI is offering us. I am using Gradle as my build tool, but you can go with Maven.

The only lines that need some explanation here are -

1. We are using one of the lightweight (you’ll see in the next section) Gemini models, mainly because it still has a “functional” free tier!
2. The Maven BOM (Bill of Materials) dependency for Spring AI. It basically imports a bunch of Spring AI specific dependencies.

```java
plugins {
    id 'java'
    id 'org.springframework.boot' version '3.5.8'
    id 'io.spring.dependency-management' version '1.1.7'
}

group = 'net.pranjal'
version = '0.0.1-SNAPSHOT'
description = 'AgentDemo'

java {
    toolchain {
        languageVersion = JavaLanguageVersion.of(17)
    }
}

repositories {
    mavenCentral()
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    implementation 'org.springframework.ai:spring-ai-starter-model-google-genai'
}

ext {
    set('springAiVersion', "1.1.0")
}

dependencyManagement {
    imports {
        mavenBom "org.springframework.ai:spring-ai-bom:${springAiVersion}"
    }
}
```

## Application Properties

Again, very minimal setup here as well. In the coming installments we’ll be adding a bunch of parameters to be able to perform vector search in PostgreSQL database and achieve RAG.

We’re using `gemini-2.0-flash-lite`, but based on your need, you can pick `gemini-2.0-flash`, `gemini-pro`, and `gemini-1.5-flash` too.

You can log in to Google AI Studio to get your own API key! In the future, we’ll replace this using Ollama and have our model running locally.

```properties
spring.application.name=AgentDemo
spring.ai.google.genai.chat.options.model=gemini-2.0-flash-lite
spring.ai.google.genai.api-key=${GEMINI_API_KEY}
```

## “Hello World”

And now comes the actual controller. As I said before, this is a very basic controller for now, but we’ll keep building on this.

The `ChatClient.Builder` is “autoconfigured” to use Gemini as the provider, based on the Gemini dependency we’ve added. We can have multiple bean configuration to have multiple models in our project overriding this default behavior. We’ll explore those later on.

```java
public class AssistantController {

    private final ChatClient ai;

    public AssistantController(ChatClient.Builder ai) {
        this.ai = ai.build();
    }

    @GetMapping("/assistant")
    String inquire(@RequestParam String question) {
        return ai
                .prompt()
                .user(question)
                .call()
                .content();
    }
}
```

Here, we have exposed an API that receives a `java.lang.String` and sends it as a prompt to Gemini. And, since we have not set up continuous conversation (which we will do eventually), every query is in a new context!

!["Say my name"](/assets/images/2.png)

---

If you have all these working, congratulations! If you think this was all too simple, you are right and that was the intention. We’ll try creating an API where we can have continuous conversation (and some more) in the next installment. See you there.
