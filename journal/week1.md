# Week 1 — App Containerisation

Why container an application? There will be different versions on python for example, there will be different operating systems and is an easy way to combine and test into a container. 
Linuxserver.io -> container images with docker files.
Dockerhub --> container registry for sharing and pushing images to a container registry. There are standards for building images for applications. (Like a github for storing images). 

### VSCode Docker Extension
Docker for VSCode makes it easy to work with Docker

https://code.visualstudio.com/docs/containers/overview

#### Issues faced & solved
When installing the ```pip3 install -r requirements.txt``` followed by the command ```python3 -m flask run --host=0.0.0.0 --port=4567``` there is an issue when trying to load the URL 

```sh
cd backend-flask
export FRONTEND_URL="*"
export BACKEND_URL="*"
python3 -m flask run --host=0.0.0.0 --port=4567
cd ..
```
Issue was fixed when unlocking the port on the port tab. The following needed adding to URL `/api/activities/home` to open the URL returning the json 

#### CRTL+C quits the opened window stops the terminal

### Add docker file initiation 
```
FROM python:3.10-slim-buster

WORKDIR /backend-flask

COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY . .

ENV FLASK_ENV=development

EXPOSE ${PORT}
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]
```
#### To remove variables the following command is used `unset BACKEND_URL`
#### To check if variables are removed you use env | grep Backend --> This should return with nothing as the variables are removed 
#### `git config --global pull.rebase true` fixed the pull / push issue in syncing into git

#### To install the Postgres Client: 
  - name: postgres
   ``` init: |
      curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg
      echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" |sudo tee  /etc/apt/sources.list.d/pgdg.list
      sudo apt update
      sudo apt install -y postgresql-client-13 libpq-dev
```

#### To install Dynamodb local
```
aws dynamodb create-table \
    --endpoint-url http://localhost:8000 \
    --table-name Music \
    --attribute-definitions \
        AttributeName=Artist,AttributeType=S \
        AttributeName=SongTitle,AttributeType=S \
    --key-schema AttributeName=Artist,KeyType=HASH AttributeName=SongTitle,KeyType=RANGE \
    --provisioned-throughput ReadCapacityUnits=1,WriteCapacityUnits=1 \
    --table-class STANDARD

```



