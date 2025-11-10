# Build the testserver binary
# Docker command must be invoked from the projec root directory
FROM golang:1.25@sha256:6ca9eb0b32a4bd4e8c98a4a2edf2d7c96f3ea6db6eb4fc254eef6c067cf73bb4 AS builder

ARG TARGETARCH

ENV GOARCH=$TARGETARCH

WORKDIR /src

# Copy the go manifests and source
COPY go.mod go.mod
COPY go.sum go.sum
COPY gosql.go gosql.go

# Build
RUN go mod download
RUN go build -o gosql gosql.go

# Create final image from minimal + built binary
FROM debian:bookworm-slim@sha256:936abff852736f951dab72d91a1b6337cf04217b2a77a5eaadc7c0f2f1ec1758

WORKDIR /
COPY --from=builder /src/gosql .
USER 0:0

CMD [ "/gosql" ]