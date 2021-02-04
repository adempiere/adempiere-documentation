---
description: Describes the steps to install ADempiere with Docker.
---

# Install ADempiere easily with Docker

## Install Docker for your operating system

To install Docker on MacOS see [https://docs.docker.com/docker-for-mac/install/](https://docs.docker.com/docker-for-mac/install/)

To Install Docker on Window see [https://docs.docker.com/docker-for-windows/install/](https://docs.docker.com/docker-for-windows/install/)

To Install Docker on Debian Linux see [https://docs.docker.com/engine/install/debian/](https://docs.docker.com/engine/install/debian/)

Verify that docker is installed :

```bash
docker --version
Docker version 20.10.2, build 2291f61
```

## Install Docker Compose for your operating system

To install Docker [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)

```bash
docker-compose --version
docker-compose version 1.27.4, build 40524192
```

## Install git for your operating system

to Install git see [https://git-scm.com/book/en/v2/Getting-Started-Installing-Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

```text
git --version
git version 2.24.3 (Apple Git-128)
```

## Clone the ADempiere Docker Repository

```bash
git clone https://github.com/adempiere/adempiere-docker.git
```

## Setup ADempiere Docker Install

Open a shell command terminal and run the following statements:

Edit and modify the default settings for the PostgreSQL database 

```bash
cd adempiere-docker
cat .env
#  Copyright (C) 2010-2017, OpenUp S.A. , http://www.openup.com.uy
#  Copyright (C) 2003-2017, e-Evolution Consultants S.A. , http://www.e-evolution.com
#  This program is free software: you can redistribute it and/or modify
#  it under the terms of the GNU General Public License as published by
#  the Free Software Foundation, either version 3 of the License, or
#  (at your option) any later version.
#  This program is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
#  You should have received a copy of the GNU General Public License
#  along with this program.  If not, see <http://www.gnu.org/licenses/>.
#  Email: raul.capecce@openupsolutions.com, http://openupsolutions.com , http://github.com/rcapecce
#  Email: victor.perez@e-evolution.com, http://www.e-evolution.com , http://github.com/e-Evolution
ADEMPIERE_DB_PORT=55432
ADEMPIERE_DB_PASSWORD=adempiere
ADEMPIERE_DB_ADMIN_PASSWORD=postgres
PG_VERSION=12.2
vi .env
```

Edit and modify the default setting for the ADempiere

```bash
cd adempiere
cat .env
#  Copyright (C) 2003-2017, e-Evolution Consultants S.A. , http://www.e-evolution.com
#  This program is free software: you can redistribute it and/or modify
#  it under the terms of the GNU General Public License as published by
#  the Free Software Foundation, either version 3 of the License, or
#  (at your option) any later version.
#  This program is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
#  You should have received a copy of the GNU General Public License
#  along with this program.  If not, see <http://www.gnu.org/licenses/>.ce
#  Email: victor.perez@e-evolution.com, http://www.e-evolution.com , http://github.com/e-Evolution
ADEMPIERE_WEB_PORT=8274
ADEMPIERE_SSL_PORT=4444
ADEMPIERE_VERSION=3.9.3
# ATENTION If is "Y" it will be replace de actual defined database with a empty ADempiere seed
ADEMPIERE_DB_INIT=Y
vi .env
```

Deployment ADempiere using the application shell script

```bash
cd ..
pwd 
# From the adempiere-docker directory execute
./application.sh adempiere up -d --build
# Wait a few minutes while the ADempiere Server installation is done 
docker ps |grep postgres
# The output should show something like 
e70086fe9f89   dd4fa36a9c2f             "docker-entrypoint.s…"   11 months ago       Up 4 minutes       0.0.0.0:55432->5432/tcp                          postgres122_db_1
docker ps |grep adempiere
# The output should show something like 
fe8cc0a49e77   adempiere                "/bin/sh -c '/root/s…"   11 months ago       Up 8 minutes       0.0.0.0:4444->4444/tcp, 0.0.0.0:8274->8888/tcp   adempiere
docker logs adempiere
```

Based on the configuration of ./adempiere/.env, docker will show the available ports where the ADempiere services were deployed 0.0.0.0:4444-&gt;4444/tcp, 0.0.0.0:8274-&gt;8888/tcp

If everything goes well up to here, open the following url [http://0.0.0.0:8274/webui/](http://0.0.0.0:8274/webui/) in the browser of your choice

![](../../.gitbook/assets/image%20%2814%29.png)

To access use the username and password GardenAdmin

![ADempiere Role](../../.gitbook/assets/image%20%2810%29.png)

Congratulations now you can evaluate and try adempiere locally

![ADempiere Main Screen](../../.gitbook/assets/image%20%2811%29.png)

{% hint style="danger" %}
The deployment in Docker is done for didactic purposes, for a production installation requires specific adjustments in the database and memory parameters
{% endhint %}

## See Also

[Github ADempiere Docker Repository](https://github.com/adempiere/adempiere-docker/blob/master/README.md)

