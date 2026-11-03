# Derper_Server

[![GitHub](https://img.shields.io/badge/GitHub-W0n9%2Fderper__server-181717?logo=github)](https://github.com/W0n9/derper_server)
[![Docker Hub](https://img.shields.io/badge/Docker%20Hub-w0n9%2Fderper__server-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/w0n9/derper_server)
[![Tailscale](https://img.shields.io/badge/Tailscale-tailscale%2Ftailscale-4D4D4D?logo=tailscale)](https://github.com/tailscale/tailscale/tree/main/cmd/derper)

Tailscale's self-hosted DERP-server docker image, built from [tailscale/cmd/derper](https://github.com/tailscale/tailscale/tree/main/cmd/derper).

## Links

- GitHub: https://github.com/W0n9/derper_server
- Docker Hub: https://hub.docker.com/r/w0n9/derper_server
- Tailscale DERP (derper) 源码仓库: https://github.com/tailscale/tailscale/tree/main/cmd/derper
- 官方自建 DERP 文档: https://tailscale.com/kb/1118/custom-derp-servers/

# Setup

> required: set env `DERP_DOMAIN` to your domain

```bash
docker run -e DERP_DOMAIN=derper.your-domain.com -p 80:80 -p 443:443 -p 3478:3478/udp w0n9/derper_server:latest
```

# Docker Tags

`latest` 与 `master` 是可变 tag，内容随上游同步自动更新；部分 registry 镜像 / CDN / HTTP 代理可能按 tag 名缓存旧 manifest，导致拉到过期镜像。如遇缓存问题，请改用以下不可变 tag 固定版本：

| tag 格式                      | 示例                   | 说明                                   |
| ----------------------------- | ---------------------- | -------------------------------------- |
| `sha-<commit>`                | `sha-9c8a1f2`          | 按构建 commit 唯一，完全不可变         |
| `derper-<tailscale版本>`      | `derper-v1.104.4`      | 按内含的 derper（Tailscale）版本标识   |
| `v<semver>` / `v<major.minor>`| `v1.2.3` / `v1.2`      | 发布 tag（`v*.*.*` 触发构建时才有）    |
| `<branch>-amd64/-arm64`       | `master-amd64`         | 单架构镜像（多架构 manifest 由聚合 tag 提供） |

```bash
# 示例：固定到某次构建
docker pull w0n9/derper_server:sha-9c8a1f2
# 示例：固定到某个 derper 版本
docker pull w0n9/derper_server:derper-v1.104.4
```

| env                 | required | description                                                            | default value     |
| ------------------- | -------- | ---------------------------------------------------------------------- | ----------------- |
| DERP_DOMAIN         | true     | derper server hostname                                                 | your-hostname.com |
| DERP_CERT_DIR       | false    | directory to store LetsEncrypt certs(if addr's port is :443)           | /app/certs        |
| DERP_CERT_MODE      | false    | mode for getting a cert. possible options: manual, letsencrypt         | letsencrypt       |
| DERP_ADDR           | false    | listening server address                                               | :443              |
| DERP_STUN           | false    | also run a STUN server                                                 | true              |
| DERP_HTTP_PORT      | false    | The port on which to serve HTTP. Set to -1 to disable                  | 80                |
| DERP_VERIFY_CLIENTS | false    | verify clients to this DERP server through a local tailscaled instance | false             |

# Usage

Fully DERP setup offical documentation: https://tailscale.com/kb/1118/custom-derp-servers/
