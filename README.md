
## authentik

authentik란?

인증을 아주 간편하게 만들어줍니다.

왜 이것을 사용하는가? 무수히 selfhost 서비스들이있고 각 서비스마다 모두 auth 기능을 추가할수없습니다. authentik를 통해서 인증을 아주 간편하게 넣을 수 있습니다.

## using

`traefik-anthentik.yaml` 파일을 traefik rules 파일로 이동한다.

```yaml
services:
  app:
    networks:
      - traefik_proxy
      - default
    labels:
      - traefik.enable=true
      ## HTTP Routers
      - traefik.http.routers.${SERVICE}.rule=Host(`${DOMAIN}`)
      - traefik.http.routers.${SERVICE}.entrypoints=https
      - traefik.http.routers.${SERVICE}.tls.certresolver=leresolver
      ## Service
      - traefik.http.services.${SERVICE}.loadbalancer.server.port=3000
      - traefik.http.routers.${SERVICE}.middlewares=authentik@file
```

사용하려는 앱에서 traefik label에서 미들웨어로 추가한다.

## 참고

필수시청

- https://www.youtube.com/watch?v=CPURnYaW3Zk

### docker-compose

필독

- https://goauthentik.io/docs/installation/docker-compose

[다운로드 docker-compose](https://goauthentik.io/docker-compose.yml)

설치는 모두 docs 기준으로하고 여기에 traefik 연동을 추가합니다.
