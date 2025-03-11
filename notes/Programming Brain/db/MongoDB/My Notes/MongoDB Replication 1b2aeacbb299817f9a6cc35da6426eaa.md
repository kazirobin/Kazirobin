# MongoDB Replication

In MongoDB, **replication** is the process of synchronizing data across multiple servers. This ensures data availability and redundancy, which improves fault tolerance and disaster recovery. The primary mechanism used for replication in MongoDB is called a **replica set**.

## R**eplica set** Consists

- **Primary node**: Handles all the read and write operations.
- **Secondary nodes**: Synchronize the data from the primary node and can be used for read operations (depending on the configuration). If the primary node fails, one of the secondaries is automatically elected to become the new primary.
- **Arbiter** (optional): A node that doesn't store data but participates in elections to help break ties during the selection of a new primary.

## Benefits of Replication

- **High Availability**: If the primary node fails, a secondary node takes over without downtime.
- **Data Redundancy**: Data is replicated on multiple servers, reducing the chance of data loss.
- **Read Scalability**: Reads can be distributed among secondary nodes (if configured for read operations).

## How it works

- The primary node logs all changes to the **oplog** (operation log).
- Secondary nodes constantly replicate the oplog to stay in sync with the primary.
- If the primary becomes unavailable, an election is held among the secondaries to determine the new primary.

## Setting up **MongoDB Replication**

Add the `replication` section to the `mongod.conf` file path looks like this:
`Window > C:\Program Files\MongoDB\Server\4.4\bin\mongod.conf`
`Linux > /etc/mongod.conf`
`Mac > /usr/local/etc/mongod.conf`

You can set the any name of the replication set in the `replSetName` key. In this case, I have set the name `replocal`.

```jsx
replication:
  replSetName: replocal
```

Restart the MongoDB server to apply the changes.

For Windows, you can restart the MongoDB service from the `Task manager`. Go to the `Services` tab and `restart` the `MongoDB service`.

For Linux, you can restart the MongoDB service using the following command:

```bash
sudo service mongod restart
```

For Mac, you can restart the MongoDB service using the following command:

```bash
brew services restart mongodb
```

## Set Up Hosts

To set up a MongoDB replica set, you need at least 3 hosts. These can be physical or virtual machines or even containers. For testing, you can set up multiple MongoDB instances on the same machine by using different ports.

## Start MongoDB Instances

To start each MongoDB instance as part of a replica set, you'll need to configure it with the `--replSet` option. This is how you start MongoDB on three different instances.

`—dbpath` is the path where you have stored the MongoDB data files. In this case, I have stored the data files in the `C:/data/db` directory.

For Linux you can use this `--dbpath`:

```bash
/var/lib/mongodb
```

For Mac you can use this `--dbpath`:

```bash
/usr/local/var/mongodb
```

Create Three directories after the path like `/db/mongo1`

```bash
# Start Primary (on port 27017)
mongod --port 27017 --dbpath "C:/data/db/mongo1" --replSet replocal --bind_ip localhost

# Start Secondary 1 (on port 27018)
mongod --port 27018 --dbpath "C:/data/db/mongo2" --replSet replocal --bind_ip localhost

# Start Secondary 2 (on port 27019)
mongod --port 27019 --dbpath "C:/data/db/mongo3" --replSet replocal --bind_ip localhost
```

Here, all three nodes are on the same machine (`localhost`), but they are running on different ports (`27017`, `27018`, `27019`).

## Initialize The Replica Set

Now, you need to initialize the replica set. First, connect to the **primary** instance (on port 27017) using the MongoDB shell:

```bash
mongosh --port 27017
```

Once connected, use the following command to initiate the replica set:

```bash
rs.initiate()
```

This initializes the replica set with a default configuration. If you want to specify the configuration, you can pass in a configuration object like so:

```bash
rs.initiate({_id: "replocal", members: [{ _id: 0, host: "localhost:27017" }, { _id: 1, host: "localhost:27018" }, { _id: 2, host: "localhost:27019" }]})
```

## Reconfig The Replica Set

To **reconfigure a MongoDB replica set**, you'll need to follow a few steps carefully. Reconfiguring allows you to adjust various aspects of the replica set, such as adding/removing members, changing priorities, or modifying settings. Here's how to do it:

```bash
rs.reconfig({_id: "replocal", members: [{ _id: 0, host: "localhost:27017" }, { _id: 1, host: "localhost:27018" }, { _id: 2, host: "localhost:27019" }]}, { force: true })
```

### Notes:

- **Priority settings**: The higher the priority number, the more likely the member will be elected as primary. A member with a priority of `0` will never be elected as primary.
- **Reconfig from Secondary**: If you're running `rs.reconfig()` on a **secondary node**, you need to use `{force: true}` to avoid issues. It’s safer to always make changes from the primary node.
- **Minimal disruption**: Reconfiguring the replica set can cause the election of a new primary, leading to a brief period of unavailability while the new primary is chosen.

## Verify The Replica Set

After initiating, check the replica set status:

```bash
rs.status()
```

You should see a list of nodes with one as the primary and the others as secondaries. The output will indicate which node is the current primary.

## Add an Arbiter (Optional)

If you want to add an arbiter to help with elections but without data replication, you can add an arbiter like this:

```bash
rs.addArb("localhost:27020")
```

Make sure to start the arbiter with:

```bash
mongod --port 27020 --dbpath "C:/data/db/mongo4" --replSet replocal --bind_ip localhost --no-journal
```

## Configure Read and Write Preferences

By default, all writes go to the primary, and reads also go to the primary unless otherwise specified. To read from secondaries, you can configure the client driver or use:

```bash
db.getMongo().setReadPref("secondary")
```

## Replica Set Configuration Commands

Here are some **useful commands** for managing a MongoDB replica set, covering various tasks like adding/removing members, checking the status, and performing maintenance:

To view the current status of the replica set:

```bash
rs.status()
```

This command shows the health of all nodes, including which node is the primary and which are secondaries.

To see the current configuration of the replica set:

```bash
rs.conf()
```

This command prints out the current replica set configuration details, including members, priorities, and other settings.

To add a new member (e.g., a secondary node) to the replica set:

```bash
rs.add("hostname:port")
```

To remove a member from the replica set:

```bash
rs.remove("hostname:port")
```