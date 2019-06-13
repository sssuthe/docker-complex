FROM node:alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx
#nginx will run on port 3000, this is also where the routing nginx will be looking for this
EXPOSE 3000
#get the default config for nginx and place it in its final spot on the server
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
#copy the rest of the production assets from the builder phase above and place them in the web directory
COPY --from=builder /app/build /usr/share/nginx/html
