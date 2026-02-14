FROM node:20.19.5-alpine3.21 AS build
WORKDIR /opt/server
COPY *.js .
COPY package.json .
RUN npm install

FROM node:20.19.5-alpine3.21
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
EXPOSE 8080
LABEL com.project="roboshop" \
      component="user" \
      created_by="shiva kumar"
ENV REDIS_URL="redis://redis:6379" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
COPY --from=build --chown=roboshop:roboshop /opt/server . 
CMD ["server.js"]
ENTRYPOINT ["node"]


# FROM node:20
# WORKDIR /opt/server
# COPY *.js .
# COPY package.json .
# RUN npm install
# ENV REDIS_URL="redis://redis:6379" \
#     MONGO_URL="mongodb://mongodb:27017/catalogue"
# CMD ["node","server.js"]