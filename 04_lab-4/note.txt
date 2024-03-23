# Creating a volume type

  docker volume create --name share
  docker volume ls

# Create two ubuntu containers (ubuntu1 and ubuntu2) and mount the volume created in the /tmp directory of each ubuntu container.
 
  docker run -it --name ubuntu1 -v share:/tmp -d ubuntu /bin/bash
  docker run -it --name ubuntu2 -v share:/tmp -d ubuntu /bin/bash

# Create a toto.txt file in the /tmp directory of the ubuntu1 container and check that it is present in the /tmp directory of the ubuntu2 container.

  docker exec -it ubuntu1 /bin/bash
  cd /tmp
  touch toto.txt
  exit
  docker exec -it ubuntu2 /bin/bash
  ls /tmp
  echo "eazytraining is the best"> /tmp/toto.txt

  docker exec -it ubuntu1 /bin/bash
  cat /tmp/toto.txt

# Remove ubuntu1 and restore it

  docker rm -f ubuntu1
  docker run -it --name ubuntu1-restore -v share:/tmp -d ubuntu /bin/bash
  docker exec -it ubuntu1-restore /bin/bash
  cat /tmp/toto.txt

# Deploy the web server by customizing the application code

  git clone https://github.com/diranetafen/static-website-example.git
  docker run --name webserver -p 80:80 -d -v ${PWD}/static-website-example:/usr/local/apache2/htdocs/ httpd
  vi static-website-example/index.html
  docker restart webserver
