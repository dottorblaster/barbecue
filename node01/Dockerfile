FROM golang as agent-builder

RUN git clone https://github.com/trento-project/agent.git
RUN cd agent && make build

FROM rust as fakemall-builder

RUN git clone https://github.com/fabriziosestito/fakemall.git
WORKDIR /fakemall
RUN cargo build

FROM debian
COPY --from=agent-builder /go/agent/trento-agent /usr/bin/trento-agent
COPY --from=fakemall-builder /fakemall/target/debug/fakemall /usr/bin/fakemall
COPY . /

ENTRYPOINT ["/usr/bin/trento-agent", "start"]
