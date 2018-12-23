from node:alpine
WORKDIR /app
COPY ./package.json ./
RUN npm install

COPY . .
RUN npm run build

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_ID" --password-stdin

COPY --from=builder /app/build /usr/share/nginx/html
