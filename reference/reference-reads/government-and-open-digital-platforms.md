---
description: Draft - Work in Progress
---

# Government and Open Digital Platforms

### Governments - A Complex Web Of Interactions

Governments provide multiple services to their citizens in areas such as education, health, food, law and order, and energy, among others. To do so, revenue is collected via taxes on income, property, and sales, as well as through payment on services such as water and electricity. In addition, various targeted welfare programs or schemes such as direct benefit transfers to weaker sections of the society, or food distribution at lower prices are launched by governments. To deliver these services and schemes, the government has to interact with vendors from different industries.&#x20;

![](<../../.gitbook/assets/image (14).png>)

Most countries also have a federal structure, where responsibilities are distributed between national, sub-national, and local governments - which are further bifurcated into departments and sub-departments - to deliver services and collect revenue. The departments, in turn, are categorised by geographical locations into zones, districts, blocks, and villages, to facilitate smooth delivery of services/programs across the country.

In India, for example, the national government has 40-plus ministries and 20-plus independent bodies. Every ministry has three to five departments, and each consists of five sub-departments. There are 36 sub-national governments: 28 states and 8 union territories. Each has its own departments and sub-departments. The snapshot from the local government directory website (https://lgdirectory.gov.in) below gives the numbers of districts, sub-districts, blocks, villages and local bodies.

![Snapshot from Local Government Directory (https://lgdirectory.gov.in) ](<../../.gitbook/assets/image (244).png>)

Many of these ministries, departments, sub-departments interact (exchange information) and transact (exchange money) to facilitate the delivery of services and programs run by the government. One can only try to understand how complex these interactions might get. &#x20;

### Encoding Complex Interactions Into Digital Applications Leading To Sub Optimal Equilibrium

In the digital age, the interactions at the government level are undergoing rapid transformation. Applications are helping digitize the interactions, automate tasks and coordinate the flow of information too. While this does deliver the benefits of automation, it also ends up hard coding these interactions into software, locking the associated data in closed databases that are run on non-scalable hardware architecture. As each department builds these applications, the complex interactions within the ecosystem get encoded into various applications resulting in fragmented and siloed data. Data updates and access to real-time data becomes a challenge for the end-users of the services/programs. Consequently, citizens and vendors have to run from pillar to post to update or make changes in the data. Administrators, on the other hand, struggle to get an integrated view of the data on time, resulting in delayed or incorrect decisions.

![](<../../.gitbook/assets/image (310).png>)

It becomes the citizen's and the vendor's responsibility to keep data updated in these departmental applications - who have to run from pillar to post filling forms, attaching proofs and standing in long lines to submit these applications. At the same time, administrators struggle to get integrate view of the data at the right time, thus forced to either delay decisions or make decisions based on gut.&#x20;

To address these concerns, departments start integrating these siloed departmental applications and also many of them build out multitude of web and mobile apps for citizens and vendors. (_Design of many of these applications are not taking into account the diversity, access and infrastructure issues into considerations leading to increasing the "digital divide" - but that is another important issue that needs separate attention and will not be discussed here._ )

As these applications start getting integrated with each other, the interactions get further etched into software code and proprietary data exchange mechanisms designed by software engineers. Over period of time, making changes to these data exchange mechanisms requires cascading changes across the several departmental applications which becomes a very expensive proposition and a program management nightmare - leading to multiple failures in technology implementations. As implementation failures increase, no government officer is willing to take the risk of initiating the change. The entire ecosystem gravitates towards a sub-optimal equilibrium.

It's important to understand the problem does not exist in technology but in the architecture or the design of how the interactions are encoded into - siloed applications encapsulating fragmented databases using proprietary data exchange formats running on non-scalable hardware. Platform based approach tries to address these challenges.&#x20;

### Platforms can help unlock and realize new possibilities

In 1890s, several large cities like London and New York where debating the "Great Manure Crisis". As cities were growing, the number of horse carriages were increasing. London had 50000 horses - each generating 15-35 pounds of shit. This was leading to several issues like health, land for stable, food for horses etc. An article in Times, London 1894 stated - "In 50 years, every street in London will be buried under nine feet of manure". The problem seemed so insurmountable that many proclaimed that urban civilisation was dead. By 1912, this seemingly insurmountable problem had completely disappeared, automobiles powered by internal combustion engines built by 400+ manufactures had replaced the horse carriages. Today, London has 2.6M registered cars.&#x20;

Internal combustion engine (ICE) is an example of a platform building block. It solved a pivotal problem of converting fuel to motion. This unlocked the space, accelerating innovation - 400+ manufacturers of automobiles raced to build multiple end solutions e.g. Car, Trucks, Ships, Manufacturing Plants etc. ICE transformed how automobiles where built which reshaped how roads were built. This reshaped how cities where built.&#x20;

_Platforms are a set of highly reusable building blocks with high complementarity. Each building block solves a key pivotal problem in a manner that it can be reused for building multiple solutions._ &#x20;

#### Unintended Consequences and Need for Policy

Platforms are powerful and have unintended consequences e.g. Automobiles led to increase in accidents, obesity, increase in consumption of fossil fuels etc. Hence it is important that platforms are built in the open and co-created by involving stakeholders from across the ecosystem - government, business and citizens. Appropriate policy interventions should go hand in hand to accelerate adoption of the platform as well as ensuring its ill effects are stemmed.

**Digital Platforms**

Today we are surrounded by Digital Platforms like Google Search, Facebook, WhatsApp, Amazon, Uber. These are powerful platforms that solve pivotal problems and facilitate digital interactions & transactions for the participants in their ecosystem. Similarly, there are platforms like Aadhar, UPI, Sunbird, Digit Urban at different levels of maturity that are trying to solve pivotal problems, unlock the respective spaces they operate in and enabling ecosystems to build solutions on top of these platforms. &#x20;

#### Closed vs Open Platforms - Need for Governance

Closed platforms are like walled gardens. The businesses that own these platforms are gatekeepers and define the rules of engagement on these platforms that driven by their business goals. The rules are defined to ensure the value of these platforms accrue to the businesses that own and run them. The rules of engagement for Open platforms are shaped by an open collaborative process where everyone is free to participate. To ensure open platforms evolve in a coherent manner, it needs a proper governance body - to evolve the standards, ensure openness of building blocks, ensure free and fair distribution of value.

**Digital Building Blocks**

Digital Building Blocks that make up platforms can come in various forms. Some of them are listed below.

1. Protocols and Formats for Data Exchange e.g. SMTP, HTTP, HTML etc.
2. Shared Registries e.g. Aadhar
3. Data Exchange Platforms e.g. UPI
4. Shared Services e.g. Payment, Collection etc.

Protocols and Data Exchange Formats like SMTP enables seamless exchange of information. Anyone can participate in the ecosystem by building or installing an open source system e.g. email server or webserver, one doesn't need permission or pay hefty amount to the gatekeepers. Similarly, services provided by shared registries like eKYC on Aadhar can be accessed as long as one has appropriate permission from the citizen.&#x20;

The illustration below graphically summarizes all the above points about digital platforms and demonstrates how platforms can unlock new possibilities.

![](<../../.gitbook/assets/image (67).png>)

### Key Principles for Building Digital Platforms for Government

When building digital platforms especially for enabling interactions between government and citizens, it is important that certain key principles be applied to ensure its adoption, evolution and avoid its unintended consequences.

1. **Open** - We have already talked about that digital platforms are powerful and hence need to be open to ensure value is distributed across the actors of the ecosystem and concentrated to benefit a few. This requires that these platforms be built using an open process using open standards, technology, API and data principles.
2. **Unbundled/Modular -** To ensure high reuse, the building blocks must be unbundled to small, modular and well defined microservices. Instead of trying to pack complexity into one large integrated solution e.g. ERP, it is key that the problem space be broken down into smaller modular building blocks that can be assembled and also evolved independently.
3. **Federated -** The architecture of the platform must ensure value accrues to all stakeholder of the system. Traditional centralized application architectures tend to concentrate power in the hands of those who control the data. Special care must be given to ensure platform does not create information flow that create imbalance of power for the federated structure of the government.
4. **Security -** The data stored on these platforms are very high value and will be subject to continuous attacks. It is imperative that highest standards of security be applied for data at rest and in transit.&#x20;
5. **Privacy -** Governments deal with lot of private data about citizens, platform architecture must enforce wherever possible the privacy of individuals and enable solution developers to enhance the privacy.
6. **Minimum -** Even though high reuse is of high importance for platforms, it must store minimum data and functionality that is minimum and fit for purpose.
7. **Scalable -** Given the scale of government, its imperative that platform be designed to scale to sub-national and national scale.&#x20;

### **Digital Missions building Digital Platforms for accelerating Sustainable Development Goals**

Governments are starting to recognize the power of digital platforms - on one hand, they are trying to control to unintended consequences of large closed digital platforms and on the other hand, they are trying to build digital platforms to accelerate the attainment of developmental goals.&#x20;

**Digital Public Goods Alliance**

Initiatives like the Digital Public Goods Alliance ([https://digitalpublicgoods.net/](https://digitalpublicgoods.net/)) has been setup as a "_multi-stakeholder initiative with a mission to accelerate the attainment of the sustainable development goals in low- and middle-income countries by facilitating the discovery, development, use of, and investment in digital public goods._"&#x20;

### **Digital Platforms are powerful but are not "silver bullet" by themselves**

Digital Platforms are powerful and we are seeing some early successes, however, its important to highlight that these are still early days. Platforms require sustained cooperation and cocreation amongst multiple stakeholders to design, develop, implement and sustain.&#x20;

Any ecosystem is consists of various stakeholders interacting with each other. Information and communication technologies are disintermediating these interactions. As interactions get encoded in technology, we have an opportunity to rethink these interactions. Digital platforms through shared data registries, open protocols and common services unbundles the ecosystems, makes information available and provides an opportunity to rearchitect the interactions in ecosystem. Solution designers who build on top of the platform then at least have a chance to innovate and rebuild solutions that ensures the value and benefit accrues to all stakeholders. Development of multiple such solutions will unlock existing ecosystems that stuck in sub-optimal equilibriums (be it health, finance, education etc).

Platforms themselves are part of the solutions, the reimagination of these future possibilities will still need to be done and solutions will need to be built on top of these platforms. To make the point more clear, platforms like internal combustion engines make new solution e.g. cars, trucks possible, they create power opportunities but are not the "silver bullets".&#x20;



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this website by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
