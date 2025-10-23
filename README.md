# cdn-intelexia â€” PublicaÃ§Ã£o via GitHub + jsDelivr

Este repositÃ³rio publica `styles.min.css` para consumo via jsDelivr de forma rÃ¡pida (0 infra).

## Arquivo entregue

- `styles.min.css` (na raiz) â€” bundle minificado pronto para produÃ§Ã£o
- SRI calculado:  
  `sha384-EOyQnDZNO79921+mbo5VPaLMsdmIRqUJQyoiAy+gLMd9wHHG3povzxr6prxZrjzc`

## Como publicar (GitHub + jsDelivr)

1. Crie um repositÃ³rio pÃºblico no GitHub (ex.: `cdn-intelexia-css`).
2. FaÃ§a commit de `styles.min.css` (opcionalmente adicione tambÃ©m a pasta `css/` e `css-docs.md`).
3. Crie uma tag/release (ex.: `v1.0.0`).

### URLs jsDelivr (exemplo)
Substitua `SEU_USUARIO` e `SEU_REPO`:
- CDN: `https://cdn.jsdelivr.net/gh/SEU_USUARIO/SEU_REPO@v1.0.0/styles.min.css`

### Snippet de uso (com SRI)
```html
<link rel="preload" href="https://cdn.jsdelivr.net/gh/SEU_USUARIO/SEU_REPO@v1.0.0/styles.min.css" as="style" crossorigin="anonymous">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/SEU_USUARIO/SEU_REPO@v1.0.0/styles.min.css" integrity="sha384-EOyQnDZNO79921+mbo5VPaLMsdmIRqUJQyoiAy+gLMd9wHHG3povzxr6prxZrjzc" crossorigin="anonymous">
```

## Git (exemplo de comandos)
```sh
git init
git add styles.min.css
git commit -m "feat: publish styles.min.css (v1.0.0)"
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/SEU_REPO.git
git push -u origin main
git tag v1.0.0
git push origin v1.0.0
```

## AtualizaÃ§Ãµes futuras
- Ao alterar os CSS fonte, gere um novo `styles.min.css`, recalcule o SRI e faÃ§a:
  - `git commit` + `git push`
  - crie nova tag (ex.: `v1.0.1`)
  - atualize a versÃ£o na URL do HTML
- ObservaÃ§Ã£o: jsDelivr faz cache agressivo; ao trocar a tag (ex.: `@v1.0.1`) a CDN baixa a nova versÃ£o automaticamente.

## ObservaÃ§Ãµes tÃ©cnicas
- O CSS Ã© escopado ao conteÃºdo do post (`.article`), conforme documentaÃ§Ã£o.
- O tema `cdn-intelexia` aplica overrides de variÃ¡veis no wrapper do post (`<article class="article" data-theme="cdn-intelexia">`).
- Em produÃ§Ã£o, use apenas `styles.min.css` com `integrity` + `crossorigin="anonymous"`.
