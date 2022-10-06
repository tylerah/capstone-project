#### Database Work:
- Created an RDS in AWS called yrbs-database2
    - Made settings public
- Connected my pgAdmin to rds instance
    - Made a server named AWS and database named yrbs-database2
- Created an s3 bucket called group2-yrbs-data
    - Added in demographics.csv and records.csv
- created a gitignore for passwords
- Created an ERD to show relationship between demographics and records tales
- Created tables in pgAdmin so that the demographics and records data importing from the jupyter notebook would have somewhere to go
    - the sql code is stored in the file postgres_table_creation
    - I also added code in this file that joins the two tables together
- Wrote code in the jupyter notebook file named data_to_database_code to: 
    - Read data from s3 bucket into pandas dataframe using boto3
    - put dataframe into the aws rds postgres
    - pulled the data back into a dataframe
    - pulled in a table that was joined in postgres

#### Roadblocks encountered:
- The first big roadblock was when I was writing the 'create engine' statement to put the a test dataframe into the database. I accidentally wrote a statement for a mysql database instead of a postgres database, which is what I selected when I set up the aws rds. 
- The second big roadblock was when I was putting the real dataframes into the database. I was capitalizing the names of my tables, which was creating problems in pgAdmin. Also, in troubleshooting, I managed to lock/freeze the session, which prevented anything from happening. I wasn't getting any error message, but the data wasn't transfering to the table. It was helpful to troubleshoot by looking at the error log in AWS, and to look on the dashboard of pgAdmin. After terminating the problmatic sessions and deleting and recreating tables with lowercase names, the data import was successful. 