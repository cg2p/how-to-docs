# Mongo

## Run and check
```
mongod --config /usr/local/etc/mongod.conf --fork
ps aux | grep -v grep | grep mongod
```
Use Compass desktop tool to connect and browse databases

## Mongo via Docker
[Mongo on Docker](https://hub.docker.com/_/mongo)

## Mongo via IBM Cloud Database as a Service
IBM Cloud
- created db instance [db instance name]
- Manage tab > Settings > change Admin pwd
- Service Credentials > create new
- used 'composed' as URI string in Compass
- added to Compass settings
https://cloud.ibm.com/docs/databases-for-mongodb?topic=databases-for-mongodb-getting-started
- created cert file from Manage | Connection panel
- Server Validated


## Other References
CONNECITON STRING

https://books.google.com.au/books?id=1cHvAwAAQBAJ&pg=PA150&lpg=PA150&dq=how+connection+string+mongo+dev+prod&source=bl&ots=BrA_tiUyjY&sig=ACfU3U2G4pbqzyAVR4TdqRobnsmXDvKBfg&hl=en&sa=X&ved=2ahUKEwiRtffmqqXpAhXxzjgGHXHmA_4Q6AEwC3oECAoQAQ#v=onepage&q=how%20connection%20string%20mongo%20dev%20prod&f=false

https://codingsans.com/blog/node-config-best-practices 

Mongodb as operator
https://www.mongodb.com/blog/post/introducing-the-mongodb-enterprise-operator-for-kubernetes  

