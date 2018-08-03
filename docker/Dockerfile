FROM maven:3-alpine

RUN apk add --update nodejs-current nodejs-npm

RUN npm install apigeetool -g \
    && npm install openapi2apigee -g

RUN apk update && \
    apk add --no-cache ansible && \
    rm -rf /tmp/* && \
    rm -rf /var/cache/apk/*