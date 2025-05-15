# ELASTICSEARCH & KIBANA NOTES

---
## A. Requirements

1. Make sure you have cloned this [repository](https://github.com/ardhiraka/DEBlitz).

2. Make sure that the Docker and PostgreSQL applications are installed on your computer

3. **It is highly recommended to use Python 3.9 or Python 3.10.** If you have Python 3.11, create another Python environment with Python 3.9 or Python 3.10 (Python 3.9 is recommended). Example of how to create a new Python's environment with Anaconda.

   *The syntax below will create a new environment named `env_py39`. You can change the name of this environment according to your preference.*
   ```sh
   conda create -n env_py39 python=3.9
   ```

4. **Use the same Python environment to run Apache Airflow, Elasticsearch, and Kibana**.

5. Install the following packages : 
    * For Elasticsearch
        ```py
        pip install "elasticsearch<7.14"
        pip install faker
        pip install --upgrade "numpy<2.0"
        pip install --upgrade "pandas<2.0.0"
        pip install psycopg2-binary
        ```

   * For Apache Airflow 
        - Python 3.9
            ```py
            pip install apache-airflow==2.3.4 --constraint https://raw.githubusercontent.com/apache/airflow/constraints-2.3.4/constraints-3.9.txt
            
            pip install apache-airflow-providers-postgres --constraint https://raw.githubusercontent.com/apache/airflow/constraints-2.3.4/constraints-3.9.txt
            ```
            
            If you encounter an error while installing the `apache-airflow-providers-postgres` package, then install the following package.
            ```py
            pip install apache-airflow-providers-postgres==5.4.0
            ```
   
        - Python 3.10
            ```py
            pip install apache-airflow==2.3.4 --constraint https://raw.githubusercontent.com/apache/airflow/constraints-2.3.4/constraints-3.10.txt
            
            pip install apache-airflow-providers-postgres --constraint https://raw.githubusercontent.com/apache/airflow/constraints-2.3.4/constraints-3.10.txt
            ```

            If you encounter an error while installing the `apache-airflow-providers-postgres`` package, then install the following package.
            ```py
            pip install apache-airflow-providers-postgres==5.4.0
            ```

6. Make sure the above packages are installed succesfully before you run docker-compose of Elasticsearch and Airflow.

---

## B. Elasticsearch

1. Open Docker Desktop.

2. Open file `DEBlitz/compose_file/elastic-kibana.yml`.

3. Change the following lines :
   * **For Non Apple M1/M2/M3 Computer**
     * Elasticsearch version
   
        **BEFORE**
         ```yml
         version: "3.3"
         services:
            elasticsearch:
               image: docker.elastic.co/elasticsearch/elasticsearch:7.4.0
               container_name: elasticsearch
         ```

         **AFTER**
         ```yml
         version: "3.3"
         services:
            elasticsearch:
               image: docker.elastic.co/elasticsearch/elasticsearch:7.13.0
               container_name: elasticsearch
         ```
      
      * Kibana version
   
        **BEFORE**
         ```yml
         kibana:
            container_name: kibana
            image: docker.elastic.co/kibana/kibana:7.4.0
         ```
   
         **AFTER**
         ```yml
         kibana:
            container_name: kibana
            image: docker.elastic.co/kibana/kibana:7.13.0
         ```
   * **For Apple M1/M2/M3 Computer**
     * Elasticsearch version
   
        **BEFORE**
         ```yml
         version: "3.3"
         services:
            elasticsearch:
               image: docker.elastic.co/elasticsearch/elasticsearch:7.4.0
               container_name: elasticsearch
         ```

         **AFTER**
         ```yml
         version: "3.3"
         services:
            elasticsearch:
               image: docker.elastic.co/elasticsearch/elasticsearch:7.13.0-arm64
               container_name: elasticsearch
         ```
      
      * Kibana version
   
        **BEFORE**
         ```yml
         kibana:
            container_name: kibana
            image: docker.elastic.co/kibana/kibana:7.4.0
         ```
   
         **AFTER**
         ```yml
         kibana:
            container_name: kibana
            image: docker.elastic.co/kibana/kibana:7.13.0-arm64
         ```
4. Open Command Prompt or Terminal.

5. Change directory to `DEBlitz/compose_file/`.

6. Run file `elastic-kibana.yml` with command :  
   ```py
   docker-compose -f elastic-kibana.yml up
   ```
   Let this command prompt run and open to use Kibana & Elastic.

7. Check apps :
   - Open your browser
   - For **Elasticsearch**, type `http://localhost:9200` in your browser tab
     ![plot](image/elastic-kibana/elasticsearch-7.13.png)
   - For **Kibana**, type `http://localhost:5601` in your browser tab
     ![plot](image/elastic-kibana/kibana-7.13.png)

8. To close the apps :
    - Terminate the Command Prompt used to run Elasticsearch by pressing `CTRL + C` or `Command + C`.
    - If the previous steps above cannot be done then open Command Prompt or Terminal and navigate to `DEBlitz/compose_file/` directory.
    - Run the following command :
        ```py
        docker-compose -f elastic-kibana.yml down
        ```

## C. Apache Airflow

For the Apache Airflow class (Week 2 - Day 1 PM), the docker compose that will be used is on the `DEBlitz/MLPipeline/airflow_lite.yaml` path.

1. Open Docker Desktop.

2. Open Command Prompt or Terminal.

3. Change directory to `DEBlitz/MLPipeline/`.

4. Run file `airflow_lite.yml` with command :  
    ```sh
    docker-compose -f airflow_lite.yaml up
    ```

5. Wait until `airflow-scheduler`, `airflow-webserver`, and `postgres` show green status as shown in the image below. ![plot](image/airflow/01%20-%20Setup.png) **It takes some time for these three to turn green.** Therefore, please be patient and wait.

6. If the three items above are already in green status, then follow the steps below to ensure whether Apache Airflow is fully running or not.
   - Open your browser.
   - Type `http://localhost:8080` in the browser tab.
   - A display like the one below will appear. ![plot](image/airflow/02%20-%20Browser.png)
   - If the above display does not appear on the browser tab, wait for a moment. You can continue refreshing the page until the Apache Airflow Homepage is visible.

7. To close the app : 
    - Terminate the Command Prompt used to run Apache Airflow by pressing `CTRL + C` or `Command + C`.
    - If the previous steps above cannot be done then open Command Prompt or Terminal and navigate to `DEBlitz/MLPipeline/` directory.
    - Run the following command :
        ```py
        docker-compose -f airflow_lite.yml down
        ```