# syntax=docker/dockerfile:1

FROM node:20-alpine as libreria-fe-builder

RUN apk update
RUN apk add git
RUN git clone https://github.com/Nidala96/Libreria-front-end.git
WORKDIR Libreria-front-end
RUN npm i
RUN npm run build

FROM nginx:1.25.3-alpine

ENV NODE_ENV production
ENV REACT_APP_LOCAL_URL http://192.168.1.2:8081/
COPY --from=libreria-fe-builder /Libreria-front-end/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
