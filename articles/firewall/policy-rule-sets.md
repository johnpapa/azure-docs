---
title: Azure Firewall policy rule sets
description: Azure Firewall policy has a hierarchy of rule collection groups, rule collections, and rules.
services: firewall
author: vhorne
ms.service: firewall
ms.topic: article
ms.date: 09/12/2022
ms.author: victorh
---

# Azure Firewall Policy rule sets

Firewall Policy is a top-level resource that contains security and operational settings for Azure Firewall. You can use Firewall Policy to manage rule sets that the Azure Firewall uses to filter traffic. Firewall policy organizes, prioritizes, and processes the rule sets based on a hierarchy with the following components: rule collection groups, rule collections, and rules.

:::image type="content" source="media/policy-rule-sets/policy-rule-sets.png" alt-text="Azure Policy rule set heirarchy":::

## Rule collection groups

A rule collection group is used to group rule collections. They're the first unit to be processed by the Azure Firewall and they follow a priority order based on values. There are three default rule collection groups, and their priority values are preset by design. They're processed in the following order:


|Rule collection group name  |Priority  |
|---------|---------|
|Default DNAT (Destination Network Address Translation) rule collection group      |100|
|Default Network rule collection group      |200|
|Default Application rule collection group      |300|

Even though you can't delete the default rule collection groups nor modify their priority values, you can manipulate their processing order in a different way. If you need to define a priority order that is different than the default design, you can create custom rule collection groups with your wanted priority values. In this scenario, you don't use the default rule collection groups at all and use only the ones you create to customize the processing logic.  

Rule collection groups contain one or multiple rule collections, which can be of type DNAT, network, or application. For example, you can group rules belonging to the same workloads or a VNet in a rule collection group. 

Rule collection groups have a maximum size of 2 MB. If you need more than 2 MB, you can split the rules into multiple rule collection groups. A Firewall Policy can contain 50 rule collection groups.


## Rule collections

A rule collection belongs to a rule collection group, and it contains one or multiple rules. They're the second unit processed by the firewall and they follow a priority order based on values. Rule collections must have a defined action (allow or deny) and a priority value. The defined action applies to all the rules within the rule collection. The priority value determines order the rule collections are processed.
  
There are three types of rule collections:

- DNAT
- Network
- Application

Rule collection types must match their parent rule collection group category. For example, a DNAT rule collection can only be part of a DNAT rule collection group.

## Rules

A rule belongs to a rule collection, and it specifies which traffic is allowed or denied in your network. They're the third unit to be processed by the firewall and they don't follow a priority order based on values. The processing logic for rules follows a top-down approach. All traffic that passes through the firewall is evaluated by the defined rules for an allow or deny match. If there's no rule that allows the traffic, then the traffic is denied by default.

For application rules, the traffic is processed by our built-in [infrastructure rule collection](infrastructure-fqdns.md) before it's denied by default.

There are three types of rules:

- DNAT
- Network
- Application

### DNAT rules

DNAT rules allow or deny inbound traffic through the firewall public IP address(es). 
You can use a DNAT rule when you want a public IP address to be translated into a private IP address. The Azure Firewall public IP addresses can be used to listen to inbound traffic from the Internet, filter the traffic and translate this traffic to internal resources in Azure.

### Network rules

Network rules allow or deny inbound, outbound, and east-west traffic based on the network layer (L3) and transport layer (L4).  
You can use a network rule when you want to filter traffic based on IP addresses, any ports, and any protocols.


### Application rules

Application rules allow or deny outbound and east-west traffic based on the application layer (L7). 
You can use an application rule when you want to filter traffic based on fully qualified domain names (FQDNs), URLs, and HTTP/HTTPS protocols. 


## Next steps

- Learn more about Azure Firewall rule processing: [Configure Azure Firewall rules](rule-processing.md).
