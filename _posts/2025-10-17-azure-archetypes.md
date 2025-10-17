---
title:  "Azure Landing Zones, Tailored with Archetypes for your organization's needs."
header:
  teaser: "/assets/images/Binary-Code-RLC-500x300.png"
categories: 
  - Code
tags:
  - Landing Zones, Archetypes
---
# Introduction and Point-of-view.
As a Cloud Consultant, I help organizations transition to the cloud. What I often see is that the decision to move to the cloud is made quickly. But the next question is just as important: how do you do this in a smart, secure, and future-proof way?
Fortunately, Microsoft provides clear guidance: the **Cloud Adoption Framework** (CAF). Within this framework, the **“Landing Zone”** is an essential component. This is the foundation on which you build your cloud environment. What makes it truly powerful is that we can tailor this foundation to your organization using archetypes.

# What is a landing zone?
A landing zone is essentially the foundation for your cloud environment. Think of it as the base of a house. You could start building right away, but without a solid foundation, everything risks collapsing over time. You also want to be able to use utilities like gas, water, and electricity in your house. Similarly, you ensure that the landing zone and everything you do in the cloud is secure, organized, and well-structured. Once this is set up, you can literally “land” your workloads here and connect them to your existing infrastructure.

# Archetypes, Modular Architecture, and Customization for Your Cloud Strategy
One of the most powerful aspects of this framework is the modular architecture built around archetypes. These archetypes are essentially predefined configurations that meet common organizational needs. Whether you are a startup, a medium-sized company, or a global enterprise, there is always an archetype that fits.
Some archetypes focus on platform operations, others on application landing zones. The beauty is that they are adaptable and can be combined based on your priorities.

>For example, as a platform component, you can choose a Security platform landing zone when security is your top priority. You might even set up your own SOC, where these specialists have a distinct set of rights and resources to keep the environment under control.

These are our three basic application landing zones:

* Corporate: An extension of the on-premises network with connectivity via a private connection, without direct access to the internet.
* Online-Isolated: No network connectivity to on-premises or Azure resources, only a direct connection to the web.
* Online-Connected: A combination of the two above, allowing resources to be accessed via the internal network as well as connecting to an API or a SaaS service.

Of course, you may want to add another variant, for example, for using AI or Sovereign Landing Zone to meet specific requirements without interfering with other workloads or granting access to unwanted sources.

By making this separation based on archetypes, policies can be enforced that are very specific, which ensures both security and manageability. This applies not only to the management burden but also to the costs of these resources.

# What I have learned.
The best cloud projects start with collaboration. When IT, security, and business are involved from the beginning, the landing zone becomes a strategic tool rather than a technical puzzle.
Another important lesson is the value of automation. By using infrastructure-as-code, we can consistently implement and manage your landing zone across different environments. This reduces errors, speeds up delivery, and makes it easier to adapt as your needs change.
