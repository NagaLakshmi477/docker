FROM almalinux:9
RUN dnf install nginx -y
RUN rm -rf /usr/share/nginx/html/index.html
ADD https://github.com/NagaLakshmi477/ansible/blob/main/notes.md  /usr/share/nginx/html/index.html
# we need to give read acess
RUN chmod+r /usr/share/nginx/html/index.html
CMD [ "nginx", "-g" ,"daemon off ;"]