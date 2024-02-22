# Dockerfile

# **********
# base stage para contenedor de productivo, alpine es por Entrypoint
# **********

# FROM node:20.9.0-alpine AS base

# WORKDIR /app

# # Install AWS CLI and Amplify CLI
# RUN apk update && \
#     apk add --no-cache \
#     python3 \
#     py-pip \
#     groff \
#     less \
#     && pip install --upgrade pip \
#     && pip install awscli \
#     && npm install -g @aws-amplify/cli
    
# modo desarrollo    
FROM node:20.9.0 AS base

WORKDIR /app

RUN apt-get update \
    && apt-get install -y git curl xdg-utils \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip
RUN ./aws/install

RUN aws configure set region "us-east-2"
RUN aws configure list

# Instalar el CLI de Amplify
RUN npm install -g @aws-amplify/cli    
# RUN amplify env set _CUSTOM_IMAGE=$_CUSTOM_IMAGE
# RUN amplify env set _LIVE_UPDATES=$_LIVE_UPDATES

# **********
# deps stage
# **********
FROM base AS deps

# Copy package.json to /app
# COPY package*.json /app/

# Disable the telementary
ENV NEXT_TELEMETRY_DISABLED 1

# ***********
# inter stage
# ***********
FROM deps AS inter

# Copy all other files excluding the ones in .dockerignore
COPY . /app

# exposing the port
EXPOSE 3000

# **********
# prod stage
# **********
FROM inter AS prod

RUN npm run build

CMD ["npm", "start"]

# **********
# dev stage
# **********
FROM inter AS dev
# Instal dependencies according to the lockfile
# # Instal dependencies according to the lockfile

CMD ["npm", "run", "dev"]