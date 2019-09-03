# Use a lighter version of Node as a parent image
FROM mhart/alpine-node:8.11.4

# Set the working directory to /api
WORKDIR /api

# Address the error of RUN /wait-for-it.sh api_1 | env: can't execute 'bash': No such file or directory.  See https://stackoverflow.com/questions/40944479/how-to-use-bash-with-an-alpine-based-docker-image/40944512 
RUN apk add --no-cache bash

# https://github.com/vishnubob/wait-for-it/issues/57
COPY wait-for-it.sh /wait-for-it.sh
RUN chmod +x /wait-for-it.sh

# copy package.json into the container at /api
COPY package*.json /api/

# install dependencies
RUN npm install

# Copy the current directory contents into the container at /api
COPY . /api/

# Make port 80 available to the world outside this container
EXPOSE 80

# Run the app when the container launches
CMD node ./bin/www