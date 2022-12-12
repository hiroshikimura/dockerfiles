FROM ruby:3.1.2-bullseye as nodejs

WORKDIR /tmp
RUN curl -LO https://nodejs.org/dist/v14.17.4/node-v14.17.4-linux-x64.tar.xz && \
    tar xvf node-v14.17.4-linux-x64.tar.xz && \
    mv node-v14.17.4-linux-x64 node

FROM ruby:3.1.2-bullseye

COPY --from=nodejs /tmp/node /opt/node
ENV PATH /opt/node/bin:$PATH

RUN useradd -m -u 1000 web && \
    mkdir /app && \
    chown web /app

USER web

RUN curl -o- -L https://yarnpkg.com/install.sh | bash
ENV PATH /home/web/.yarn/bin:/home/web/.config/yarn/global/node_modules/.bin:$PATH

RUN gem install bundler

WORKDIR /app
COPY --chown=web Gemfile Gemfile.lock package.json yarn.lock /app/
RUN bundle install && \
    yarn install

COPY --chown=web . /app/

RUN bin/rails assets:precompile

VOLUME /app/public

# CMD ["bin/rails", "s", "-b", "0.0.0.0", "--port", "3000"]

