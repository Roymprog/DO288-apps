# Use the httpd-parent image as base
FROM quay.io/redhattraining/httpd-parent

# Expose port 8080, lower than 1024 not allowed
EXPOSE 8080
# Add Kuberenetes and Openshift labels
LABEL io.openshift.expose-services="8080:http" \ 
      io.k8s.description="A basic Apache HTTP Server child image, uses ONBUILD" \ 
      io.k8s.display-name="Apache HTTP Server" \ 
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="apache, httpd"
# Replace port exposure in apache server config
RUN sed -i "s/Listen 80/Listen 8080/g" /etc/httpd/conf/httpd.conf

# Assign all read and write files to group id 0, assume all files are root files for Openshift
RUN chgrp -R 0 /var/log/httpd /var/run/httpd && \ 
    chmod -R g=u /var/log/httpd /var/run/httpd

# Omit using root user
USER 1001
