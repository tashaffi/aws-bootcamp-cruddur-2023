# Week 1 — App Containerization

To run the backend and frontend locally, run the following commands from the root directory:

```
cd backend-flask/
pip3 install -r requirements.txt
export BACKEND_URL="*"`
export FRONTEND_URL="*"`python3 -m flask run --host=0.0.0.0 --port=4567
```

Unlock the ports as such:

![Unlock Port](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/journal/Assets/Week1/unlock_ports.png)

Check the backend is working correctly:

![Backend API Response](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/journal/Assets/Week1/backend_response_JSON.png)


The Dockerfiles 

[Dockerfile for Flask backend](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/backend-flask/Dockerfile)

[Dockerfile for React frontend](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/frontend-react-js/Dockerfile)
