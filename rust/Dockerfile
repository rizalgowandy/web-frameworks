FROM rust:1.37

WORKDIR /usr/src/app

RUN apt -y update && \
    apt -y install musl-tools

RUN rustup target add x86_64-unknown-linux-musl


COPY Cargo.toml ./
COPY src src

RUN cargo install
ENV RUSTFLAGS "-C target-cpu=native" 
RUN cargo build --target x86_64-unknown-linux-musl --release

FROM alpine    
COPY --from=0 /usr/src/app/target/x86_64-unknown-linux-musl/release/server /usr/src/app/target/x86_64-unknown-linux-musl/release/server
CMD /usr/src/app/target/x86_64-unknown-linux-musl/release/server