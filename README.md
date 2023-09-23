# Backup PostgreSQL Database in Docker Using Cron Job (Crontab)

![My Image](crontab.png)


## Introduction:

In a Dockerized environment, ensuring the security and integrity of your PostgreSQL database is crucial. Regular backups are a vital component of any disaster recovery strategy. In this article, we will explore how to automate the backup process of a PostgreSQL database running in a Docker container using the powerful cron job scheduler.

### _What is Crontab?_

Crontab is a Unix-based utility that allows users to schedule tasks to run automatically at specific intervals. By utilizing cron job scheduling, administrators can automate repetitive tasks, such as database backups, with ease.

#### Prerequisites
- Install Docker: `https://devopssec.fr/article/cours-complet-apprendre-technologie-docker` 
- Run Postgres Image on Docker: `https://www.docker.com/blog/how-to-use-the-postgres-docker-official-image/` 
- Basic knowledge of Cron: `https://phoenixnap.com/kb/set-up-cron-job-linux`

#### Step 1: Verify PostgreSQL database running on Docker

![My Image](docker-pg.jpeg)

Step 2: Creating a Backup Script
Next, let's create a shell script that will perform the backup operation. Open a text editor and create a new file named `backup.sh` with the following contents:
```shell
#!/bin/bash

docker exec rsDb pg_dump -U your_postgres_username -d your_postgres_database > /your_backup_directory/backup_$(date +\%Y-\%m-\%d-\%H:\%M).sql
```

Make sure to replace `/your_backup_directory` with the actual path where you want to store your backups. This script utilizes the `docker exec` command to execute the `pg_dump` utility inside the `my-postgresql` container, dumping the entire database to a file named based on the current date and time.

Step 3: Restrict access backup script file and backup directory

