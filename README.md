# cdn-intelexia — Publicação via GitHub + jsDelivr

Este repositório publica `styles.min.css` para consumo via jsDelivr de forma rápida (0 infra).

## Arquivo entregue

- `styles.min.css` (na raiz) — bundle minificado pronto para produção
- SRI calculado:  
  `sha384-V38exks0JiM91ckUqa4WH88wyMAQ2OMt/vTZbZExF4rlK3W1DlkIVKrrbPWQuKgd`

## Como publicar (GitHub + jsDelivr)

1. Crie um repositório público no GitHub (ex.: `cdn-intelexia-css`).
2. Faça commit de `styles.min.css` (opcionalmente adicione também a pasta `css/` e `css-docs.md`).
3. Crie uma tag/release (ex.: `v1.0.0`).

### URLs jsDelivr (exemplo)
Substitua `SEU_USUARIO` e `SEU_REPO`:
- CDN: `https://cdn.jsdelivr.net/gh/SEU_USUARIO/SEU_REPO@v1.0.0/styles.min.css`

### Snippet de uso (com SRI)
```html
<link rel="preload" href="https://cdn.jsdelivr.net/gh/SEU_USUARIO/SEU_REPO@v1.0.0/styles.min.css" as="style" crossorigin="anonymous">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/SEU_USUARIO/SEU_REPO@v1.0.0/styles.min.css" integrity="sha384-V38exks0JiM91ckUqa4WH88wyMAQ2OMt/vTZbZExF4rlK3W1DlkIVKrrbPWQuKgd" crossorigin="anonymous">
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

## Atualizações futuras
- Ao alterar os CSS fonte, gere um novo `styles.min.css`, recalcule o SRI e faça:
  - `git commit` + `git push`
  - crie nova tag (ex.: `v1.0.1`)
  - atualize a versão na URL do HTML
- Observação: jsDelivr faz cache agressivo; ao trocar a tag (ex.: `@v1.0.1`) a CDN baixa a nova versão automaticamente.

## Observações técnicas
- O CSS é escopado ao conteúdo do post (`.article`), conforme documentação.
- O tema `cdn-intelexia` aplica overrides de variáveis no wrapper do post (`<article class="article" data-theme="cdn-intelexia">`).
- Em produção, use apenas `styles.min.css` com `integrity` + `crossorigin="anonymous"`.
