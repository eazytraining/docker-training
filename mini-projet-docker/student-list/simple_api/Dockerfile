ARG VERSION="3.8-buster"
FROM python:$VERSION
LABEL maintainer="EAZYTraining" email="contact@eazytraining.fr"
RUN apt update -y && apt install python3-dev libsasl2-dev libldap2-dev libssl-dev -y 
COPY requirements.txt student_age.py /
RUN pip3 install -r /requirements.txt
VOLUME /data
EXPOSE 5000
CMD [ "python3", "./student_age.py" ]