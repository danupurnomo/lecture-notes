# AIRFLOW NOTES

Make sure you have cloned this [repository](https://github.com/ardhiraka/DEBlitz). 

For the Apache Airflow class (Week 2 - Day 1 PM), the docker compose that will be used is on the  `DEBlitz/MLPipeline/airflow_lite.yaml` path.

## A - Setup

1. Open Command Prompt or Terminal.

2. Change directory to `DEBlitz/MLPipeline/`.

3. Run file `airflow_lite.yml` with command :  
   ```sh
   docker-compose -f airflow_lite.yml up
   ```
4. Wait until `airflow-scheduler`, `airflow-webserver`, and `postgres` show green status as shown in the image below. **It takes some time for these three to turn green.** Therefore, please be patient and wait.

5. Check apps :
   - Open your browser and type `localhost:8080` in your browser tab

5. To close the apps :
   - Open Command Prompt or Terminal and change directory to `DEBlitz/MLPipeline/`.
   - Run the following command in Command Prompt or Terminal
     ```
     Syntax : $ docker-compose -f airflow_lite.yml down
     ```



---
## A. Docker-Compose
Location : `DEBlitz/MLPipeline/airflow_lite.yaml`

---
# B. Apache-Airflow Package
```
$ pip install apache-airflow==2.3.4 --constraint https://raw.githubusercontent.com/apache/airflow/constraints-2.3.4/constraints-3.9.txt
$ pip install apache-airflow-providers-postgres --constraint https://raw.githubusercontent.com/apache/airflow/constraints-2.3.4/constraints-3.9.txt

Jika error dalam instalasi apache-airflow-providers-postgres
$  pip install apache-airflow-providers-postgres==5.4.0
```

---
# C. Cek Database
1. Step 1 : Cari nama container dari `airflow-scheduler`
   ```
   Syntax : $ docker ps -a
   ```

   Contoh hasil
   ```
   CONTAINER ID   IMAGE                  COMMAND                  CREATED       STATUS                   PORTS                              NAMES
   52f5eed4b6b9   apache/airflow:2.3.4   "/usr/bin/dumb-init …"   2 hours ago   Up 2 hours (healthy)     0.0.0.0:8080->8080/tcp             airflow-webserver
   e4c734fc7103   apache/airflow:2.3.4   "/usr/bin/dumb-init …"   2 hours ago   Up 2 hours               8080/tcp, 0.0.0.0:8793->8793/tcp   airflow-scheduler
   79f9e206d104   apache/airflow:2.3.4   "/bin/bash -c 'mkdir…"   2 hours ago   Exited (0) 2 hours ago                                      airflow-init
   1a61b7006758   postgres:13            "docker-entrypoint.s…"   2 hours ago   Up 2 hours (healthy)     0.0.0.0:5434->5432/tcp             postgres
   ```
   Terlihat bahwa container untuk `airflow-scheduler` bernama `airflow-scheduler`

2. Masuk ke dalam container `airflow-scheduler
   ```
   Syntax  : $ docker container exec -it <container-name> bash
   Example : $ docker container exec -it airflow-scheduler bash
   ```

3. Masuk ke dalam Python dengan cara ketikkan `python`

4. Koneksikan Python dengan SQL
   ```
   import pandas as pd
   from sqlalchemy import create_engine
   engine = create_engine('postgresql+psycopg2://airflow:airflow@postgres/airflow')
   pd.read_sql('SELECT * FROM experiments', engine)
   ```

5. Keluar dari Python, ketikkan `$ exit()`.

6. Keluar dari Docker Container, ketikkan `$ exit`.
