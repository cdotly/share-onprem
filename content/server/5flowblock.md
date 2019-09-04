---
title: "Running Flowblock"
date: 2019-08-09T13:32:11-05:00
draft: false
weight: 150
---
The simplest way to run flowblock is by invoking docker directly:

```
$ docker run -e <ENV_VAR1>=<value> -p 8400:8400 -p 8401:8401 <flowblock_image>:<tag>
```

The following environment variables must be set (eg. using the `-e` option to docker):

**Variable**|**Description**
:-----:|:-----:
FLOWBLOCK\_OBJECT\_STORE\_BASE\_URL|The base URL of the S3-compatible API.
FLOWBLOCK\_OBJECT\_STORE\_ACCESS\_KEY|The access key to use when accessing the S3 API.
FLOWBLOCK\_OBJECT\_STORE\_SECRET\_KEY|The secret key to use when accessing the S3 API.
FLOWBLOCK\_OBJECT\_STORE\_SECURE|Whether or not the S3 API endpoint uses TLS.
FLOWBLOCK\_OBJECT\_STORE\_BLOCK\_BUCKET\_NAME|Name of the S3 bucket to store flowblock objects in.
FLOWBLOCK\_OBJECT\_STORE\_BLOCK\_BUCKET\_REGION|S3 region to use.
FLOWBLOCK\_AUTHTOKEN\_SIGN\_SK|Authtoken signing secret key, from keygen (see Generating Keys above).
FLOWBLOCK\_AUTHTOKEN\_VERIFY\_PKS|Authtoken signing public key.
FLOWBLOCK\_LOCAL\_STORAGE\_DIR|Path to local cache directory.
FLOWBLOCK\_DEPLOYMENT\_CIFS|Connection Information Files (CIFs) paths and contents

The following environment variables are optional:

**Variable**|**Description**
:-----:|:-----:
FLOWBLOCK\_DEBUG\_HTTP\_ADDRESS|`<hostname>:<port>` to bind debug HTTP listening socket. Default: 0.0.0.0:8402
FLOWBLOCK\_DEBUG\_HTTP\_HEALTHZ\_PATH|URL path (on the debug HTTP socket) to the "healthz" endpoint. This is a no-op and can be used for container liveness checks. Default: /healthz
FLOWBLOCK\_DEBUG\_HTTP\_METRICS\_PATH|URL path (on the debug HTTP socket) where Prometheus metrics will be exposed. Default: /metrics
FLOWBLOCK\_SERVICE\_HTTP\_ADDRESS|`<hostname>:<port>` to bind HTTP listening socket. Default: 0.0.0.0:8401

An alternative way to run flowblock is using an .list file with the variables listed. Create a file called `env-block.list` and  list the variables and your specific values like this (values listed are sample values, please replace with your own):

```
FLOWBLOCK_OBJECT_STORE_BASE_URL=https://sharetest.us-east-2.amazonaws.com
FLOWBLOCK_OBJECT_STORE_ACCESS_KEY=gPc+8EKpc0YS+VUPphS1CAXbZpc0YS+VUPphS1CAXbZOoJ
FLOWBLOCK_OBJECT_STORE_SECRET_KEY=SK37UETVSIWQSK37UETVSIWQ
FLOWBLOCK_OBJECT_STORE_SECURE=true
FLOWBLOCK_OBJECT_STORE_BLOCK_BUCKET_NAME=share-test
FLOWBLOCK_OBJECT_STORE_BLOCK_BUCKET_REGION=us-east-2
FLOWBLOCK_AUTHTOKEN_SIGN_SK=injUfjaBgrS5wsWxlasjdprinjUfjaBgrS5wsWxlasjdpr
FLOWBLOCK_AUTHTOKEN_VERIFY_PKS=AfoAACJhdXRodG9rZW4uQXV0aGVudGljYXRpb25TZXJ2aWNlS2V5AQBDPgMEr4TBF9iov6f-Fbx21cYJtp0PK4ZhH5y88gD6buMRlpozPolkX6F5fLu4vjQo9MywQklHcFpJHmFsXRxT4sk9-AIASD4FMEQCIHDr-AfoAACJhdXRodGXVljYXRpb25TZXJ2aWNlS2V5AQBDPgMEr4TBF9iov6f-Fbx21cYJtp0PK4ZhH5yPolkX6F5fLu4vjQo9MywQklHcFpJHmFsXRxT4sk9-AIASD4FMEQCIHDr
FLOWBLOCK_LOCAL_STORAGE_DIR=/block_local_storage
FLOWBLOCK_DEPLOYMENT_CIF_HASH_PATH=/b4084b2a72985a1004ae3be85739597b4084b2a72985a1004ae3be85739597
FLOWBLOCK_DEPLOYMENT_CIF={"blockAddr":"http://flow-block.testingcif.com","storeAddr":"http://flow-store.testingcif.com"}
```

When running the command with a .list file, omit the `-e <ENV_VAR1>=<value>` portion of the command and instead run a command like this:

```
docker run -p 8400:8400 -p 8401:8401 registry.spideroak.com/share-onprem/flowblock:latest --env-file=/path/to/env-block.list/
```


