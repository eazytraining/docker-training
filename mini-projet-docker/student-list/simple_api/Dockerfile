FROM python:2.7-buster
LABEL maintainer="Aurelie Kamgang" email="toto@admin.fr"
RUN apt update -y && apt install python-dev python3-dev libsasl2-dev python-dev libldap2-dev libssl-dev -y
RUN pip install flask==1.1.2 flask_httpauth==4.1.0 flask_simpleldap python-dotenv==0.14.0
COPY student_age.py /
VOLUME /data
EXPOSE 5000
CMD [ "python", "./student_age.py" ]
