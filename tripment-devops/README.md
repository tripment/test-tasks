# Тестовое задание Tripment

## Docker

В Трипменте все завернуто в Докер. В этом тестовом задании предлагается улучшить Dockerfile для Ruby on Rails проекта. Этот Докерфайл используется везде: в локальной разработке, в CI и в продакшне. Что в этом конфиге не так? Что можно улучшить?
        
```dockerfile
ARG RUBY_VERSION
FROM ruby:${RUBY_VERSION}
WORKDIR /app
COPY . /app/
RUN apt-get update -qq && \
	apt-get -yq install libpq-dev nodejs
RUN curl -sL https://deb.nodesource.com/setup_14.15.4.x | bash - && \
    curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update -qq && apt-get -yq install yarn
RUN yarn install
RUN yarn build
RUN bundle install
RUN rails assets:precompile
```
