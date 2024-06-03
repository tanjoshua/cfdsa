# Set the runtime
FROM node:22-bullseye

## BUILD the application
WORKDIR /app

# copy all sources into image
COPY package.json .
COPY package-lock.json .
COPY main.js .
COPY public public
COPY views views

# Install dependencies
RUN npm ci

## Run the application
ENV PORT=3000
EXPOSE ${PORT}

ENTRYPOINT node main.js