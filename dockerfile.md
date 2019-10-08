# Dockerfile

```dockerfile
FROM ruby:2.2.10

RUN apt-get update && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /usr/src/app
ENV RAILS_ENV=development

COPY Gemfile* ./
RUN bundle install
COPY . .

EXPOSE 3000
CMD ["rails", "server", "-b", "0.0.0.0"]
```

```dockerfile
FROM ruby:2.2.10-alpine

ARG BUILD_PACKAGES="build-base curl-dev git openssl"
ARG DEV_PACKAGES="postgresql-dev"
ARG RUBY_PACKAGES="tzdata"

RUN apk update \
    && apk upgrade \
    && apk add --update --no-cache $BUILD_PACKAGES $DEV_PACKAGES $RUBY_PACKAGES

WORKDIR /usr/src/app
ENV RAILS_ENV=production

COPY Gemfile* ./

RUN bundle config --global frozen 1 && bundle install

COPY . .

EXPOSE 3000
CMD ["rails", "server", "-b", "0.0.0.0"]
```

```dockerfile
FROM ruby:2.6.5-alpine3.10

ARG BUILD_PACKAGES="build-dependencies build-base ruby-dev openssl-dev libxml2-dev libxslt-dev postgresql-dev libc-dev linux-headers nodejs tzdata git"

COPY Gemfile* /app/

RUN apk --update add --virtual $BUILD_PACKAGES && \    
    gem install bundler && cd /app && \
    bundle config build.nokogiri --use-system-libraries && bundle install --without development test


WORKDIR /app

COPY . .

ENV RAILS_ENV=production
ENV NODE_ENV=production

RUN chown -R nobody:nogroup /app
USER nobody

CMD ["rails", "s", "-p", "8080"]
```
