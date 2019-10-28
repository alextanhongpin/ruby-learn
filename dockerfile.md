# Dockerfile

```dockerfile
FROM ruby:2.6.5-alpine3.10

# ruby-dev is required by Rails 5.
ARG BUILD_PACKAGES="ruby-dev build-base curl-dev git openssl bash"
ARG DEV_PACKAGES="postgresql-dev"
ARG RUBY_PACKAGES="tzdata"

COPY Gemfile* /app/
VOLUME /app

RUN apk update && apk upgrade 
RUN apk --update add --virtual $BUILD_PACKAGES $DEV_PACKAGES $RUBY_PACKAGES && \    
    gem install bundler && cd /app && \
    bundle install

WORKDIR /app

COPY . .

RUN chown -R nobody:nogroup /app /etc/pki/tls/certs
USER nobody

EXPOSE 3000

# Prefer to run this as a command, in case we need to run sidekiq or something else.
# CMD ["bundle", "exec", "rails", "s", "-p", "3000", "-b", "0.0.0.0"]
# CMD ["bundle", "exec", "sidekiq"]
# CMD ["rails", "server", "-b", "0.0.0.0", "--port", "3000"]
```


## Possible commands
```
$ docker run --env-file=.env.development -p 3000:3000 rails/api:latest
$ @docker run --env-file=.env.development -p 3000:3000 rails/api:latest rails server -b 0.0.0.0 --port 3000
$ docker run --env-file .env.development -p 3000:3000 rails-api:latest bundle exec puma -C config/puma.rb -b tcp://0.0.0.0:3000
```
