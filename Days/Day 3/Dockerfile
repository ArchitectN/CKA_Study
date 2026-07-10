# FROM (sets the base image)
FROM python:3.9-slim

# WORKDIR sets the working directory inside the Docker image. All subsequent commands will be executed in this directory.
# if the directory does not exist, it will be created.
WORKDIR /app


# ADD used to copy files from the host machine into the Docker image. In this case, it copies the appy.py file into the /app directory inside the image.
ADD appy.py appy.py


# RUN executes commands during the build process of the Docker image. It is used to install dependencies, set up the environment, and perform other tasks needed to prepare the image for running your application.
RUN pip install flask

# EXPOSE for documentation purposes only
EXPOSE 5000


# CMD specifies the command to run when a container is started from the image. In this case, it runs the Flask application using Python.
CMD ["python", "appy.py"]

