FROM almalinux:9
RUN dnf install nginx -y
RUN rm -rf /usr/share/nginx/html/index.html
ADD https://github.com/NagaLakshmi477/ansible/blob/main/01-playbook.yaml rm -rf  /usr/share/nginx/html/index.html
CMD [ "nginx", "-g" ,"daemon off ;"]