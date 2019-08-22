FROM ruby:alpine

MAINTAINER Carlos Melendez <kalolomagno@gmail.com>

RUN addgroup --g 1000 -S rubygroup
RUN adduser -SD -g "" -G rubygroup -u 1000 theuser
RUN adduser root rubygroup
RUN apk add --update build-base bash nodejs tzdata postgresql-dev postgresql-client libxslt-dev libxml2-dev yarn vim
RUN gem update --system
RUN gem install rails
WORKDIR /app
COPY Gemfile Gemfile.lock /app/
RUN bundle install
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000
CMD ["rails", "server", "-b", "0.0.0.0"]