# Databasee

## Install:

**Install MongoDB**

```sh
# Ubuntu 18.04 LTS
sudo apt-get install gnupg

wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -

echo "deb http://repo.mongodb.org/apt/debian buster/mongodb-org/4.2 main" | sudo tee /etc/apt/sources.list.d/mongodb.list


sudo apt install mongodb-org

sudo systemctl enable mongod
sudo systemctl start mongod 

# whitelist IPs : https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-18-04

# Validate: mongo --eval 'db.runCommand({ connectionStatus: 1})'
```

## Configure DB
**Admin config**

```sh
#1) disable security (/etc/mongod.conf) --> Restart Mongodb
#> security:
#>   authorization: "disabled"

#2) drop admin user if exist
mongo admin --eval 'db.dropUser("superadmin")'
#3) create admin user
mongo admin --eval 'db.createUser( { user: "superadmin", pwd: "MyPass1234", roles: [ { role: "clusterAdmin", db: "admin" }, { role: "userAdminAnyDatabase", db: "admin" } ] } )'
#4) enable security (/etc/mongod.conf) --> Restart Mongodb
#> security:
#>   authorization: "enabled"
```