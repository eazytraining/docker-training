FROM nginx:alpine
LABEL maintainer="Eazytraining <contact@eazytraining.fr>" \
      description="Serveur Nginx pour le site static"
COPY static-website-example/ /usr/share/nginx/html/
EXPOSE 80
ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
