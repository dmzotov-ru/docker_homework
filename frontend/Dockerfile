FROM node:15-alpine AS build
ENV PATH /app/docker_homework/node_modules/.bin:$PATH
WORKDIR /app
RUN apk update && apk add git
RUN git clone https://github.com/dmzotov-ru/docker_homework.git
RUN cd docker_homework/frontend && npm install --only=prod
RUN cd docker_homework/frontend && npm run build


FROM nginx:alpine AS runtime
WORKDIR /usr/share/nginx/html
COPY --from=build /app/docker_homework/frontend/build ./
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx/nginx.conf /etc/nginx/conf.d
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
