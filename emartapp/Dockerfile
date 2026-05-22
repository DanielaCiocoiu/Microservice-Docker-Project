FROM node:18-alpine AS ui-build
WORKDIR /usr/src/app
COPY client/ ./client/
RUN cd client && npm install && npm run build

FROM node:18-alpine AS server-build
WORKDIR /usr/src/app
COPY nodeapi/ ./nodeapi/
RUN cd nodeapi && npm install

FROM node:18-alpine
WORKDIR /usr/src/app/
COPY --from=server-build /usr/src/app/nodeapi/ ./
COPY --from=ui-build /usr/src/app/client/dist ./client/dist
RUN ls
EXPOSE 4200
EXPOSE 5000
CMD ["/bin/sh", "-c", "cd /usr/src/app/ && npm start"]
