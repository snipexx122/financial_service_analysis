FROM python:3.8

WORKDIR /app

COPY . /app

RUN pip install pipenv
RUN pipenv --python 3.8

ENV AIRFLOW_HOME=/app

RUN pipenv install apache-airflow==2.1.0
RUN pipenv install apache-airflow-providers-databricks


# Install Airflow system-wide
RUN pipenv run pip install apache-airflow==2.1.0

# Initialize the Airflow database
RUN pipenv run airflow db init

# Set the password environment variable
RUN AIRFLOW__CORE__LOAD_EXAMPLES=False pipenv run airflow db init

# Create the Airflow admin user
RUN AIRFLOW__CORE__LOAD_EXAMPLES=False pipenv run airflow users create --username admin --firstname abdalla --lastname taarit --role Admin --email abdallah.taarit01206@gmail.com --password $AIRFLOW_ADMIN_PASSWORD

RUN pip install "apache-airflow[databricks, celery, s3, password]"

RUN pipenv run airflow webserver

ENTRYPOINT ["pipenv", "run", "airflow"]
CMD ["scheduler"]