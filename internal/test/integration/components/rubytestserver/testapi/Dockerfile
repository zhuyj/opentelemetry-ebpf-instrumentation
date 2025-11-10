FROM ruby:3.4.7@sha256:88ce517a2537f1255e97d2b290b6460036dc7b19dfed751b2e6d140d1c1d14b5 AS builder

# Set the working directory to /build
WORKDIR /build

# Copy the source code into the image for building
COPY internal/test/integration/components/rubytestserver/testapi .

# Install Rails 
RUN gem install rails
RUN gem install bundler
RUN bundle install
RUN bundle exec rake app:update:bin
RUN bin/rails db:migrate

EXPOSE 3040

FROM ruby:3.4.7-slim@sha256:2de50c072bed1bdaf5e6b6c132fb2bc56f03700046ad95a515b4111203bf5034

WORKDIR /
COPY --from=builder /build .
COPY --from=builder /usr/local/bundle /usr/local/bundle

# Run the node app
CMD [ "rails", "server", "-p", "3040", "-b", "0.0.0.0" ]
