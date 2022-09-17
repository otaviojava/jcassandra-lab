# Cassandra installation

In the previous chapters, we discussed the concepts of non-relational databases, their comparisons with the relational ones, and we dissected the internal workings of Cassandra.

In this chapter, we will have a more practical view: we will show the installation process, configuration, how to create Cassandra instances inside a container with Docker, as well as how to create a cluster simply with docker-compose.

## Downloading Cassandra

Before starting the installation, it is important to talk about Cassandra's prerequisites. As it is a database made in Java, for installation, you must have installed a Java 8 implementation (OpenJDK, Azul, Oracle HotSpot, etc.).

In this first installation moment, no other client will be used besides `cqlsh`, Cassandra's native communicator, so it is necessary that the computer also has the latest version of Python 2.7. `cqlsh` is a communication bridge with the database that allows interaction with an instance via Shell lines through CQL, the Cassandra Query Language.


* Download Cassandra from the project website: http://cassandra.apache.org/download/

* Unzip the file, which will have a name similar to `tar -xvf apache-cassandra-VERSION-bin.tar.gz`

* With the files unzipped, the next step is to enter the `bin` folder and start Apache Cassandra. To do this, run the command `sh cassandra -f`.

Once the database instance is up, the next step will be to test communication with it. For this, the client mentioned above, will be used. Thus, to execute it, it is necessary to run the `./cqlsh` command inside the `bin` folder.

```bash
Connected to Test Cluster at 127.0.0.1:9042.
[cqlsh 5.0.1 | Cassandra 3.11.3 | CQL spec 3.4.4 | Native protocol v4]
Use HELP for help.
cqlsh> SHOW VERSION
[cqlsh 5.0.1 | Cassandra 3.11.3 | CQL spec 3.4.4 | Native protocol v4]
cqlsh>
```

## Simplifying installation with containers


One way to install Cassandra is through a container with Docker. In a general view, a container is an isolated environment and Docker technology uses the linux kernel and resources, for example, Cgroups and namespaces, to segregate processes, so that they can be executed independently.

The purpose of containers is to create such independence: the ability to run multiple processes and applications in isolation, make better use of the infrastructure, maintain security between the containers executed, in addition to the ease of creation and maintenance.

Once Docker is installed (https://docs.docker.com/install/), run the following command on the console:

```bash
docker run -d --name casandra-instance -p 9042:9042 cassandra
```

This command downloads and runs[ https://store.docker.com/images/cassandra](https://store.docker.com/images/cassandra), Cassandra's official image, directly from the *docker hub*.

To run `cqlsh` inside Docker:

* List the containers running on the machine with the `docker ps` command

```bash
$ docker ps
CONTAINER ID IMAGE
7373093f921a cassandra
```

* Each container created has a unique identifier or ID. The purpose of the previous command was to list the existing containers and their respective Ids. Once you have found the Cassandra container ID,  run the command for `docker exec -it CONTAINER_ID cqlsh`.

```bash
$ docker exec -it 7373093f921a cqlsh
Connected to Test Cluster at 127.0.0.1:9042.
[cqlsh 5.0.1 | Cassandra 3.11.3 | CQL spec 3.4.4 | Native protocol v4] Use HELP for help.
cqlsh> SHOW VERSION
[cqlsh 5.0.1 | Cassandra 3.11.3 | CQL spec 3.4.4 | Native protocol v4]
```

By default in Docker, all files are created inside the container. Thus, to extract the volume of data out of the container, it is necessary to map the `/var/lib/cassandra` path, for example:

```bash
docker run --name some-cassandra -p 9042: 9042 -v /my/own/datadir:/var/lib/cassandra -d cassandra
```

