FROM caddy:2-builder AS builder
RUN xcaddy build \
    --with https://github.com/mholt/caddy-l4

FROM caddy:2-alpine
COPY --from=builder /usr/bin/caddy /usr/bin/caddy