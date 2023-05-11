FROM node:18.12.1-slim as base
WORKDIR /app
COPY . .
EXPOSE 5000

FROM base as dev
ENV NODE_ENV=development
RUN npm ci
RUN mv node_modules /node_modules
CMD ["npm", "run", "dev"]

FROM base as production
ENV NODE_ENV=production
ENV npm_config_cache=/tmp
RUN npm ci --omit=dev
RUN chown -R 1000:1000 "/tmp"
USER node
CMD ["npm", "start"]