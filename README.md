Postgres Backup and Restore for K8s postgres statefulsets

Requirements:
1. S3 Bucket
2. Aws account with IAM permission for S3 bucket
3. Postgres user with privilege for database(s)


Backup:
The pg_dumpall utility is used due to the possible presence of multiple databases running on the Postgres server

To setup backup; 
1. Configure aws.yml with your aws credential details
2. Configure the db_backup.yml spec. and make the following changes:
   - Set the backup job schedule (default is 1:00AM daily)
   - Set the required values for dbhost, dbuser and s3 bucket
3. Configure the secret.yml with the required credentials 
4. Kubectl create -f db_backup.yml
This initiates the daily backup cronjob


To Restore Database:
1. Configure the restore-configmap.yml file
2. Kubectl create -f db_restore.yml
3. Clean up resources when done
