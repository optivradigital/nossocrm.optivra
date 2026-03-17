# Checklist Pós-Instalação - NossoCRM Linux

## Aplicação

- [ ] `npm install` executado com sucesso
- [ ] `npm run build` executado com sucesso
- [ ] PM2 com processo `nossocrm` online
- [ ] Aplicação responde na porta 3001

## Supabase

- [ ] `.env.local` preenchido com URL e chaves corretas
- [ ] migration `20251201000000_schema_init.sql` aplicada
- [ ] migration `20260205000000_add_performance_indexes.sql` aplicada
- [ ] instalador abre em `/install/start`

## HTTPS

- [ ] domínio apontando para o IP do servidor
- [ ] Nginx configurado
- [ ] Certbot executado com sucesso
- [ ] instalador acessível por HTTPS

## Operação

- [ ] `pm2 save` executado
- [ ] script de update disponível
- [ ] documentação operacional revisada
