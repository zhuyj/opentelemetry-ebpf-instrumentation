# Dockerfile that will build a container that runs rust ironssl HTTPS on port 8080
FROM rust:latest@sha256:a0dba1c1b2c90585fc44421b55ddf8063323760dc644ba1d35f5b389ad3e8e14
EXPOSE 8080
RUN mkdir -p /src
COPY src/main.rs /src/main.rs
COPY Cargo.toml /Cargo.toml
COPY Cargo.lock /Cargo.lock
COPY localhost.crt /localhost.crt
COPY localhost.key /localhost.key
COPY identity.p12 /identity.p12
RUN cargo build
CMD ["/target/debug/rust_ironssl"]