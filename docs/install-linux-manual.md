# NossoCRM - Instalação Manual em Servidor Linux

Este guia descreve como instalar o NossoCRM em um servidor Linux (Ubuntu) sem usar Vercel.

## Arquitetura recomendada

- Aplicação: Next.js
- Processo: PM2
- Banco/Auth: Supabase
- Proxy reverso: Nginx
- SSL: Let's Encrypt / Certbot

## Pré-requisitos

- Ubuntu com acesso SSH
- Node.js 20+
- npm
- PM2
- Git
- Nginx
- domínio ou subdomínio apontando para o IP do servidor
- projeto criado no Supabase

## 1. Clonar o repositório

```bash
cd ~/apps
git clone git@github.com:optivradigital/nossocrm.optivra.git
cd nossocrm.optivra
```

## 2. Instalar dependências

```bash
npm install
```

## 3. Criar `.env.local`

```bash
cp .env.example .env.local
nano .env.local
```

Preencher no mínimo:

```env
NEXT_PUBLIC_SUPABASE_URL=https://SEU-PROJETO.supabase.co
NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY=sb_publishable_...
SUPABASE_SECRET_KEY=sb_secret_...
ALLOW_AI_TEST_ROUTE=false
ALLOW_UI_MOCKS_ROUTE=false
INSTALLER_ENABLED=true
INSTALLER_TOKEN=
```

## 4. Aplicar migrations no Supabase

No SQL Editor do Supabase, executar nesta ordem:

1. `supabase/migrations/20251201000000_schema_init.sql`
2. `supabase/migrations/20260205000000_add_performance_indexes.sql`

## 5. Gerar build

```bash
npm run build
```

## 6. Subir com PM2

```bash
PORT=3001 pm2 start npm --name nossocrm -- start
pm2 save
```

## 7. Validar aplicação

```text
http://IP_DO_SERVIDOR:3001
```

## 8. Configurar Nginx

Exemplo para `nossocrm.aet.com` em `infra/nginx/nossocrm.aet.com.conf`.

## 9. Configurar SSL

```bash
sudo certbot --nginx -d nossocrm.aet.com
```

## 10. Concluir instalação

Com HTTPS ativo:

```text
https://nossocrm.aet.com/install/start
```

## Observações importantes

- O instalador web depende de HTTPS por causa do uso de `crypto.subtle` no navegador.
- Não subir `.env.local` para o Git.
- Sem Vercel, a aplicação do schema do Supabase é manual.
