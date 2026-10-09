FROM node:22-alpine
WORKDIR /app

COPY package.json package-lock.json ./
COPY shared/package.json shared/
COPY client/package.json client/
RUN npm ci --workspace=client

COPY shared/ shared/
COPY client/ client/
RUN npm run build --workspace=client


WORKDIR /app/client
EXPOSE 3001
CMD ["npm", "run", "preview", "--", "--host", "0.0.0.0", "--port", "3001"]
