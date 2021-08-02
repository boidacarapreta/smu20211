# SMU 2021.1

Projeto de desenvolvimento de jogo Web com WebRTC para a disciplina de Sistemas Multimídia do Curso de Engenharia de Telecomunicações do IFSC câmpus São José

## Infraestrutura

O servidor `smu20211.sj.ifsc.edu.br` suporta o protocolo HTTP via NGINX. A configuração global do serviço está assim:

```nginx
# Virtual host smu20211.sj.ifsc.edu.br

server {
    if ($host = smu20211.sj.ifsc.edu.br) {
        return 301 https://$host$request_uri;
    }
    listen 80;
    listen [::]:80;
    server_name smu20211.sj.ifsc.edu.br;
    return 404;
}

server {
    server_name smu20211.sj.ifsc.edu.br;
    listen [::]:443 http2 ssl ipv6only=on;
    listen 443 http2 ssl;
    ssl_certificate /etc/letsencrypt/live/smu20211.sj.ifsc.edu.br/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/smu20211.sj.ifsc.edu.br/privkey.pem;
    #include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_session_timeout 1d;
    ssl_session_cache shared:MozSSL:10m;
    ssl_session_tickets off;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_prefer_server_ciphers off;
    add_header Strict-Transport-Security "max-age=63072000" always;
    ssl_stapling on;
    ssl_stapling_verify on;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;
    include /etc/nginx/conf.d/*.conf;
    location / {
        proxy_pass https://smu20211.sj.ifsc.edu.br:5349/;
    }
}
```

Além de HTTP, este servidor também suporta o protocolo STUN/TURN com a implementação `coturn` e sua respectiva configuração:

```ini
# turnserver.conf

# Rede
listening-ip=0.0.0.0
listening-ip=::
external-ip=191.36.8.50
external-ip=2804:1454:1004:101::50

# Transporte
listening-port=3478
min-port=49152
max-port=65535

# Logging
syslog
verbose

# Identificação do servidor
server-name=smu20211.sj.ifsc.edu.br
realm=smu20211.sj.ifsc.edu.br

# TLS
fingerprint
cert=/etc/letsencrypt/live/smu20211.sj.ifsc.edu.br/fullchain.pem
pkey=/etc/letsencrypt/live/smu20211.sj.ifsc.edu.br/privkey.pem
no-tlsv1
no-tlsv1_1

# Autenticação
lt-cred-mech
user=etorresini:smu20211
user=marcelo.bn:smu20211
user=gustavo.wg1985:smu20211
user=douglas.as1997:smu20211
user=adonis.m1997:smu20211
user=guilherme.ff10:smu20211
user=amanda.pm:smu20211
user=felipe.p19:smu20211
user=osvaldo.sn:smu20211
```

## Projetos das Equipes

- [farmy](https://github.com/pf-game-studio/farmy), de [pf-game-studio](https://github.com/pf-game-studio) ([projeto](https://github.com/pf-game-studio/farmy/projects/1?fullscreen=true))
- [jogo-web-smu](https://github.com/marcelo-osvaldo-smu/jogo-web-smu), de [marcelo-osvaldo-smu](https://github.com/marcelo-osvaldo-smu) ([projeto](https://github.com/marcelo-osvaldo-smu/jogo-web-smu/projects/1?fullscreen=true))
- [jogo-web-rtc](https://github.com/Douglas-and-Adonis/jogo-web-rtc), de [Douglas-and-Adonis](https://github.com/Douglas-and-Adonis) ([projeto](https://github.com/Douglas-and-Adonis/jogo-web-rtc/projects/1?fullscreen=true))
- [jogo-web](https://github.com/SMU-Amanda-Felipe/jogo-web), de [SMU-Amanda-Felipe](https://github.com/SMU-Amanda-Felipe) ([projeto](https://github.com/SMU-Amanda-Felipe/jogo-web/projects/1?fullscreen=true))
- [take-pots](https://github.com/web-game-SMU/take-pots), de [web-game-SMU](https://github.com/web-game-SMU/take-pots) ([projeto](https://github.com/web-game-SMU/take-pots/projects/1?fullscreen=true))

# Entregas

| Equipe              | Entrega 1 | Entrega 2 | Entrega 3 |
| ------------------- | --------- | --------- | --------- |
| pf-game-studio      | 10        | 10        | 10        |
| marcelo-osvaldo-smu | 10        | 10        | 10        |
| Douglas-and-Adonis  | 10        | 10        | 5         |
| SMU-Amanda-Felipe   | 10        | 10        | 5         |
| web-game-SMU        | -         | -         | -         |
