# Installation Instructions

## Database

### Step 01 - Adding the MongoDB Repository

MongoDB is already included in Ubuntu package repositories, but the official MongoDB repository provides most up-to-date version and is the recommended way of installing the software and also we use latest stable MongoDB version to test the system.

Import the key for the official MongoDB repository

```bash
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
```

Create a list file for MongoDB

```bash
echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
```

Update the packages list

```bash
sudo apt-get update
```

### Step 2 - Installing and Verifying MongoDB

Install the MongoDB package

```bash
sudo apt-get install -y mongodb-org
```

This command will install several packages containing latest stable version of MongoDB along with helpful management tools for the MongoDB server.

Create Unit file

In order to properly launch MongoDB as a service on Ubuntu 16.04, we additionally need to create a unit file describing the service. A unit file tells systemd how to manage a resource.

We'll create a unit file to manage the MongoDB service. Create a configuration file named **mongodb.service** in the **/etc/systemd/system_ directory** using **nano** or your favorite text editor.

```bash
sudo nano /etc/systemd/system/mongodb.service
```

Paste in the following contents, then save and close the file.

```
[Unit]
Description=High-performance, schema-free document-oriented database
After=network.target

[Service]
User=mongodb
ExecStart=/usr/bin/mongod --quiet --config /etc/mongod.conf

[Install]
WantedBy=multi-user.target
```

Next, Enable automatically starting MongoDB when the system starts.

```bash
sudo systemctl enable mongodb
```

Start the newly created service with **systemctl**.

```bash
sudo systemctl start mongodb
```

Use **systemctl** to check that the service has started properly.

```bash
sudo systemctl status mongodb
```

### Step 03 - Configuration

**Create database administrator account**

Create a database administrative account with Built-In Role root. This account will be used when connecting to the database after enabling authentication on MongoDB.

```javascript
use admin;
db.createUser(
  {
    user: "admin",
    pwd: "password",
    roles: [ { role: "root", db: "admin" } ]
  }
);
```

Read [Built-In Roles "root" — MongoDB Manual](https://docs.mongodb.com/manual/reference/built-in-roles/#root) for more information about "root" builtin role.


**Create user account for Tensor**

This account will be used by the Hilbert Space.

```javascript
use hilbertspace;
db.createUser(
  {
    user: "tensor",
    pwd: "tensor",
    db: "tensordb",
    roles: [ { role: "dbOwner", db: "tensordb" } ]
  }
);
```
Read [Built-In Roles "dbOwner" — MongoDB Manual](https://docs.mongodb.com/manual/reference/built-in-roles/#dbOwner) for more information about "dbOwner" builtin role. 


Tensor requires authentication to be enabled in MongoDB database.

Open **/etc/mongodb.conf** using **nano* or your favorite text editor.

```bash
sudo nano /etc/mongodb.conf
```

Uncomment **security** tag in configuration file and add **authorization: enabled** or replace it by following configuration values.

```yaml
security:
  authorization: enabled
```

Below is the full configuration file we used in production and testing, to learn more information about configuration options please refer the official [documentation of all options](http://docs.mongodb.org/manual/reference/configuration-options/).

```yaml
# mongod.conf

# Where and how to store data.
storage:
  dbPath: /var/lib/mongodb
journal:
  enabled: true
#  engine:
#  mmapv1:
#  wiredTiger:

# where to write logging data.
systemLog:
  destination: file
logAppend: true
path: /var/log/mongodb/mongod.log

# network interfaces
net:
  port: 27017
bindIp: 0.0.0.0


#processManagement:

security:
  authorization: enabled
#operationProfiling:

#replication:

#sharding:

## Enterprise-Only Options:

#auditLog:

#snmp:
```