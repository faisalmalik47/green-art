FROM node:18
WORKDIR /app
RUN apt-get update && apt-get install -y \
    python3 \
    build-essential

COPY package.json package-lock.json ./
RUN npm install --force
COPY . .
RUN npm run build
EXPOSE 7000
CMD ["npm", "run", "start"]