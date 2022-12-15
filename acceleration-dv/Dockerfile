FROM node:10.14.2-alpine

#workdir
WORKDIR /acc-dv

# Copy package.json and package-lock.json
ADD . /acc-dv

# setup yarn  production packages 
RUN yarn install && \
    yarn build

ENV NODE_ENV production
ENV PORT 3001

EXPOSE 3001

CMD [ "yarn", "start" ]

