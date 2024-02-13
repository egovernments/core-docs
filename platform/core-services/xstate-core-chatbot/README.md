# XState Core Chatbot

## Overview

**Goal:** To onboard developers onto the XState-Chatbot code base so that they can modify existing flows or create new ones.

This document sticks to explaining the chatbot's core features and does not dive into the use cases implemented by the chatbot.&#x20;

### Chatbot Fundamentals

This chatbot handles basic form-filling within a chat flow by collecting user information and making API calls to the rainmaker backend services to meet user needs. It utilizes StateCharts, similar to State Machines, to manage the user's state in the chat flow and store provided information. XState, a JavaScript implementation of StateCharts, is employed to code all chat flows.

This chatbot does not have any Natural Language Processing component. In future, we have plans to extend the chatbot to add such features.

### XState - Basic Introduction

XState is a JavaScript implementation of StateCharts. There is detailed documentation available to study XState. Some of the XState concepts used in the Chatbot are listed below. Basic knowledge of these concepts is necessary. It can also be learned while going through the chat flow implementation of pilot use cases in PGR and Bills.

1. [State](https://xstate.js.org/docs/guides/states.html)
   * [State Nodes](https://xstate.js.org/docs/guides/statenodes.html)
   * [Hierarchical State Nodes](https://xstate.js.org/docs/guides/hierarchical.html)
2. Actions
   * onEntry
   * [invoke…onDone…onError](https://xstate.js.org/docs/guides/communication.html#the-invoke-property)
3. [Guard Conditions](https://xstate.js.org/docs/guides/guards.html#guards-condition-functions)

Below are some tips for using XState, which have been followed throughout the pilot chat flows:

1. When transitioning to a state that is not at the same hierarchical level, assign a unique ID value. If the state has an ID, address it using the # qualifier in the target attribute.
2. Ensure that each state has a unique ID value to avoid duplicates. Having duplicate IDs can cause unexpected behavior in the application.
3. Surround any actions, such as onEntry, with 'assign' for effective handling of state changes and updates.

```
assign( (context, event) => { ... } )
```

This includes almost all functions except the guard condition code snippets.

## Pre-requisites

* NodeJS
* [XState](https://xstate.js.org/docs/)
* PostgreSQL
* Kafka(_optional_)

## Key Functionalities

* Build a chat flow to facilitate a user to interact with rainmaker modules
* Link a chat flow with back-end services

## Deployment Details

1. Deploy the latest version of xstate-chatbot
2. Configure /xstate-chatbot to be a whitelisted open endpoint in zuul
3. Add [indexer-config](https://github.com/egovernments/configs/blob/DEV/egov-indexer/chatbot-telemetry-v2.yaml) to the egov-indexer to index all the telemetry messages

<table><thead><tr><th width="238">Environment Variable</th><th>Description</th></tr></thead><tbody><tr><td><code>WHATSAPP_PROVIDER</code></td><td><p>The provider through which WhatsApp messages are sent &#x26; received. An adapter for ValueFirst is written. If there is any new provider a separate adapter will have to be implemented.</p><p>A default <code>console</code> adapter is provided for developers to test the chatbot locally.</p></td></tr><tr><td><code>REPO_PROVIDER</code></td><td><p>The database used to store the chat state. Currently, an adapter for PostgreSQL is provided.</p><p>An <code>InMemory</code> adapter is provided to test the chatbot locally</p></td></tr><tr><td><code>SERVICE_PROVIDER</code></td><td><p>If it’s value is configured to be eGov, it will call the backend rainmaker services. If the value is configured as Dummy, dummy data would be used rather than fetching data from APIs.</p><p>Dummy option is provided for initial dialog development, and is only to be used locally.</p></td></tr><tr><td><code>SUPPORTED_LOCALES</code></td><td>A list of comma-separated locales supported by the chatbot.</td></tr></tbody></table>

Other configuration details are mentioned as part of the [XState-Chatbot Integration Document](xstate-chatbot-integration-document.md).

## Chat Flow&#x20;

Below are some guidelines for coding chat interactions using XState:

1. Interaction with the user, such as sending a message or processing incoming messages, should be coded as states in the State Machine.
2. It's recommended to test any chat flow using the provided react-app. Follow the instructions in the README file of the react-app for testing.
3. Follow standard patterns when coding chat interactions. These patterns are explained below and can also be studied by browsing through the code of pilot use cases like PGR and Bills.
4. Chat states should only contain dialogue-specific code. Backend service-related code should be written in separate files, such as ...-service.js.
5. Code that doesn't involve asynchronous API calls can be written within the onEntry function or action.
6. If an API call is needed, follow the invoke-onDone pattern. Write asynchronous functions in separate service files, and process the consolidated data returned by these functions in the dialogue file's state.
7. Helper functions should be written in the dialog.js file. It's advisable to use these functions instead of writing custom logic in dialogue files whenever possible.

## Scaffolding

Apart from the chat flow and its backend service API calls, a few other components are present in the project. These components do NOT need to be modified to code any new chat flow or changed for an existing chat flow. These components with a short description for each are listed below:

1. **Session Manager:** It manages the sessions of all the users on a server. It stores, updates and reads the user’s state in a datastore. Based on the state of the user, it creates a state machine and sends the incoming message event to the state machine. It sanctifies the state data (any sensitive data like the name and mobile number of a user are removed) before storing it in the datastore.
2. **Repository:** It is the datastore that stores the user states. To reduce dependency, an in-memory repository is also provided configured using environment variables. So to run the chatbot service, Although PostgreSQL is not a strict requirement, using it as the repository provider is recommended.
3. **Channel Provider:** It supports multiple WhatsApp Providers. Any one of the providers is configured for use. A separate `console` WhatsApp Provider is present for the developer to test the chatbot server locally. Additionally, a Postman collection is provided to simulate receiving messages from users to the server..
4. **Localisation:** Messages to be sent to the user are stored within the chatbot. Here, the localisation service is not used. The messages are typically present near the bottom of the dialogue files. A separate localisation-service.js is provided to retrieve the messages for the localisation codes not owned by the chatbot. For example, the PGR complaint types data is under the ownership of the PGR module, and the messages for such can be fetched from the egov-localization-service using the functions provided in the localization-service.js.
5. **Service Provider:** Simplifies initial dialogue development by allowing configuration of a dummy service instead of coding API calls to backend services. This can be set up via environment variables and modifying the service-loader.js file.
6. **Telemetry:** Chatbot logs telemetry events to a Kafka topic with the provision to mask any sensitive data before indexing the events onto ElasticSearch by egov-indexer. Below are the list of events that get logged:
   * Incoming message
   * Outgoing message
   * State transitions
