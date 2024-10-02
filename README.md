# General

[Course](https://web.dio.me/course/introducao-ao-mongodb-e-bancos-de-dados-nosql/learning/d8c1eb33-27f5-44f9-a57c-68d65fcac8da?back=/track/coding-the-future-claro-java-spring-boot&tab=undefined&moduleId=undefinedhttps://web.dio.me/course/introducao-ao-mongodb-e-bancos-de-dados-nosql/learning/d8c1eb33-27f5-44f9-a57c-68d65fcac8da?back=/track/coding-the-future-claro-java-spring-boot&tab=undefined&moduleId=undefined)


## Introducton - needs

Needs foor NoSQL:

- Some specialists say that the "we" double the volume of data stored every year;
- "We" develop more and more apps with a non conventional behaviour;
- "We" have a demand for scalable applications.

The deficiencies of SQL databases make born the NoSQL databases.


## Differences between SQL and NoSQL

### Scalability

- In SQL databases is more related to a vertical scalability and NoSQL to a horizontal scalability (although obviousy NoSQL can also gain the benefits of vertical scalablity). There are cases of relational databases that have horizontal scalability also, like MySQL cluster, but this databases are related to data reading. The data sharing between replicas in a NoSQL scenario is named "`sharding`".

As in a NoSQL world is more easy to deal with the question of the horizontal scalability, you can interact better with a non constant request level, as you can scale horizontally more easy.

### Schemas or structure

- In a SQL world you need a rigid definition of tables and other things like relations and in a NoSQL world you almost no need to pre define a structure;

### Use of SQL or no

- In the relational databases world SQL is the language used and in the NoSQL world, SQL is not used (or not used often).

### Performance

- As SQL databases is more frequent related to vertical scalability, the permormance is often increased by upgrading the hardware, like disks, bur in the case of NoSQL databases, as they are often linked to a horizonal scalability, the often receives a performance increase by the things like the size of the cluster and the performance of the network of the cluster.

### Transactions

Please see the next image:
![transactions](images/differences-sql-nosql-transactions.png)

In general the NoSQL databases do not have the concept of `"transaction"` except for MongoDB. They do not use "`transactions`" to increase high availability and performance.

### Advantages of NoSQL

- Flexibility;
- Scalability;
- High performance.

## Types of NoSQL databases

The thing that is common between the several types of NoSQL databases is that they do not use SQL (in most part of the time, they do not depends on SQL).
We have this image about a ranking of a use of databases:

![ranking of databases](images/ranking-of-databases.png)

The types of NoSQL databases:

![types of NoSQL databases](images/types-of-nosql-databases.png)

Some comments:

- Document store: common, can store documents like JSON or XML;
- Key value: often used for cache;
- Oriented to columns: more next to relational databases;
- Graphs: used on social networks, games, filesystems or fraud detection as example

## NoSQL databases - graphs

Please initially see this image:

![graphs general overview](images/graphs-general-overview.png)

Basically this type of database contains `nodes` and `vertices`. `Nodes` are the data and `vertices` are the relations.

Ranking of databases oriented to graphs most used:
![ranking of databases oriented to graphs most used](images/ranking-of-databases-oriented-to-graphs-most-used.png)

About Neo4j:
- Uses the language "cypher";
- Apply the ACID (atomicity, consistency, isolation, durability) properties;
- Is the leader in the previous image :).

In the class we used [this sandbox](https://sandbox.neo4j.com/) of Neo4j.

We created a balnk database and in this blank database we could create a registry using the next command:

```
create (:Client {name: "Bob Esponja", age: 28, hobbiees:["Caçar água-viva", "comer hamburguer"]})
```

The output was "`Added 1 label, created 1 node, set 3 properties, completed after 75 ms.`".

I also inserted another node with this command:

```
create (:Car {windows: 4, color: "red"})
```

The output was "`Added 1 label, created 1 node, set 2 properties, completed after 14 ms.`".

We can consult all nodes using the next command as example. I used "banana" to demonstrate that this variable name do not matter:

```
match(banana) return (banana)
```

The output of the above command was:

![example of a consulting in Neo4j](images/example-consulting-neo4j.png)

You can saw that we can consult all the documents without type a paramenter related to a thing like a table.

With the next command we can create two nodes and a relationship:

```
create (:Client {name: "Lula Molusco", age: 50}) - [:Bloqueado] -> (:Client{name: "Patrick", hooblies : ["caçar água viva"]})
```

The return of the previous command:

```
Added 2 labels, created 2 nodes, set 4 properties, created 1 relationship, completed after 15 ms.
```

We resulted in this image after inserting more data

![neo4j new graphical representation](images/neo4j-new-graphical-representation.png)

We can also insert an empty object this way:

```
create(:object)
```

An the graph will be now:

![graph 3 in Neo4j](images/graph-3-neo4j.png)

Different colors? Yes, because they have different labels (teacher said about properties, but I saw that different labes result in different colors as you can see comparing all images).

With this script we can create a new "Bloqueado" relation:

```
match(lula:Client{name: "Lula Molusco"}), (patrick: Client {name: "Patrick"}) create (lula) -[:Bloqueado] -> (patrick)
```

Explanation: we was getting two datas with the label "client" related to the parameters to filter (example "{name: "Lula Molusco"}) and this returned data was saved in variables ("lula" and "patrick"). After the dash signal ("-") with this two variables we created a "Bloqueado" relation.

The resulted graph was:
![graph 4 in Neo4j](images/graph-4-neo4j.png)

Deleting the 2 relationships "Bloqueado" of the above image:

```
match(lula:Client {name: "Lula Molusco"}) - [relacionamento: Bloqueado] - () delete relacionamento
```

As you can see, the script have a similar format. The result graph now is:
![Graph 5 in Noe4j](images/graph-5-new4j.png)

Deleting a node (not a relation):

```
match(lula: Client {name: "Lula Molusco"}) delete lula
```

To enforce the idea of the general format of the commands, see how we consult the "patrick" client:

```
match(patrick: Client {name: "Patrick"}) return patrick
```

This way you can insert a new property in a node or update its value:

```
match(patrick: Client {name: "Patrick"}) set patrick.age = 44
```

The **`relatioships`** and `nodes` can have `properties`.

You can insert a new `label` in a `node` this way:

```
match(patrick:Client {name: "Patrick"}) set patrick: marinho
```

You can see the result in this image. I added 2 new labels:

![new-labels-neo4j](images/new-labels-neo4j.png)

Talking about columns and columnfamilies:

![column, columnfamily](images/column-columnfamily.png)

In a non relational world we have fo every column:

- key
- values
- timestamp

Ranking of databases based on columns or columnfamily:

![ranking databases based on columns](images/ranking-databases-based-columns.png)

Terminology related to a NoSQL databases:

![terminology nosql](images/terminology-nosql.png)

Talking about NoSQL databases (I not talking that this cannot be applied to other scenarios), you have to make your colsuts bases on columns that have `indexes`, like the `row key`.

## Examples of CQL

Some clausules of CQL:

![example-1-cql](images/cql-demo-1.png)

Other clausules. One thing that the teacher talked this time was about the fact of the column age be null in case of Patrick (non exists, was not inserted):

![example-2-cql](images/cql-demo-2.png)

Other clausules. The clausules are very similar to `SQL-92` clausules:

![example-3-cql](images/cql-demo-3.png)

Other clausules. Cassandra seems more next to relational databases than DynamoDB. When I used DynamoDB I am not inserted a column. I inserted the information directly in the JSON of the registry. But see if a registry does not have a information in a column, if I did a where based on this column, the information is not stored (null), see in the next image:

![example-4-cql](images/cql-demo-4.png)

# Key-value

![key value](images/key-value.png)

In a key-value database the data to be stored can be simple or complex.

- Good performance;
- Less capacity of searches.
- Cassandra (comlums, columnfamily) was based on DynamoDB (key-value);
- Uses: cache, user sessions, carts (next to cassandra uses).

![ranking key value databases](images/ranking-key-value-databases.png)

Main characteristics of `Redis`:

![main characteristics of Redis](images/redis-main-characteristics.png)

In Redis there is a key-value storage without a schema. There is no a thing like a table.

[This site](https://onecompiler.com/redis) as [the link used in the course](http://try.redis.io) is unavailable don't work for make tests on a `Redis` server. So I have to install `Redis` locally, but it was very easy. In a "happy path". you will need only:

```
# apt update
sudo apt update

# install
sudo apt install redis-server -y

# configuring
# In /etc/redis/redis.conf find the line starting with "supervised" to "supervised systemd" (without quotes)

# start
sudo systemctl restart redis.server

# checking installation
sudo systemctl status redis.server
# Ideally you will see "active (running)" in green

# accessing shell
redis-cli
```

I followed the tutorial of [this link](https://linuxhint.com/install_redis_linux_mint/). I installed in Linux Mint 20.

Some tests of Redis using `redis-cli`:

```
# It was possible to save a value this way. See, without equals sign
set user "Andre"

# or this way, also without equals sign
set user:name "Andre"

# we can store a JSON
set user "{'name': 'Andre', 'age': 42}

# to retrieve a value we only need a
# get key
# Examples
get user
get user.name

# But at least for now, if I store a JSON, I could not use the commands 'set'/'get'. It was needed to use the commands 'hmset'/'hmget'. Examples:
# Is a little obvious the structure of the command
# hmset group_key specifc_key1 value1 specific_value2 value2
hmset person name "andre" age 42

# Then you can retrive the value using the command hmget. Example:
hmget person name

# But remember, you can't access the entire group of information. The next command WILL NOT WORK:
hmget person
```