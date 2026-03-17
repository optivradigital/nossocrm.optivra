# Troubleshooting - NossoCRM em Linux

## 1. `npm install` falha com `ENOENT package.json`

Causa provável: comando executado na pasta errada.

```bash
pwd
ls -la
```

O diretório esperado é:

```bash
~/apps/nossocrm.optivra
```

## 2. Instalador abre, mas não avança

### Sintoma no backend

Erro como:

```text
Could not find the function public.is_instance_initialized
```

### Causa

Migrations do Supabase não foram aplicadas.

### Solução

Executar no SQL Editor do Supabase:

- `supabase/migrations/20251201000000_schema_init.sql`
- `supabase/migrations/20260205000000_add_performance_indexes.sql`

## 3. Instalador abre, mas o botão continuar não faz nada

### Sintoma no navegador

Erro no console:

```text
Unhandled Promise Rejection: TypeError: undefined is not an object (evaluating 'crypto.subtle.digest')
```

### Causa

Aplicação sendo acessada por HTTP/IP e não por HTTPS.

### Solução

Publicar com domínio + Nginx + SSL.

## 4. `date-fns` ou outra dependência ausente

### Sintoma

```text
Module not found: Can't resolve 'date-fns'
```

### Solução

Corrigir o repositório e rodar:

```bash
npm install
npm run build
```

## 5. PM2 online mas aplicação não responde

Validar:

```bash
pm2 status
pm2 logs nossocrm --lines 100
ss -tulpn | grep 3001
```

## 6. Banco Supabase configurado, mas app não conecta

Validar `.env.local`:

- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY`
- `SUPABASE_SECRET_KEY`

Depois reiniciar:

```bash
pm2 restart nossocrm --update-env
```
