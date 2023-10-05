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

Creating the notifications endpoint:

It is similar to the `/api/activities/home` endpoint.

- Add `/api/activities/notifications` path to `paths` in the `openapi-3.0.yml` file. 
- Create a `notifications_activities.py` file in the `services` folder. Again it should be similar to `/api/activities/home`. 
- Import everything to the `app.py` file from `notifications_activities.py`.
- Add a new route called `/api/activities/notifications`. Don't forget to change the function from `data_home` to something else if you copied code from `/api/activities/home`.
