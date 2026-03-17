# NossoCRM - Linux Self-Hosted Pack

Este pacote adiciona uma opção oficial de instalação do NossoCRM em servidor Linux sem Vercel.

## Conteúdo

- `docs/` documentação manual, automática e troubleshooting
- `scripts/` bootstrap, instalação e update
- `infra/nginx/` exemplos de virtual host
- `infra/ssl/` notas para Certbot
- `.env.linux.example` exemplo de variáveis de ambiente

## Fluxo resumido

1. preparar servidor Linux
2. criar projeto Supabase
3. preencher `.env.local`
4. aplicar migrations do Supabase
5. subir app com PM2
6. configurar Nginx e SSL
7. finalizar instalador em HTTPS
