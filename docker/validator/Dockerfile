FROM debian:buster-20220228@sha256:fd510d85d7e0691ca551fe08e8a2516a86c7f24601a940a299b5fe5cdd22c03a AS debian-base

FROM debian-base AS toolchain

# To use http/https proxy while building, use:
# docker build --build-arg https_proxy=http://fwdproxy:8080 --build-arg http_proxy=http://fwdproxy:8080

RUN apt-get update && apt-get install -y cmake curl clang git pkg-config libssl-dev libpq-dev

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --default-toolchain none
ENV PATH "$PATH:/root/.cargo/bin"

WORKDIR /aptos
COPY rust-toolchain /aptos/rust-toolchain
RUN rustup install $(cat rust-toolchain)

FROM toolchain AS builder

ARG ENABLE_FAILPOINTS
COPY . /aptos

RUN IMAGE_TARGET="release" ./docker/build-common.sh

### Production Image ###
FROM debian-base AS prod

RUN apt-get update && apt-get install -y libssl1.1 ca-certificates && apt-get clean && rm -r /var/lib/apt/lists/*

### Needed to run debugging tools like perf
RUN apt-get update && apt-get install -y linux-tools-4.19 sudo procps

RUN addgroup --system --gid 6180 aptos && adduser --system --ingroup aptos --no-create-home --uid 6180 aptos

RUN mkdir -p /opt/aptos/bin /opt/aptos/etc
# TODO(geekflyer): Probable dead code - consider removing the 2 lines as install-tools.sh is not executed and therefore probably obsolete.
COPY docker/validator/install-tools.sh /root
COPY --from=builder /aptos/target/release/aptos-node /opt/aptos/bin
COPY --from=builder /aptos/target/release/db-backup /opt/aptos/bin
COPY --from=builder /aptos/target/release/db-bootstrapper /opt/aptos/bin
COPY --from=builder /aptos/target/release/db-restore /opt/aptos/bin

# Admission control
EXPOSE 8000
# Validator network
EXPOSE 6180
# Metrics
EXPOSE 9101
# Backup
EXPOSE 6186

# Capture backtrace on error
ENV RUST_BACKTRACE 1

ARG BUILD_DATE
ARG GIT_REV
ARG GIT_UPSTREAM

LABEL org.label-schema.schema-version="1.0"
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vcs-ref=$GIT_REV
