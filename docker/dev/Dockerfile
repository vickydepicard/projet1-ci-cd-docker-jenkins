FROM nginx:alpine

COPY docker/dev/nginx/default.conf /etc/nginx/conf.d/default.conf
COPY src/ /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

