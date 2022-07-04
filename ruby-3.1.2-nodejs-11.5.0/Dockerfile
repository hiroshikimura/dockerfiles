FROM ruby:3.1.2-buster
ARG UID=1000
ARG GID=1000
RUN groupadd -g $GID www && \
    useradd -m -s /bin/bash -u $UID -g $GID www
RUN apt-get update -qq && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    curl -fsSL https://deb.nodesource.com/setup_11.x | bash - && \
    apt-get install -y nodejs yarn

USER www
WORKDIR /home/www

