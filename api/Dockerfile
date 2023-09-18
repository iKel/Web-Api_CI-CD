FROM node:16

WORKDIR /app

# copy list of packages
COPY package.json package-lock.json ./
# install packages based on the package list file
RUN npm install

# copy all the app source code
COPY ./ ./

ENV PORT=3000
EXPOSE 3000

# start the app when container launches
CMD npm start
