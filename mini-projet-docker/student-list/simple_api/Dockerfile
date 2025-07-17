FROM python:3.11-slim
LABEL maintainer="EAZYTraining" email="contact@eazytraining.fr"
COPY requirements.txt student_age.py /
RUN apt update -y && apt install python3-dev libsasl2-dev libldap2-dev libssl-dev gcc build-essential -y
RUN pip install -r /requirements.txt
VOLUME /data
EXPOSE 5000
CMD [ "python3", "./student_age.py" ]
