---
layout: default
title: How does the Internet work?
parent: Web
grand_parent: Study
nav_order: 1
mathjax: true
mermaid: true
permalink: /docs/web/01
---

# How does the Internet work?
{: .no_toc }

<details markdown="block">
  <summary>
	Table of contents
  </summary>
{: .fs-3 .text-delta }
- TOC
{:toc}
</details>

---

> 참고: [How does the Internet work?](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/How_does_the_Internet_work)

- Objective: You will learn the basics of the technical infrastructure of the Web and the difference between Internet and Web

## A simple network

- When two computers need to communicate, you have to link them, either physically (usually with an Ethernet cable) or wirelessly (for example with Wi-Fi or Bluetooth systems)

<center markdown=block>
![internet-schema-1](/assets/web/images/01-internet-schema-1.png)
</center>

- Such a network is not limited to two computers. but it gets complicated quickly

<center markdown=block>
![internet-schema-2](/assets/web/images/01-internet-schema-2.png)
</center>

- To solve this problem, each computer on a network is connected to a special tiny computer called a router

- Router makes sure that a message sent from a given computer arrives at the right destination computer

<center markdown=block>
![internet-schema-3](/assets/web/images/01-internet-schema-3.png)
</center>

## A network of networks

- By connecting computers to routers, then routers to routers, we are able to scale infinitely

<center markdown=block>
![internet-schema-5](/assets/web/images/01internet-schema-5.png)
</center>

- It's not possible to set cables up between your house and the rest of the world

- There are already cables linked to your house, for example, electric power and telephone

- To connect our network to the telephone infrastructure, We need a special piece of equipment called a modem

- This modem turns the information from our network into information manageable by the telephone infrastructure and vice versa

<center markdown=block>
![internet-schema-6](/assets/web/images/01-internet-schema-6.png)
</center>

- The next step is to send the messages from our nework to the network we want to reach

- To do that, we will connect our network to an Internet Service Provider (ISP)

- An ISP is a company that manages some special routers that are all linked together and can also access other ISPs' routers

- The internet consists of this whole infrastructure of networks

<center markdown=block>
![internet-schema-7](/assets/web/images/01-internet-schema-7.png)
</center>

## Finding computers

- If you want to send a message to a computer, you have to specify which one.

- Thus any computer linked to a network has a unique address that identifies it, called an IP address (where IP stands for Internet Protocol)

- It's an address made of a series of four numbers separated by dots, for excample: 192.168.2.10

- We human beings have a hard time remembering that sort of address

- To make things easier, we can alias an IP address with a human readable name called a domain name

	- google.com is the domain name used on top of the IP address 142.250.207.78

- So using the domain name is the easiest way for us to reach a computer over the Internet

## Internet and the web

- The Internet is a technical infrastructure which allows billions of computers to be connected all together

- Among those computers, some computers (called Web servers) can send messages intelligible to web browsers

- The Internet is an infrastructure, whereas the Web is a service built on top of the infrastructure

- It is worth noting there are several other services on top of the Internet, such as email and IRC

## Intranets and Extranets

- Intranets are private networks that are restricted to members of a particular organization

- They are commonly used to provide a portal for members to securely access shared resources, collaborate and communicate

- Extranets are very similar to Intranets, except they open all or part of a private network to allow sharing and colloration with other organizations

- They are typically used to safely and securely share information with clients and stakeholders who work closely with a business

- Both intranets and extranets run on the same kind of infrastructure as the Internet, and used the same protocols

- They can therefore be accessed by authorized members from different physical locations

<center markdown=block>
![internet-schema-8](/assets/web/images/01-internet-schema-8.png)
</center>
