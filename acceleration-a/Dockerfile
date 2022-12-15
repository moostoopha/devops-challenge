FROM node:10.14.2-alpine

#workdir
WORKDIR /acc-a

# Copy package.json and package-lock.json
ADD . /acc-a

# setup yarn  production packages 
RUN yarn install && \
    yarn build

ENV NODE_ENV production
ENV PORT 3002

EXPOSE 3002

CMD [ "yarn", "start" ]
