# 构建容器,使用版本: golang:1.16
FROM golang:1.18-alpine AS builder

ENV GO111MODULE=on \
    CGO_ENABLED=0 \
    GOOS=linux \
    GOARCH=amd64 \
    GOPROXY=https://goproxy.cn,direct

WORKDIR /publish
COPY . .
RUN go build -ldflags="-s -w" -o app .
# 最终容器, 基础镜像alpine 中包含 tini
FROM kubelilin/apline:tini-3.16.2 as production

COPY --from=builder /publish/app /
COPY --from=builder /publish/config_test.yml /config_dev.yml
# Run
CMD ["/app"]