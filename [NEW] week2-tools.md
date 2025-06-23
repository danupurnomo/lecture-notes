# WEEK 2 TOOLS NOTES

---

## A. Requirements

1. Make sure you have cloned this [repository](https://github.com/ardhiraka/DEBlitz).

2. Make sure that the Docker and PostgreSQL applications are installed on your computer

3. It is highly recommended to use Python 3.9 or Python 3.10.
    - If you have Python 3.11 or higher, please create a new environment with Python 3.9 or 3.10 (Python 3.9 is preferred for compatibility).
    - You can create a Python 3.9 environment by following the guide at the following [link](https://drive.google.com/drive/folders/1jZvfr8eMT_jN9zKfOEZAE44gHeJRQvwp?usp=drive_link). *Make sure to follow the instructions in the `notes.md` file provided in the folder.*

4. You will be using a Python environment named `h8_env` during Phase 2, especially for topics related to Data Engineering.

5. Make sure the above packages are installed succesfully before you run docker-compose of Elasticsearch and Airflow.

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

5. Activate the Python environment named `h8_env`. Type the following command : 
    ```bash
    conda activate h8_env
    ```

6. Change directory to `DEBlitz/compose_file/`.

7. Run file `elastic-kibana.yml` with command :  
   ```py
   docker-compose -f elastic-kibana.yml up
   ```
   Let this command prompt run and open to use Kibana & Elastic.

8. Check apps :
   - Open your browser
   - For **Elasticsearch**, type `http://localhost:9200` in your browser tab
     ![plot](image/elastic-kibana/elasticsearch-7.13.png)
   - For **Kibana**, type `http://localhost:5601` in your browser tab
     ![plot](image/elastic-kibana/kibana-7.13.png)

9. To close the apps :
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

3. Activate the Python environment named `h8_env`. Type the following command : 
    ```bash
    conda activate h8_env
    ```

4. Change directory to `DEBlitz/MLPipeline/`.

5. Run file `airflow_lite.yml` with command :  
    ```sh
    docker-compose -f airflow_lite.yaml up
    ```

6. Wait until `airflow-scheduler`, `airflow-webserver`, and `postgres` show green status as shown in the image below. ![plot](image/airflow/01%20-%20Setup.png) **It takes some time for these three to turn green.** Therefore, please be patient and wait.

7. If the three items above are already in green status, then follow the steps below to ensure whether Apache Airflow is fully running or not.
   - Open your browser.
   - Type `http://localhost:8080` in the browser tab.
   - A display like the one below will appear. ![plot](image/airflow/02%20-%20Browser.png)
   - If the above display does not appear on the browser tab, wait for a moment. You can continue refreshing the page until the Apache Airflow Homepage is visible.

8. To close the app : 
    - Terminate the Command Prompt used to run Apache Airflow by pressing `CTRL + C` or `Command + C`.
    - If the previous steps above cannot be done then open Command Prompt or Terminal and navigate to `DEBlitz/MLPipeline/` directory.
    - Run the following command :
        ```py
        docker-compose -f airflow_lite.yml down
        ```