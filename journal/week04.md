# Week 4 — Postgres and RDS

#### Provision RDS Database
``` aws rds create-db-instance \
  --db-instance-identifier cruddur-db-instance \
  --db-instance-class db.t3.micro \
  --engine postgres \
  --engine-version  14.6 \
  --master-username root \
  --master-user-password huEE33z2Qvl383 \
  --allocated-storage 20 \
  --availability-zone ca-central-1a \
  --backup-retention-period 0 \
  --port 5432 \
  --no-multi-az \
  --db-name cruddur \
  --storage-type gp2 \
  --publicly-accessible \
  --storage-encrypted \
  --enable-performance-insights \
  --performance-insights-retention-period 7 \
  --no-deletion-protection
```
### issues using the above to setup RDS: 
Create a subnet group with the following commaand and existing subents from VPC: 
```
aws rds create-db-subnet-group \
  --db-subnet-group-name mydbsubnetgroup \
  --db-subnet-group-description "My DB subnet group" \
  --subnet-ids subnet-12345678 subnet-87654321 # Specify the subnet ID's 
```
Another fix around this is to go in the RDS section on AWS management console and check the subnet group name which is already assigned: Then use the command: ``` --db-subnet-group-name < enter the name of the subnet group already assigned > ``` in the above setup code for provisioning the database. This will allow any errors returned be approved without any issues. I tried this and I am seeing the database being setup under RDS. 

