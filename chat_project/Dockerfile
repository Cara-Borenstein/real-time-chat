FROM python:3.7.2

# Use nginx as proxy server to upgrade connections from http to ws
RUN apt-get update && apt-get install -y nginx

# Install python project requirements
ADD requirements.txt .
RUN pip3 install -r requirements.txt

# Create logging directories
RUN mkdir -p /var/log/supervisor && \
  mkdir -p /etc/supervisor/conf.d
RUN mkdir -p /var/log/nginx
RUN mkdir -p /var/log/asgi && \
  mkdir -p /var/log/wsgi

ARG ENVIRONMENT
ENV ENVIRONMENT=prod

# Use /code directory as work directory
RUN mkdir /code
ADD . /code/
WORKDIR /code/

ADD supervisor.conf /etc/supervisor/conf.d/supervisor.conf
ADD nginx-docker-proxy.conf /etc/nginx/conf.d/nginx-docker-proxy.conf

EXPOSE 8080

ENTRYPOINT ["sh", "start_app.sh"]
