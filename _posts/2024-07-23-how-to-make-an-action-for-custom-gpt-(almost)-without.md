---
layout: post
title: "Create a Custom GPT Action with Cloudflare Workers: A Step-by-Step Guide"
published: true
date: 2024-07-23
excerpt: "Learn how to create a custom GPT action using Cloudflare Workers, enabling your AI to check domain availability. This guide walks you through setting up a worker, integrating it with GPT, and testing the final product."
---


In today's rapidly evolving AI landscape, creating custom GPT actions can significantly enhance the capabilities of your AI assistants. This tutorial will guide you through the process of creating a custom GPT action using Cloudflare Workers, specifically for checking domain availability. By the end of this guide, you'll have a functional custom GPT that can generate domain ideas and check their availability in real-time.

![Demo of the Custom GPT Action](/assets/img/how-to-make-an-action-for-custom-gpt-(almost)-without-any-coding-using-cloudflare-workers/demo.gif)
## Prerequisites

Before we begin, ensure you have:

1. A Cloudflare account
2. Access to GPT-4 or a similar AI model with custom action capabilities
3. Basic understanding of JavaScript and API concepts

## Steps to Create Your Custom GPT Action

### 1. Setting Up Your Cloudflare Worker

First, we'll create a Cloudflare Worker to handle our domain checking functionality.

1. Log into your Cloudflare dashboard and navigate to the Workers section.
2. Click on "Create a Worker" to start a new project.

![Creating a new Cloudflare Worker](/assets/img/how-to-make-an-action-for-custom-gpt-(almost)-without-any-coding-using-cloudflare-workers/image_0.png)

3. You'll be presented with a default "Hello World" worker. Give your worker a name, such as "my-domain-checker".

![Naming your Cloudflare Worker](/assets/img/how-to-make-an-action-for-custom-gpt-(almost)-without-any-coding-using-cloudflare-workers/image_1.png)

4. Deploy this initial version of your worker by clicking the "Deploy" button.

![Deploying the initial worker](/assets/img/how-to-make-an-action-for-custom-gpt-(almost)-without-any-coding-using-cloudflare-workers/image_2.png)

### 2. Modifying the Worker Code

Now that we have our basic worker set up, let's modify it to check domain availability.

1. Click on the "Edit code" button for your newly created worker.

![Editing the worker code](/assets/img/how-to-make-an-action-for-custom-gpt-(almost)-without-any-coding-using-cloudflare-workers/image_4.png)

2. Replace the existing code with the following JavaScript:

```javascript
export default {
  async fetch(request, env, ctx) {
    // Extract the domain name from the request URL
    const url = new URL(request.url);
    const domain = url.searchParams.get('domain');

    if (!domain) {
      return new Response('Please provide a domain name using the "domain" query parameter.', { status: 400 });
    }

    try {
      // Attempt to resolve the domain using DNS
      const dnsResult = await fetch(`https://cloudflare-dns.com/dns-query?name=${domain}`, {
        headers: {
          'Accept': 'application/dns-json'
        }
      });

      const dnsData = await dnsResult.json();

      // Check if the domain exists based on the DNS response
      const exists = dnsData.Answer && dnsData.Answer.length > 0;

      return new Response(exists ? 'yes' : 'no');
    } catch (error) {
      return new Response('Error checking domain existence', { status: 500 });
    }
  },
};
```

3. Save and deploy your updated worker.

![Updated worker code](/assets/img/how-to-make-an-action-for-custom-gpt-(almost)-without-any-coding-using-cloudflare-workers/image_7.png)

### 3. Testing Your Worker

Before integrating with GPT, let's test our worker to ensure it's functioning correctly.

1. Use the testing interface provided by Cloudflare to send a request to your worker.
2. Add a domain parameter to test, for example: `?domain=example.com`

![Testing the worker](/assets/img/how-to-make-an-action-for-custom-gpt-(almost)-without-any-coding-using-cloudflare-workers/image_9.png)
![Testing the worker](/assets/img/how-to-make-an-action-for-custom-gpt-(almost)-without-any-coding-using-cloudflare-workers/image_11.png)

If everything is working correctly, you should see a response of "yes" for existing domains and "no" for non-existent ones.

### 4. Creating a Custom GPT

Now that our worker is operational, let's create a custom GPT that utilizes this functionality.

1. Navigate to the GPT interface and create a new custom GPT.
2. Give your GPT a name and description related to domain checking.

![Creating a new custom GPT](/assets/img/how-to-make-an-action-for-custom-gpt-(almost)-without-any-coding-using-cloudflare-workers/image_101.png)
![Creating a new custom GPT](/assets/img/how-to-make-an-action-for-custom-gpt-(almost)-without-any-coding-using-cloudflare-workers/image_12.png)
![Creating a new custom GPT](/assets/img/how-to-make-an-action-for-custom-gpt-(almost)-without-any-coding-using-cloudflare-workers/image_13.png)
![Creating a new custom GPT](/assets/img/how-to-make-an-action-for-custom-gpt-(almost)-without-any-coding-using-cloudflare-workers/image_14.png)

### 5. Adding the Custom Action

To enable our GPT to use the Cloudflare Worker, we need to add it as a custom action.

1. In the GPT creation interface, find the "Actions" section and click "Add action".
2. You'll need to provide a schema for your action. Use the following OpenAPI schema. 

The schema can be generated using openai or Claude with the following prompt: 


```
Make a Schema for the method below . use the domain
< ADD YOUR WORKER CODE HERE>

Schema example: 

{
  "openapi": "3.1.0",
  "info": {
    "title": "Get weather data",
    "description": "Retrieves current weather data for a location.",
    "version": "v1.0.0"
  },
  "servers": [
    {
      "url": "https://weather.example.com"
    }
  ],
  "paths": {
    "/location": {
      "get": {
        "description": "Get temperature for a specific location",
        "operationId": "GetCurrentWeather",
        "parameters": [
          {
            "name": "location",
            "in": "query",
            "description": "The city and state to retrieve the weather for",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "deprecated": false
      }
    }
  },
  "components": {
    "schemas": {}
  }
}
```

The result from Claude or ChatGPT should look like this:



```json
{
  "openapi": "3.1.0",
  "info": {
    "title": "Domain Existence Checker",
    "description": "Checks if a domain name exists.",
    "version": "v1.0.0"
  },
  "servers": [
    {
      "url": "https://my-domain-checker.36ooagwp.workers.dev"
    }
  ],
  "paths": {
    "/": {
      "get": {
        "description": "Check if a domain exists",
        "operationId": "checkDomainExistence",
        "parameters": [
          {
            "name": "domain",
            "in": "query",
            "description": "The domain name to check",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Successful response",
            "content": {
              "text/plain": {
                "schema": {
                  "type": "string",
                  "enum": ["yes", "no"]
                }
              }
            }
          }
        }
      }
    }
  }
}
```

3. Test the action to ensure it's working correctly.

![Testing the custom action](/assets/img/how-to-make-an-action-for-custom-gpt-(almost)-without-any-coding-using-cloudflare-workers/image_16.png)

### 6. Configuring GPT Behavior

To make our GPT use the new action effectively, we need to provide it with clear instructions. Add the following prompt to your GPT's configuration:

```
You are an AI assistant tasked with generating domain name ideas for a given topic and checking their availability. Follow these instructions carefully:

1. You will be given a topic. Your task is to generate creative and relevant domain name ideas for this topic.

2. The topic you will be working with is:
<topic>
{{TOPIC}}
</topic>

3. Generate at least 5 domain name ideas related to the given topic. Be creative and consider various aspects of the topic, including synonyms, related concepts, and catchy phrases.

4. For each domain name idea you generate, you must check its availability using the CheckDomainExistence action.

5. After checking each domain, provide a list of all the domain names you generated, along with their availability status. Format your output as follows:
- For available domains: [AVAILABLE] domain_name
- For unavailable domains: [UNAVAILABLE] domain_name

6. Present your final list of domain names and their availability inside <domain_list> tags.

Here's an example of how your output should look:

<domain_list>
[AVAILABLE] example-topic-hub.com
[UNAVAILABLE] besttopicsite.net
[AVAILABLE] mytopicworld.org
[UNAVAILABLE] topicmaster.com
[AVAILABLE] all-about-topic.net
</domain_list>

Remember to generate at least 5 domain names and check each one.
```

### 7. Testing Your Custom GPT

Now that everything is set up, it's time to test your custom GPT.

1. Start a conversation with your GPT and ask it to generate domain names for a specific topic.
2. The GPT should generate domain ideas and check their availability using the custom action.

![Testing the custom GPT](/assets/img/how-to-make-an-action-for-custom-gpt-(almost)-without-any-coding-using-cloudflare-workers/image_22.png)

## Conclusion

Congratulations! You've successfully created a custom GPT action using Cloudflare Workers. This powerful combination allows your AI to perform real-time domain availability checks, making it an invaluable tool for brainstorming and validating domain name ideas.

Remember, this is just the beginning. You can extend this concept to create more complex actions, integrating various APIs and services to enhance your GPT's capabilities further.

Happy coding, and enjoy your new custom GPT!