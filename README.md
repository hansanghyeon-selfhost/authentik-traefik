
## authentik

authentik란?

인증을 아주 간편하게 만들어줍니다.

왜 이것을 사용하는가? 무수히 selfhost 서비스들이있고 각 서비스마다 모두 auth 기능을 추가할수없습니다. authentik를 통해서 인증을 아주 간편하게 넣을 수 있습니다.

## install

### 1. traefik config 설정

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

### 2. git clone

```sh
git clone ...
```

```sh
cp .env.example .env
```

```sh
docker-compose up -d
```

### 3. 초기설정

설정한 도메인에 접속해서 뒤에 `/if/flow/initial-setup`로 접속하여 초기 관리자 계정을 만든다.

## 참고

필수시청

- https://www.youtube.com/watch?v=CPURnYaW3Zk

### docker-compose

필독

- https://goauthentik.io/docs/installation/docker-compose

[다운로드 docker-compose](https://goauthentik.io/docker-compose.yml)

설치는 모두 docs 기준으로하고 여기에 traefik 연동을 추가합니다.
