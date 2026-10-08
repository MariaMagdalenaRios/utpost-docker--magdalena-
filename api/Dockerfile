FROM node:24-alpine
WORKDIR /app

COPY package.json package-lock.json ./
COPY shared/package.json shared/
COPY api/package.json api/
COPY client/package.json client/
COPY web/package.json web/
RUN npm ci

COPY shared/ shared/
COPY api/ api/

EXPOSE 4000
CMD ["npm", "start", "--workspace=api"]