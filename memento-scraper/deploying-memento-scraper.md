# This Is My First Time Running This Application

## Spin Up The Containers
1. Copy the ```docker-compose.yml``` file in this directory into a directory on your machine.
2. ```cd``` into the directory you created in step 1.
3. Run the following in a CLI
    ```bash
    docker-compose up --build
    ```
4. Initialize the database with appropriate db tables and db views.
    * Identify the ```memento-scraper-api```'s container id.
        ```bash
        docker container ls
        ```
    * Paste the id into a Docker copy command to bring a creation script to your host machine.
        ```bash
        docker cp <CONTAINER_ID>:./app/migration-scripts/creation-script.sql ./db-scripts/creation-script.sql
        ```
    * Run the newly copied script on ```memento-scraper-db```.
        ```bash
        docker exec -i memento-scraper-db mysql -uroot -proot MementoScraperDatabase < db-scripts/creation-script.sql
        ```
    * Create a db view. This file is saved in the ```memento-scraper-api``` repo. [Located Here.](https://github.com/LoganConnor44/MementoScraperApi/blob/master/Database/DbViews.sql) The below command assumes that you saved the file in db-scripts, which is a child directory under this one.
        ```bash
        docker exec -i memento-scraper-db mysql -uroot -proot MementoScraperDatabase < db-scripts/DbViews.sql
        ```

# I Have Ran This Application Before And There Are No Changes To The Database Structure
1. Run the following in a CLI
    ```bash
    docker-compose up --build
    ```

# I Want To Stop The Containers - I Plan To Return To This To Work On It.
1. Run the following in a CLI
    ```bash
    docker-compose down
    ```

# I Want To Stop The Containers - I DO NOT Plan To Return To This And Would Like Everything Removed.
1. Run the following in a CLI
    ```bash
    docker-compose down --volumes
    ```