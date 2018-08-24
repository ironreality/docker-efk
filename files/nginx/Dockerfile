FROM nginx

# htpasswd generation
ARG HTTP_AUTH_LOGIN
ARG HTTP_AUTH_PASS
RUN apt-get update && apt-get install openssl \
&& echo -n ${HTTP_AUTH_LOGIN:-admin}:$(openssl passwd -apr1 ${HTTP_AUTH_PASS:-admin}) > /etc/nginx/.htpasswd
