# Base Image
FROM ubuntu:22.04

# Set environment to non-interactive
ENV DEBIAN_FRONTEND=noninteractive

# Update and install required packages
RUN apt-get update && \
    apt-get install -y nginx mariadb-server supervisor && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Create a simple web page
RUN echo '<!doctype html><html><body><h1>Activity 11 Container</h1><p>Web and Database Server running in one container.</p></body></html>' > /var/www/html/index.html

# Setup MariaDB initial configuration
RUN service mysql start && \
    mysql -e "UPDATE mysql.user SET plugin = 'mysql_native_password' WHERE User = 'root'; FLUSH PRIVILEGES;" || true

# Expose HTTP and MySQL ports
EXPOSE 80 3306

# Copy supervisord configuration file
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Set Supervisor to run on container start
CMD ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisor/conf.d/supervisord.conf"]

