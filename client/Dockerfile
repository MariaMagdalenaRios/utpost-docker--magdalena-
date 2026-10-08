FROM node:24-alpine
WORKDIR /app

COPY package.json package-lock.json ./
COPY shared/package.json shared/
COPY api/package.json api/
COPY client/package.json client/
COPY web/package.json web/
RUN npm ci

COPY shared/ shared/
COPY client/ client/

EXPOSE 3001
CMD ["npm", "run", "dev", "--workspace=client", "--", "--host", "0.0.0.0"]