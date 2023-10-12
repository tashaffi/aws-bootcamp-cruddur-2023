# Week 1 — Running the app locally

### Running the App Locally

To run the backend and frontend locally, run the following commands from the root directory:

```
cd backend-flask/
pip3 install -r requirements.txt
export BACKEND_URL="*"`
export FRONTEND_URL="*"`python3 -m flask run --host=0.0.0.0 --port=4567
```
```
cd frontend-react-js/
npm i
npm start
```

Unlock the ports as such:

![Unlock Port](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/journal/Assets/Week1/unlock_ports.png)

Check the backend and frontend is working correctly:

![Backend API Response](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/journal/Assets/Week1/backend_response_JSON.png)

![Frontend API Response](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/journal/Assets/Week1/frontend_response.png)


### Containerize Frontend and Backend

The Dockerfiles 

For containerizing both the apps, write a Dockerfile in the `backend-flask` and `frontend-react-js` folder as below.

[Dockerfile for Flask backend](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/backend-flask/Dockerfile)

[Dockerfile for React frontend](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/frontend-react-js/Dockerfile)

Build the docker images:

```
cd /workspace/aws-bootcamp-cruddur-2023
docker build -t backend-flask ./backend-flask
docker build -t frontend-react-js ./frontend-react-js
```

Run the containers:

```
docker run --rm -p 4567:4567 -it -e FRONTEND_URL='*' -e BACKEND_URL='*' backend-flask
docker run --rm -p 3000:3000 -d frontend-react-js
```

Check the images have been created:

![Check Docker Up](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/journal/Assets/Week1/check_docker_up.png)


Separarely running the Dockerfiles will launch the frontend and backend apps at port 3000 and 4567 respectively, which we can check from `ports`.

### Creating the notifications endpoint

It is similar to the `/api/activities/home` endpoint.

- Add `/api/activities/notifications` path to `paths` in the `openapi-3.0.yml` file. 
- Create a `notifications_activities.py` file in the `services` folder. Again it should be similar to `/api/activities/home`. 
- Import everything to the `app.py` file from `notifications_activities.py`.
- Add a new route called `/api/activities/notifications`. Don't forget to change the function from `data_home` to something else if you copied code from `/api/activities/home`.

Check notifications endpoint: 

![Check Notifications Backend](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/journal/Assets/Week1/backend_notifications.png)


For frontend, the process is pretty similar to the `home` endpoint there. Simply add a new route `/notifications` to `App.js`. Create `NotificationsFeedPage.css` and `NotificationsFeedPage.js` files in the `pages` folder and import them in `App.js`. 

Check notifications endpoint: 

![Check Notifications Frontend](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/journal/Assets/Week1/frontend_notification.png)


### Adding DynamoDB Local and Postgres

Under `services` in the `docker-compose.yml` file, add the following:

```
dynamodb-local:
    # https://stackoverflow.com/questions/67533058/persist-local-dynamodb-data-in-volumes-lack-permission-unable-to-open-databa
    # We needed to add user:root to get this working.
    user: root
    command: "-jar DynamoDBLocal.jar -sharedDb -dbPath ./data"
    image: "amazon/dynamodb-local:latest"
    container_name: dynamodb-local
    ports:
      - "8000:8000"
    volumes:
      - "./docker/dynamodb:/home/dynamodblocal/data"
    working_dir: /home/dynamodblocal
```
 
For `postgres`, add the following under `services`:

```
db:
    image: postgres:13-alpine
    restart: always
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=password
    ports:
      - '5432:5432'
    volumes: 
      - db:/var/lib/postgresql/data
```

Don't forget to define a volume `db` that uses the `local` storage. This volume allows data to be persisted across container restarts or shared between multiple containers. Add the following to the end of the file:

```
volumes:
  db:
    driver: local
```

You can test connection to `dynamodb` using the code in this link: [challenge-dynamodb-local](https://github.com/100DaysOfCloud/challenge-dynamodb-local)

To interact with `postgres`, install the client by adding following commands to the `.gitpod.yml` file:

```
- name: postgres
    init: |
      curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg
      echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" |sudo tee  /etc/apt/sources.list.d/pgdg.list
      sudo apt update
      sudo apt install -y postgresql-client-13 libpq-dev
```

Install the `PostgreSQL` extension on VSCode from `cweijan`. Connect to it using password `password`. 

![Test Database Connection](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/journal/Assets/Week1/postgre_connection.png)

