FROM node:18.12.1-slim as sources
WORKDIR /app
COPY . .

FROM sources as dev
ENV NODE_ENV=development
ENV NG_CLI_ANALYTICS=ci
RUN npm ci
CMD ["npm", "run", "dev"]

FROM sources as build
ENV NG_CLI_ANALYTICS=ci
RUN npm ci && npm run build

FROM nginx:1.22-alpine as production
COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=build /app/dist/result-ui/ /usr/share/nginx/html/
EXPOSE 80
