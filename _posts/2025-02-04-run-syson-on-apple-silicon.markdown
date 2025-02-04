---
layout:     post
author:     Juande Santander-Vela
title:     "How to run SysON for personal testing on an Apple Silicon Mac"
categories: macOS "Apple Silicon" docker SysML "Systems Engineering"
---

As Systems Engineer (not the IT type, but the [real engineering one](https://en.wikipedia.org/wiki/Systems_Engineering)), I need to reference many different types of models, but the most valuable ones are what enable [Model-Based Systems Engineering](https://en.wikipedia.org/wiki/Model-based_systems_engineering) (MBSE).

An already established standars for models is [SysML](https://en.wikipedia.org/wiki/Systems_modeling_language), which currently is in the process of being standardised on version 2.

One of the emerging tools for SysML is [SysON](https://mbse-syson.org), which is open-source, and can be simply run with a Docker command (see [their instructions](https://doc.mbse-syson.org/syson/v2024.11.0/installation-guide/how-tos/install/local_test.html))... but only on x86_64 machines.

I have created an issue on their GitHub repository, but while it gets fixed, I tried the following work around.

First, let's run a Docker-based Postgres database mapping the normal Postgres port (5432) to 5430, and making sure it is available through 127.0.0.1:

```bash
docker run -p 127.0.0.1:5430:5432 --name syson-postgres \
                                  -e POSTGRES_USER=dbuser \
                                  -e POSTGRES_PASSWORD=dbpwd \
                                  -e POSTGRES_DB=syson-db \
                                  -d postgres
```

Notice the usage of `5430` next to `127.0.0.1`. This is key for the proper running of the next command.

Once we have Postgres running, we need to run the SysOM Jar file:

```bash
java -jar ./syson-application-2025.1.0.jar \
     --spring.datasource.url=jdbc:postgresql://127.0.0.1:5430/syson-db \
     --spring.datasource.username=dbuser \
     --spring.datasource.password=dbpwd
```

How do we know which Jar file to download? We follow the instructions on the [How to install SysON ecosystem only?](https://doc.mbse-syson.org/syson/v2024.11.0/installation-guide/how-tos/install/ecosystem_only.html) page, and then the [Installing SysON Manually](https://doc.mbse-syson.org/syson/v2024.9.0/installation-guide/how-tos/install.html#download) instructions, to make sure that we download a stable version of `org.eclipse.syson.syson-application-YYYY.M.0.jar`.

Please note that:

 * We use `127.0.0.1` explicitly, and not `localhost`.
 * We use `5430` for the port in the `spring.datasource.url` key, as we mapped in the `docker run` command.
 * The end of the `spring.datasource.url` corresponds to the `POSTGRES_DB` key after the `IP:PORT/` part.
 * The `spring.datasource.username` key must match the `POSTGRES_USER` key in the `docker run` command.
 * The `spring.datasource.password` key must match the `POSTGRES_PASSWORD` key in the `docker run` command.

Please also note that the instructions on the _How to install SysON ecosystem only?_ page are slightly different. These instructions have been verified for consistency.
 
With the caveats above, it should be possible now to point your browser (preferably Firefox; Safari has problems) to `127.0.0.1:8080` and start using SysON.

# Using Docker on Apple Silicon

For your docker needs, specially on Apple Silicon, I suggest you forget about the official Docker Desktop application, and instead use Colima.

You can start Colima simply with

```bash
colima start
```

And the docker environment will be preserved until you do

```bash
colima stop
```
