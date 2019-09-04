---
title: "HTTPS Reverse Proxy"
date: 2019-08-09T13:42:53-05:00
draft: false
weight: 170
---

The Share client application is configured to connect to flowblock and flowstore over HTTPS, at the address/port combinations you provide. It is possible to run the services on separate IP addresses, or both services on the same IP address (and same DNS domain name) on different ports. Either way, you must provide TLS termination by way of a reverse proxy.