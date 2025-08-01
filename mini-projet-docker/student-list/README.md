# Student List

This repository contains a simple application designed to display a list of students through a web server (PHP) and an API (Flask).

![Project](https://user-images.githubusercontent.com/18481009/84582395-ba230b00-adeb-11ea-9453-22ed1be7e268.jpg)

---

## Objectives

This practice exam aims to evaluate your capability to manage Docker infrastructure. You will be assessed on the following skills:

### Themes

- Improving the existing application deployment process.
- Versioning infrastructure releases.
- Adhering to best practices for Docker infrastructure implementation.
- Infrastructure as Code (IaC).

## Context

**POZOS** is an IT company based in France that develops software for high schools.

The innovation department aims to modernize its existing infrastructure to ensure scalability and easy deployment through maximum automation.

POZOS requires a **Proof of Concept (POC)** demonstrating Docker’s efficiency and agility.

Currently, the application runs on a single server without scalability or high availability. Deployments often encounter issues. Therefore, POZOS seeks enhanced agility for its software infrastructure.

## Infrastructure

For this POC, you will use a single machine with Docker installed. Both the build and deployment processes will occur on this machine.

POZOS recommends Ubuntu 20.04, the most commonly used OS in the company. You may use an Ubuntu 20.04-based virtual machine instead of your physical machine.

Security is critical for POZOS DSI; therefore, do not disable the firewall or any other security mechanisms unless explicitly justified in your delivery.

## Application

You will work with the application **student_list**, a basic app used by POZOS to display students' names along with their ages.

The application consists of two modules:

- **REST API:** Requires basic authentication and returns the list of students based on a JSON file.
- **Web Application:** Written in HTML and PHP, allowing end-users to view the list of students.

Your task is to containerize each module separately and enable communication between them.

Application source code: [student-list GitHub repository](https://github.com/diranetafen/student-list.git)

### Required Files

You must deliver the following files:

- **Dockerfile** (initially empty)
- **docker-compose.yml** (initially empty)

### File Descriptions:

- **docker-compose.yml:** Deploys both the API and the web application.
- **Dockerfile:** Builds the API image.
- **requirements.txt:** Lists all packages required by the API.
- **student_age.json:** Contains student names and ages in JSON format.
- **student_age.py:** Python API source code.
- **index.php:** PHP page allowing end-users to access the student list. Update the following line with your API deployment details before running the container:

```php
$url = 'http://<api_ip_or_service_name:port>/pozos/api/v1.0/get_student_ages';
```

## Build and Test (7 Points)

POZOS provides instructions to build the API container:

- **Base Image:** Use `python:3.11-slim`.
- **Maintainer:** Include maintainer information in your Dockerfile.
- **Source Code:** Copy the API source code to the root directory `/` inside the container.
- **Prerequisites:** The API uses Flask and requires additional packages. Install them using:

```bash
apt update -y && apt install -y python3-dev libsasl2-dev libldap2-dev libssl-dev
```

Copy `requirements.txt` to `/` and install packages:

```bash
pip3 install -r /requirements.txt
```

- **Persistent Data:** Create a `/data` folder as a volume for storing student data. Mount `student_age.json` here.
- **API Port:** Expose port 5000.
- **CMD:** Run `student_age.py` on container start:

```Dockerfile
CMD ["python3", "./student_age.py"]
```

Build and test the container. Confirm the API is responsive by executing:

```bash
curl -u toto:python -X GET http://<host_ip>:5000/pozos/api/v1.0/get_student_ages
```

Take a screenshot for the delivery.

**Congratulations! Proceed to the docker-compose step.**

## Infrastructure as Code (5 Points)

After testing the API, deploy the application using `docker-compose.yml`:

Deploy two services:

- **website**:
  - Image: `php:apache`
  - Environment: Set `USERNAME` and `PASSWORD` to access the API (USERNAME=toto ; PASSWORD=python).
  - Volume: Bind local `./website` directory to `/var/www/html`.
  - Dependency: Ensure it starts after the API service.
  - Expose the required port.

- **api**:
  - Use the previously built image.
  - Mount `student_age.json` to `/data/student_age.json`.
  - Expose port 5000.
  - Use a dedicated Docker network for communication.

Clean up previous containers, run `docker-compose.yml`, and test by accessing the web interface. Click "List Student" and take a screenshot if successful.

**Congratulations! You've successfully dockerized the POZOS application.**

## Docker Registry (4 Points)

Deploy a private Docker registry:

- Docker [registry](https://docs.docker.com/registry/)
- Web [interface](https://hub.docker.com/r/joxit/docker-registry-ui/) or [Portus](http://port.us.org/)

Push your built images to the registry and include screenshots in your delivery.

## Delivery (4 Points)

Your delivery must include a repository link containing:

- A `README.md` with screenshots and detailed explanations.
- Configuration files (`docker-compose.yml` and `Dockerfile`).

Your delivery will be evaluated on:

- Quality of explanations
- Quality of screenshots (clarity and relevance)
- Presentation quality
- Repository structure

Send your delivery link to **contact@eazytraining.fr** to receive the solution link.


📌 **Useful Resource:**

To perform this exercise in a standardized environment, you can use the following Vagrant stack provided by Eazytraining:

🔗 [Vagrant Stack with Docker](https://github.com/diranetafen/cursus-devops/tree/master/vagrant/docker)



![Good luck!](https://user-images.githubusercontent.com/18481009/84582398-cad38100-adeb-11ea-95e3-2a9d4c0d5437.gif)

