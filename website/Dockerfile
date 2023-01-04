FROM devopsedu/webapp
ADD website /var/www/html
RUN rm /var/www/html/index.html
EXPOSE 8080
CMD [ "/usr/sbin/apache2ctl", "-D", "FOREGROUND" ]
