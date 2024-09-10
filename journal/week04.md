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

#### Quick start for Postgres
1) Use the postgres:bash terminal. ``` psql -Upostgres --host localhost ``` This is to connect into localhost psql
2) Create a database called cruddur. You can check what databases are available by using ```\l```
3) The command for this is ``` CREATE database cruddur; ```
4) Go back into the bash terminal by pressing /q to quit from the Upostgres page and head back into postgress:bash.
5) Enter this command in backend-flask by cd into it. ```psql cruddur < db/schema.sql -h localhost -U postgres``` This pushes the contents of db/schema.sql into cruddur
6) Following this to check if the contents have been pushed you will use the following command to confirm the connection can be made using the following command: ``` PSQL postgresql://postgres:password@127.0.0.1:5432/cruddur ```
7) Once the environment variables have been saved
```
export CONNECTION_URL="postgresql://postgres:password@127.0.0.1:5432/cruddur"
gp env CONNECTION_URL="postgresql://postgres:password@127.0.0.1:5432/cruddur"
```
8) Check on postgres:bash if the connection can be made without entering the long URL by entering: ``` psql $ CONNECTION_URL. The error I faced was the local host IP address in connection URL. Before I had ```password@localhost:5432 ``` I changed this to ``` postgresql://postgres:password@127.0.0.1:5432/cruddur ``` and can now connect into the database this way
9) The files created db-create, db-drop and db-schema-load will be able to accessed by entering ./bin/db-drop (This will drop the database). ./bin/db-create will create the database. Making sure the file locations are assigned correctly.   

  
