# NossoCRM - Instalação Semi-Automática em Servidor Linux

Este guia usa os scripts em `scripts/` para preparar o servidor e subir a aplicação.

## Pré-requisitos

- servidor Ubuntu com Node.js 20+, npm, Git e PM2 já instalados
- projeto Supabase já criado
- domínio opcional na fase inicial

## 1. Executar bootstrap do servidor

```bash
bash scripts/bootstrap-server.sh
```

## 2. Executar instalação da aplicação

```bash
bash scripts/install-nossocrm.sh
```

Na primeira execução, o script:
- clona o repositório
- instala dependências
- cria `.env.local` se não existir
- interrompe para edição do arquivo

## 3. Editar `.env.local`

```bash
nano ~/apps/nossocrm.optivra/.env.local
```

## 4. Aplicar migrations no Supabase

Executar manualmente no SQL Editor do Supabase:

- `supabase/migrations/20251201000000_schema_init.sql`
- `supabase/migrations/20260205000000_add_performance_indexes.sql`

## 5. Rodar novamente o script de instalação

```bash
bash scripts/install-nossocrm.sh
```

## 6. Validar

```bash
pm2 status
pm2 logs nossocrm --lines 100
```

Abrir:

```text
http://IP_DO_SERVIDOR:3001
```

## 7. Publicar com domínio e SSL

- configurar Nginx
- configurar Certbot
- acessar via HTTPS
