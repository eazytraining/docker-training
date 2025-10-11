FROM nginx:alpine
LABEL maintainer="Eazytraining <contact@eazytraining.fr>" \
      description="Serveur Nginx pour le site static a partir d'un clone"
RUN apk update && apk add --no-cache git && \
    rm -rf /usr/share/nginx/html/* && \
    git clone https://github.com/diranetafen/static-website-example.git /usr/share/nginx/html/ && \
    apk del git 
EXPOSE 80
ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
