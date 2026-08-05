FROM node:18-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY tsconfig.json knexfile.ts ./
COPY src ./src

RUN npm run build

FROM node:18-alpine AS runtime

WORKDIR /app

ENV NODE_ENV=production

COPY package*.json ./
RUN npm install --omit=dev --ignore-scripts

COPY --from=build /app/dist ./dist

EXPOSE 3333

CMD ["npm", "start"]