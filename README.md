# rest-server
Node.js test server with Rest API

## 1. Environment
AWS is used for this server with below image.
* Image: Ubuntu Server 18.04 LTS (HVM), SSD Volume Type - ami-078e96948945fc2c9
* H/W: t2.micro(1 vCPUs, 2.5 GHz, Intel Xeon Family, 1 GiB memory, EBS only)
* Storage: 8GiB -> 30GiB

### 1. Install node.js (Latest LTS: 10.15.3)
https://github.com/nodesource/distributions/blob/master/README.md<br>
Install Node.js v10.x:<br>
For Using Ubuntu,<br>
```console
$ curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
$ sudo apt-get install -y nodejs
```
```console
$ node --version
v10.15.3
```

### 2. Install Mongo DB (currnet release: 4.0.6)
https://www.mongodb.com/download-center/community<br>
=><br>
https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/#import-the-public-key-used-by-the-package-management-system

#### 2-1. Import the public key used by the package management system
```console
$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
```

#### 2-2. Create a list file for MongoDB
For Ubuntu 18.04 (Bionic)
```console
$ echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```

#### 2-3. Reload local package database
For installing the latest stable version of MongoDB
```console
$ sudo apt-get install -y mongodb-org
```

#### 2-4. Configuration
File: /etc/mongod.conf<br>
Original path: /var/lib/mongodb, /var/log/mongodb/mongod.log<br>
```
# Where and how to store data.
storage:
  dbPath: /home/ubuntu/db/data
  journal:
    enabled: true

# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path: /home/ubuntu/db/log/mongod.log

# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1
```

#### 2-5. Run with configuration
```console
$ mongod --config /etc/mongod.conf
```

Later below warning should be checked.
```
WARNING: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine
              See http://dochub.mongodb.org/core/prodnotes-filesystem
WARNING: Access control is not enabled for the database.
              Read and write access to data and configuration is unrestricted.
```

#### 2-6. Install Robo3T on local PC to check data
https://robomongo.org/download<br>
=> Select 'Download Robo 3T'<br>
=> Install Robo 3T 1.2.1
