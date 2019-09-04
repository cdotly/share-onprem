---
title: "Connection Information Files"
date: 2019-08-09T13:29:28-05:00
draft: false
weight: 140
---

Flowblock needs to serve its Connection Information File (CIF). This file is a JSON that contains the URLs used for the block and store services. End users need the link to the CIF file in order to connect to this particular flow server. 

In order to generate the CIF configuration in flowblock, two tools must be used, `flowcif` and `flowmergecifs`.

The first step is to create the directory ~/out/:

```
mkdir out
```

Next, use flowcif to create a CIF file:

```
docker run -v $(pwd)/out:/out registry.spideroak.com/share-onprem/flowcif:latest  -type legacy -version 0 -out-dir=/out/cif1.out "blockAddr=http://flow-block.testingcif.com" "storeAddr=http://flow-store.testingcif.com"
```

Please note that the URLs for `blockAddr` and `storeAddr` must match the address of the server running Flowblock and Flowstore, respectively. 

The output of flowcif is stored in the directory ~/out/cif1.out/. It is a single file. Copy the name of the file in the ~/out/cif1.out/ directory, which will be used in the next command:

```
docker run -v $(pwd)/out:/out registry.spideroak.com/share-onprem/flowmergecifs:latest --out-dir=/out /out/cif1.out/920f1725ab1158732a6e0047f3e4d7825dc31dee62e41d9ec0587a3d9ae454d1
```

The merged CIF information will output to the file `~/out/cifs.out`. The contents of the file should be added to the configuration files used in Flowblock and Flowstore as described below.

Users that want to create an account in this deployment will need to enter the CIF URL as part of onboarding. CIF URLs follow this format: `<blockAddr in the CIF>/<hash>`. The hash is the filename generated after running the Flowcif command. An example URL would look like this: `https://flow-block.cloud.spideroak.com/5ee7950c9f962d4cf33f095da9267f4f6d87e6b153cef203fd3000528bbdcf85`.

Please note that IP addresses are not acceptable for use in CIF URLs. End users will not be able to correctly connect the Share application to the server. A domain name is necessary. 