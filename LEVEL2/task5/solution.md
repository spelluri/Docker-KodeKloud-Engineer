FROM ubuntu:24.04

# Install Apache2
RUN apt-get update && \
    apt-get install -y apache2 && \
    apt-get clean

# Change Apache to listen on port 8082
RUN sed -i 's/Listen 80/Listen 8082/' /etc/apache2/ports.conf && \
    sed -i 's/<VirtualHost \*:80>/<VirtualHost \*:8082>/' /etc/apache2/sites-available/000-default.conf

# Expose port 8082
EXPOSE 8082

# Start Apache in foreground
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
