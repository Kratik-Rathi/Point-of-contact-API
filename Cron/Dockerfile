FROM ubuntu:latest

# Install necessary packages
RUN apt-get update && apt-get -y install cron tzdata curl vim logrotate

ENV TZ=America/Indiana/Indianapolis

# Create the log file to be able to run tail
RUN touch /var/log/cron.log

# Setup existing cron jobs
RUN echo "35 01 * * * curl http://127.0.0.1:5000/api/poc?repository_name=userrepo >> /var/log/cron.log" >> mycron
RUN echo "36 01 * * * curl http://127.0.0.1:5000/api/poc?product_name=marketingautomation >> /var/log/cron.log" >> mycron

# Install the cron jobs
RUN crontab mycron

# Remove the temporary file
RUN rm mycron

# Run the command on container startup
CMD cron && tail -f /var/log/cron.log
