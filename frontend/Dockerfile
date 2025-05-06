FROM node:18.20.3 as builder
#FROM  node:16.14.2 as builder
#FROM node:12.20 as builder
RUN apt-get update && npm cache clear --force
RUN npm install -g @angular/cli
#RUN node --version && npm --version && ng --version

RUN mkdir -p /home/node
WORKDIR /home/node/
RUN ls -l 
RUN pwd
COPY frontend-code .
#COPY fronted-code .
#COPY File-Maker-System-FE .
#RUN chmod -R 775 /home/node
#RUN chmod -R 775 /home/node/web-frontend
RUN ls -l
#RUN npm install --legacy-peer-deps
RUN npm install -f
RUN ng build
#RUN chmod -R 775 /home/node

# => Run container
FROM nginx:1.15.2-alpine as release
# Nginx config
RUN rm -rf /etc/nginx/nginx.conf
RUN rm -rf /etc/nginx/conf.d
COPY nginx.conf /etc/nginx/nginx.conf

## Remove default nginx index page
RUN rm -rf /var/www/*

# Static build
COPY --from=builder /home/node/dist/ /var/www/

# Default port exposure
EXPOSE 80
