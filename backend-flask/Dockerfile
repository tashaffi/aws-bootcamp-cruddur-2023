FROM python:3.10-slim-buster

#Inside Container
WORKDIR /backend-flask


#Outside container-> Inside container
#this contains the libraries we want to install to run the app
COPY requirements.txt requirements.txt


#Inside container
#Install the Python libraries used for the app
RUN pip3 install -r requirements.txt

#Outside container -> Inside container
#first period . (/backend-flask outside container)
#second period . (/backend-flask inside container)
COPY . .

#Set environment variables (Env Vars)
#Inside container and will return 
ENV FLASK_ENV=development

EXPOSE ${PORT}

#CMD (Command)
#python3 -m flask run --host=0.0.0.0 --port=4567
CMD [ "python3", "-m", "flask", "run", "--host=0.0.0.0", "--port=4567" ]

