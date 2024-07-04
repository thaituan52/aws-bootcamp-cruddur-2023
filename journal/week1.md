# Week 1 — App Containerization
*We gonna containerize the app using Docker which make other user of app who nothing to do with configurations and no need in compiling anything*

## Dockerfile on back-end (backend-flask/Dockerfile):
We have host OS (our comp) and guest OS (the container) which are seperate entities

```Dockerfile
FROM python:3.10-slim-buster

WORKDIR /backend-flask

COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY . .

ENV FLASK_ENV=development

EXPOSE ${PORT}
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]
```


## Reference and Settings:
_[VSCode Docker Extension](https://code.visualstudio.com/docs/containers/overview): will be used to make the syntax and appliance of Docker easier 
> (Gitpod is pre-installed with this)
