## Adopted from https://github.com/wbotelhos/how-to-create-a-http-server-with-elixir

FROM elixir:1.19.2-slim@sha256:85a707f5e4b8df9826cd8af5c724c3ca4952cca341eaba7e1f3a79791cf17f4f

WORKDIR /app

# Copy the source code into the image for building
COPY internal/test/integration/components/elixir .

# Install dependencies
RUN mix do deps.get, compile

EXPOSE 4000

# Run the node app
CMD [ "mix", "run", "--no-halt" ]
