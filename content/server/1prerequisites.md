---
title: "Prerequisites"
date: 2019-08-09T13:22:47-05:00
draft: false
weight: 110
---


The following are required to run Share on-premise:

* A way to run Docker images.
* An S3-compatible object store, accessible to the flow containers. In future versions of Share, the client may also connect directly to the object store using [presigned requests](https://docs.aws.amazon.com/AmazonS3/latest/dev/PresignedUrlUploadObject.html) .
* A domain name or two, with valid TLS certificate(s).
* An HTTPS reverse proxy, terminating TLS.
