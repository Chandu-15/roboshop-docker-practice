FROM python:3.9 AS build 
WORKDIR /opt/server
RUN apk add --no-cache \
    build-base \
    linux-headers \
    pcre-dev
COPY requirements.txt .
RUN pip3 install -r requirements.txt --prefix=/install


FROM python:3.9.25-alpine3.21
WORKDIR /opt/server
EXPOSE 8080
LABEL com.project="roboshop" \
      component="catalogue" \
      created_by="shiva kumar"
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"
COPY --from=build /install /usr/local
COPY --chown=roboshop:roboshop payment.ini *.py .
ENTRYPOINT ["sh","-c","sleep 30 && uwsgi --ini payment.ini"]



# FROM python:3.9
# WORKDIR /opt/server
# COPY payment.ini .
# COPY *.py .
# COPY requirements.txt .
# RUN pip3 install -r requirements.txt
# ENV CART_HOST="cart" \
#     CART_PORT="8080" \
#     USER_HOST="user" \
#     USER_PORT="8080" \
#     AMQP_HOST="rabbitmq" \
#     AMQP_USER="roboshop" \
#     AMQP_PASS="roboshop123"
# CMD ["uwsgi","--ini","payment.ini"]