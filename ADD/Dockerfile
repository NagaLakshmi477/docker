FROM almalinux:9
RUN dnf install nginx -y
# remove old index file
RUN rm -rf /usr/share/nginx/html/index.html
ADD https://github.com/NagaLakshmi477/docker/blob/main/README.md /usr/share/nginx/html/index.html
RUN chmod +r /usr/share/nginx/html/index.html
ADD sample-1.tar /tmp/
CMD [ "nginx","-g","daemon off ;" ]