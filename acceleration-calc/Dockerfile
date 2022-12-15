FROM node:10.14.2-alpine

#workdir
WORKDIR /code

# Copy package.json and package-lock.json
ADD . /code

# setup yarn  production packages 
RUN yarn install && \
    yarn build


ENV NODE_ENV production
ENV PORT 3000

EXPOSE 3000

CMD [ "yarn", "start" ]
