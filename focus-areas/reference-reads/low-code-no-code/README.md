---
description: Cocreation Platform
---

# Low Code No Code

Digit Low Code No Code will enable citizens, government employees and partners to rapidly compose new solutions on top of the platform using a visual editor. Knowledge of coding languages is not required. It has been premised that such a platform will not only expedited development but also make it easier for everyone to create new applications. Especially, for government across the world trying to digitize their services and processes - low code no code can lead significant acceleration.

Enter any government office and one will see loads of forms. To avail a service or apply for a scheme, one needs to fill one of these forms, attach relevant documents and submit it at the counter. Depending on the nature of the application, it is routed from one officer to another till it’s registered in a registry. Then an appropriate certificate is issued that will enable to citizen to access the service or benefit from the scheme.&#x20;

Today many of these forms are being digitised by developing discreet applications which are often poorly written and difficult to maintain & expensive to modify.&#x20;

We are proposing to build an open source low code no code platforms which will allow government employees, vendors and citizens to design applications using a visual application designer. Behind the scene the designer will emit an application model based on an open application modeling language or specification. The model will be registered into an an application runtime that will bring up the appropriate application model based on the user action. It will display the appropriate interface e.g. form or execute the appropriate workflow. The data will be stored in an electronic registry in a secure, private and immutable manner. If required, a digit certificate will be issued which can be verified online.&#x20;

Building such a low code no code based CoCreation environment based on open application specifications will unlock this space and enable government organisation to digitise these processes rapidly. It will ease the access, remove inefficiency, increase observability and ease maintenance & upgrades. It will enable governments to adopt these technologies without being locked into vendor proprietary platforms and infrastructure.&#x20;

Building an open collaboration environment around these open low code no code environment will enable government, citizens and business including startups to collaborate and co-create new services and rapidly evolve them to meet the needs of the citizens. The underlying open specifications and the accompanying open source implementation will enable multiple startups to innovate and compete in building better platforms. This will create a new digital ecosystem of players.&#x20;

Typically a low code no code platforms have the following components

1\. User Interface or Interaction Designer and User Interface or Interaction Runtime Engine

2\. Process or WorkFlow Designer and Process or Workflow Runtime Engine

3\. Reports Designer and Reports Engine

\


![](<../../../.gitbook/assets/image (15) (1).png>)

Users are able to use the designers to specify user interface, flow and reports. This results in a well defined specification which are stored in the files system or database. These specifications are used by the runtimes to display the UI, orchestrate the flow and generate the reports. \


Depending on the scenario, users can start by designing the entities e.g. Order and then generate the forms/views on the entity. Or the users can design the form e.g Google Forms and the entities get generated in the background. The associated CRUD API for these entities are also generated. \


Advent of schema free (no sql) databases and support for storage of json objects in relational databases has enabled storage of both the specifications as well as entities who schema is specified by the specifications. \


The creation, updation and deletion of these entities generates events that can trigger the workflow specified by the workflow designer.  These workflows are typically a chain of event-condition-actions. Events contain reference to the entity on which the conditions is applied which are typically if-then-else rules. If the conditions are met then actions are executed which can be creating, updating or deleting another entity or calling an API or external service which can assign, notify users to take appropriate actions. \


As entities are modified the modified information is pushed into a message queue and then into an analytical datastore. The reports specified by the reports designer executes against this datastore (which is typically read fast e.g. ElasticSearch)\


![](<../../../.gitbook/assets/image (51).png>)
