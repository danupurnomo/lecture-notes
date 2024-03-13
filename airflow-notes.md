# AIRFLOW NOTES

---
## A. Requirements

1. Make sure you have cloned this [repository](https://github.com/ardhiraka/DEBlitz).

2. Make sure that the Docker and PostgreSQL applications are installed on your computer

3. **It is highly recommended to use Python 3.9 or Python 3.10.** If you have Python 3.11, create another Python environment with Python 3.9 or Python 3.10 (Python 3.9 is recommended).

4. Install the following packages : 
   * For Python 3.9
     ```py
     pip install apache-airflow==2.3.4 --constraint https://raw.githubusercontent.com/apache/airflow/constraints-2.3.4/constraints-3.9.txt
     
     pip install apache-airflow-providers-postgres --constraint https://raw.githubusercontent.com/apache/airflow/constraints-2.3.4/constraints-3.9.txt
     ```
     
     If you encounter an error while installing the `apache-airflow-providers-postgres` package, then install the following package.
     ```py
     pip install apache-airflow-providers-postgres==5.4.0
     ```
   
   * For Python 3.10
     ```py
     pip install apache-airflow==2.3.4 --constraint https://raw.githubusercontent.com/apache/airflow/constraints-2.3.4/constraints-3.10.txt
     
     pip install apache-airflow-providers-postgres --constraint https://raw.githubusercontent.com/apache/airflow/constraints-2.3.4/constraints-3.10.txt
     ```

     If you encounter an error while installing the `apache-airflow-providers-postgres`` package, then install the following package.
     ```py
     pip install apache-airflow-providers-postgres==5.4.0
     ```

5. Make sure the above packages are installed succesfully before you run docker-compose of Apache Airflow.

---
## B. Setup

For the Apache Airflow class (Week 2 - Day 1 PM), the docker compose that will be used is on the `DEBlitz/MLPipeline/airflow_lite.yaml` path.

1. Open Command Prompt or Terminal.

2. Change directory to `DEBlitz/MLPipeline/`.

3. Run file `airflow_lite.yml` with command :  
   ```sh
   docker-compose -f airflow_lite.yaml up
   ```

4. Wait until `airflow-scheduler`, `airflow-webserver`, and `postgres` show green status as shown in the image below. ![plot](image/airflow/01%20-%20Setup.png) **It takes some time for these three to turn green.** Therefore, please be patient and wait.

5. If the three items above are already in green status, then follow the steps below to ensure whether Apache Airflow is fully running or not.
   * Open your browser.
   * Type `http://localhost:8080` in the browser tab.
   * A display like the one below will appear. ![plot](image/airflow/02%20-%20Browser.png)
   * If the above display does not appear on the browser tab, wait for a moment. You can continue refreshing the page until the Apache Airflow Homepage is visible.

---
## C. Close the App
To close the app : 

1. Open Command Prompt or Terminal.

2. Change directory to `DEBlitz/MLPipeline/`.

3. Run file `airflow_lite.yml` with command :  
   ```sh
   docker-compose -f airflow_lite.yaml down
   ```
