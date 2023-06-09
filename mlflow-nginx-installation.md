# MLFlow Production Server Installation

```
conda create -n mlflow_env
conda activate mlflow_env
```
```
conda install python
pip install mlflow
pip install pysftp
```
```
apt-get install postgresql postgresql-contrib postgresql-server-dev-all
```
```
sudo -u postgres psql
```
```
CREATE DATABASE mlflow_db;
CREATE USER mlflow_user WITH ENCRYPTED PASSWORD 'mlflow';
GRANT ALL PRIVILEGES ON DATABASE mlflow_db TO mlflow_user;
```
```
sudo apt install gcc
pip install psycopg2-binary
```
```
service postgresql restart
```
```
mkdir ~/mlflow/mlruns
```
```
mkdir ~/mlflow/mllogs
```
```
mlflow server --backend-store-uri postgresql://mlflow_user:mlflow@localhost/mlflow_db --default-artifact-root sftp://mlflow_user@<hostname_of_server>:~/mlflow/mlruns -h 0.0.0.0 -p 8000
```
```
sudo apt-get install nginx -y
```
```
sudo nano /etc/nginx/sites-available/default
```
```
location / {
    # First attempt to serve request as file, then
    # as directory, then fall back to displaying a 404
    proxy_pass http://127.0.0.1:8000/;
    proxy_buffering off;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-Host $host;
    proxy_set_header X-Forwarded-Port $server_port;
}
```
```
sudo service nginx restart
```
```
sudo apt-get install apache2-utils
```
```
sudo htpasswd -c /etc/apache2/.htpasswd username
```
# for other users
```
sudo htpasswd /etc/apache2/.htpasswd user2
```
