### Installation Airflow

Refer to [Airflow](https://airflow.incubator.apache.org/) instruction
Install airflow from pip.
```sh
$ export AIRFLOW_HOME=~/airflow (here is the home directory for airflow)
$ apt-get install python-dev libxml2-dev libxslt1-dev zlib1g-dev libmysqlclient-dev
$ pip install airflow 
```

If there is an error (in ubuntu 14), try 
```sh
$ pip install werkzeug itsdangerous click
```
If want to use Airflow's SQLite database and run SequentialExecuter 
```sh
$ airflow initdb
```
Otherwise setting up MySQL database to use LocalExecuter and do,
```
$ pip install airflow[mysql]
```
Then connect to MySQL and create an empty database [airflow], then run
```
airflow webserver -p 8080
airflow scheduler
```


### Airflow configuretion 
Go to airflow directory and find airflow.cfg, this is the main configuretion file for airflow
```
dags_folder = * (the location of dags)
base_log_folder = * (the location of logs, logs are also stored in MySQL)
sql_alchemy_conn = ialect+driver://username:password@host:port/database (Connect to MySQL)
executor = LocalExecutor
load_examples = False (disable examples)
smtp_host = smtp.gmail.com (Set smtp)
smtp_starttls = True 
smtp_ssl = False
smtp_user = user@oanda.com
smtp_password = *****
smtp_port = 587
smtp_mail_from = user@oanda.com
```

### Airflow command line
Refer to [Command line](https://airflow.incubator.apache.org/cli.html) 
Here are the frequently used CLIs
* Export or import variables
```
$ airflow variables [-e filepath] [-i filepath] 
```
* Trigger a dag run
```
$ airflow trigger_dag dag_id
```
* Test, runnning a task without any dependencies and dont record to database
```
$ airflow test dag_id task_id execution_date
```
* list all dags
```
$ airflow list_dags
```
* Backfill, run subsections of a dag for a specified date range
```
airflow backfill [-s START_DATE] [-e END_DATE] dag_id
```


