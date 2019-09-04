---
title: "Generating Keys"
date: 2019-08-09T13:28:06-05:00
draft: false
weight: 130
# menu:
#   server:
#     # parent: 'extras'
#     weight: 130
---
Flow uses cryptographic tokens to verify requests to the API. In order to run the flow application servers, you must generate a keypair and provide it to the servers via environment variables. This section describes how to generate the keypair, and save it to a Kubernetes Secret.

```
$ docker run —rm -it -v $PWD/keyout:/keyout registry.spideroak.com/share-onprem/flowkeygen:latest /keyout1
```

This will create a directory called `keyout` in your current working directory, and output three files:

```
$ ls keyout
public_0.key public_pins.key secret_0.key
```

