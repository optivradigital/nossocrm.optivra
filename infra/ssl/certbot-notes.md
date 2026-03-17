# SSL com Certbot

## Pré-requisitos

- domínio apontando para o IP do servidor
- Nginx ativo
- portas 80 e 443 liberadas

## Comandos

### Lavvy

```bash
sudo certbot --nginx -d lavvy.co -d www.lavvy.co
```

### NossoCRM

```bash
sudo certbot --nginx -d nossocrm.aet.com
```

## Teste de renovação

```bash
sudo certbot renew --dry-run
```
