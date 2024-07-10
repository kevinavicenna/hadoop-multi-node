# Hadoop MapReduce Multi Node

This repository contains an example of running a MapReduce job using Hadoop in Docker. Below are the steps and details of the setup and how i insert the data:

## Prerequisites

- Docker

## Setup Instructions

1. **Clone the Repository**

   Clone this repository to your local machine:
   ```bash
   git clone url_this_repo
   cd to_the_folder
   ```

3. **Run Hadoop Cluster**

   Start a multinode Hadoop cluster using Docker:
   ```bash
   docker compose up -d
   ```

4. **Verify Hadoop Cluster Status**

   Ensure all containers are running and Hadoop services are up:
   ```bash
   docker compose ps
   ```

5. **Prepare Input Data**

   Upload input data files (`/Indonesian.csv` in this example) to Hadoop HDFS:
   ```bash
   docker exec -it hadoop-settings-namenode-1 bash -c "hadoop fs -put /usr/hadoop/Indonesian.csv /"
   ```

6. **Run MapReduce Job**

   Execute a word count example job:
   ```bash
   docker exec -it hadoop-settings-namenode-1 bash -c "yarn jar /opt/hadoop-3.3.6/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.6.jar wordcount /Indonesian.csv /output"
   ```

7. **View Job Results**

   Monitor the job progress and view results:
   - Check job status and details in the Hadoop Resource Manager UI (`http://localhost:8088`).
   - View job counters and output files in Hadoop HDFS:
     ```bash
     docker exec -it hadoop-settings-namenode-1 bash -c "hadoop fs -ls /output"
     docker exec -it hadoop-settings-namenode-1 bash -c "hadoop fs -cat /output/part-r-00000"
     ```

8. **Cleanup**

   Stop and remove the Docker containers:
   ```bash
   docker compose down
   ```


