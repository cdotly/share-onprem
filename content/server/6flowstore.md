---
title: "Running Flowstore"
date: 2019-08-09T13:37:30-05:00
draft: false
weight: 160
---

The simplest way to run flowstore is by invoking docker directly:

```
$ docker run -e <ENV_VAR1>=<value> -p 8500:8500 -p 8501:8501 registry.spideroak.com/share-onprem/flowstore:latest
```

The following environment variables must be set (eg. using the `-e` option to docker):

**Variable**|**Description**
:-----:|:-----:
FLOWSTORE\_OBJECT\_STORE\_SECURE|Whether or not the S3 API endpoint uses TLS.
FLOWSTORE\_OBJECT\_STORE\_SECRET\_KEY|The secret key to use when accessing the S3 API.
FLOWSTORE\_OBJECT\_STORE\_BLOCK\_BUCKET\_REGION|S3 region to use.
FLOWSTORE\_OBJECT\_STORE\_BLOCK\_BUCKET\_NAME|Name of the S3 bucket to store flowblock objects in.
FLOWSTORE\_OBJECT\_STORE\_BASE\_URL|The base URL of the S3-compatible API.
FLOWSTORE\_OBJECT\_STORE\_ACCESS\_KEY|The access key to use when accessing the S3 API.
FLOWSTORE\_AUTHTOKEN\_VERIFY\_PKS|Authtoken signing public key, from keygen (see Generating Keys above).

The following environment variables are optional:

**Variable**|**Description**
:-----:|:-----:
FLOWSTORE\_SERVICE\_GRPC\_ADDRESS|`<hostname>:<port>` to bind gRPC listening socket. Default: 0.0.0.0:8500
FLOWSTORE\_SERVICE\_HTTP\_ADDRESS|`<hostname>:<port>` to bind HTTP listening socket. Default: 0.0.0.0:8501
FLOWSTORE\_DEBUG\_HTTP\_ADDRESS|`<hostname>:<port>` to bind debug HTTP listening socket. Default: 0.0.0.0:8502
FLOWSTORE\_DEBUG\_HTTP\_HEALTHZ\_PATH|URL path (on the debug HTTP socket) to the "healthz" endpoint. This is a no-op and can be used for container liveness checks. Default: /healthz
FLOWSTORE\_DEBUG\_HTTP\_METRICS\_PATH|URL path (on the debug HTTP socket) where Prometheus metrics will be exposed. Default: /metrics

An alternative way to run Flowstore is using a .list file with the variables listed. Create a file called `env-store.list` and list the variables and your specific values like this (values listed are sample values, please replace with your own):

```
FLOWSTORE_OBJECT_STORE_BASE_URL=https://sharetest.us-east-2.amazonaws.com
FLOWBLOCK_OBJECT_STORE_ACCESS_KEY=gPc+8EKpc0YS+VUPphS1CAXbZpc0YS+VUPphS1CAXbZOoJ
FLOWBLOCK_OBJECT_STORE_SECRET_KEY=SK37UETVSIWQSK37UETVSIWQ
FLOWBLOCK_OBJECT_STORE_SECURE=true
FLOWBLOCK_OBJECT_STORE_BLOCK_BUCKET_NAME=share-test
FLOWSTORE_OBJECT_STORE_BLOCK_BUCKET_REGION=us-east-2
FLOWBLOCK_AUTHTOKEN_VERIFY_PKS=AfoAACJhdXRodG9rZW4uQXV0aGVudGljYXRpb25TZXJ2aWNlS2V5AQBDPgMEr4TBF9iov6f-Fbx21cYJtp0PK4ZhH5y88gD6buMRlpozPolkX6F5fLu4vjQo9MywQklHcFpJHmFsXRxT4sk9-AIASD4FMEQCIHDr-AfoAACJhdXRodGXVljYXRpb25TZXJ2aWNlS2V5AQBDPgMEr4TBF9iov6f-Fbx21cYJtp0PK4ZhH5yPolkX6F5fLu4vjQo9MywQklHcFpJHmFsXRxT4sk9-AIASD4FMEQCIHDr
```

When running the command with a .list file, omit the `-e <ENV_VAR1>=<value>` portion of the command and instead run a command like this:

```
docker run -p 8400:8400 -p 8401:8401 registry.spideroak.com/share-onprem/flowstore:latest --env-file=/path/to/env-store.list/
```
