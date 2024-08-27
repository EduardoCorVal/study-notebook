# Base Image
FROM python:3-alpine3.15
# Define work directory
WORKDIR /app
# Copy information (All (.) to /app)
COPY . /app
# Commands to set up the enviroment
RUN pip install -r requirements.txt
# Expose the port
EXPOSE 3000
# Run the commands. In this case, run the python file
CMD python ./index.py
