# cdn-intelexia — Documentação de Uso (Blog Post WordPress)

Objetivo: padronizar o CSS dos artigos com escopo restrito ao conteúdo do post no WordPress, permitindo troca global de cores/tema por cliente via variáveis CSS (Custom Properties).

---

## Regra 1 — Escopo obrigatório
- O CSS só se aplica ao conteúdo do post.
- Todos os seletores são escopados com `.article`.
- Tokens e temas são definidos no próprio wrapper do post para não vazar para header/footer/sidebar.

Wrapper exigido no template Single Post (Elementor):
```html
<article class="article" itemscope itemtype="https://schema.org/Article" data-theme="cdn-intelexia">
  <!-- Aqui dentro vai o widget "Post Content" -->
</article>
```

Carregamento do CSS (Elementor → Custom Code):
- Conditions: `singular/posts` APENAS.
- Insira os links de CSS no <head> conforme a ordem de import abaixo.

---

## Estrutura do CDN e Ordem de import
Arquivos hospedados no CDN (exemplo de path):
```
/css/
  /v1/
    /tokens/
      core.css
    /themes/
      cdn-intelexia.css
    /base/
      reset.css
      typography.css
      layout.css
    /components/
      article.css
      buttons.css
      table.css
      card.css
      figure.css
      boxes.css
      utilities.css
```

Ordem de import recomendada (no <head> e condicionado a `singular/posts`):
```html
<!-- Tokens base (escopados ao article) -->
<link rel="stylesheet" href="https://cdn.seu-dominio.com/css/v1/tokens/core.css">

<!-- Base -->
<link rel="stylesheet" href="https://cdn.seu-dominio.com/css/v1/base/reset.css">
<link rel="stylesheet" href="https://cdn.seu-dominio.com/css/v1/base/typography.css">
<link rel="stylesheet" href="https://cdn.seu-dominio.com/css/v1/base/layout.css">

<!-- Componentes -->
<link rel="stylesheet" href="https://cdn.seu-dominio.com/css/v1/components/article.css">
<link rel="stylesheet" href="https://cdn.seu-dominio.com/css/v1/components/buttons.css">
<link rel="stylesheet" href="https://cdn.seu-dominio.com/css/v1/components/table.css">
<link rel="stylesheet" href="https://cdn.seu-dominio.com/css/v1/components/card.css">
<link rel="stylesheet" href="https://cdn.seu-dominio.com/css/v1/components/figure.css">
<link rel="stylesheet" href="https://cdn.seu-dominio.com/css/v1/components/boxes.css">
<link rel="stylesheet" href="https://cdn.seu-dominio.com/css/v1/components/utilities.css">

<!-- Tema do cliente (override de variáveis) -->
<link rel="stylesheet" href="https://cdn.seu-dominio.com/css/v1/themes/cdn-intelexia.css">
```

---

## Tokens e Temas (cores globais por cliente)

- Tokens (base) definidos no wrapper do post:
  - Arquivo: `css/v1/tokens/core.css`
  - Seletor: `article.article { ... }`
  - Variáveis semânticas de cor, tipografia, espaçamentos, raios e sombras.

- Tema por cliente (override das variáveis semânticas):
  - Arquivo: `css/v1/themes/cdn-intelexia.css`
  - Seletor: `article.article[data-theme="cdn-intelexia"] { ... }`
  - Ativação: atributo `data-theme="cdn-intelexia"` no `<article class="article">`.

Princípios:
- Componentes não usam cores HEX diretamente; sempre `var(--color-*)`.
- Para trocar o cliente: crie `themes/cliente-x.css`, ajuste variáveis e mude `data-theme="cliente-x"` no wrapper.

---

## Tags suportadas e regras de aplicação (sempre dentro de `.article`)

- `article.article`
  - Papel: wrapper do post; define tokens/tema e largura.
  - Propriedades: `max-width: var(--measure)`, `padding-inline: var(--s4)`.
  - Atributos: `itemscope itemtype="https://schema.org/Article"`, `data-theme="cdn-intelexia"`.

- `h1`
  - Uso: título do post (único).
  - Regra: `font-size: var(--fs-800)`, `line-height: 1.2`, cor `var(--color-heading)`.
  - Responsivo (≥1024px): `h1` aumenta 10%.

- `h2`, `h3`
  - Uso: seções/subseções.
  - Regras: cor `var(--color-heading)`.
    - `h2 { margin: var(--s8) 0 var(--s3); font-size: var(--fs-700) }`
    - `h3 { margin: var(--s6) 0 var(--s2); font-size: var(--fs-600) }`

- `p`
  - Regra: `font-size: var(--fs-400)`, `line-height: 1.7`, `margin: var(--s3) 0`.

- `ul`, `ol`, `li`
  - Regra: `margin: var(--s3) 0`, `padding-inline-start: 1.2rem`.

- `a`
  - Regra: herda cor de texto; para botões, use classes `.btn`.

- `figure`, `img`, `figcaption`
  - `figure.figure`: centraliza e ajusta margens.
  - `img`: `border-radius: var(--radius-md)`, `box-shadow: var(--shadow-sm)`.
  - `figcaption`: `color: var(--color-text-muted)`, `font-size: 0.9rem`.

- `table`, `thead`, `tbody`, `tr`, `th`, `td`
  - Recomendado envolver em `<figure class="table">` para borda/scroll.
  - `thead th`: fundo `--color-table-head-bg`, texto `--color-table-head-text`, padding `0.875rem`.
  - `td`: padding `0.875rem`, borda-top 1px `--color-border`.
  - Linhas pares (tbody): fundo `--color-surface-alt`.

- `blockquote` (opcional)
  - Pode reutilizar `.highlight-box` para ênfase visual.

- `strong`, `em`, `small`, `code`, `pre`, `hr`
  - `hr` com classe `.hr`: altura `1px`, fundo `--color-border`, margem `--s8`.

---

## Classes de componentes (dentro de `.article`)

- `.kicker`: texto superior (categoria/subcategoria).
- `.meta`: linha meta (data, badges) com flex layout.
- `.badge`: chip com borda e fundo superfície.
- `.highlight-box`, `.info-box`, `.note`: caixas com borda + faixa esquerda 4px `--color-brand`, fundo `--color-surface-highlight`.
- `.resumo-executivo`: bloco de resumo com fundo `--color-surface-highlight`.
- `.cta-row`: linha de CTAs com `display: flex`, `gap` e `wrap`.
- `.btn`, `.btn--primary`, `.btn--whatsapp`: botões e variantes semânticas.
- `.table`: contêiner com borda/scroll; estilos de `thead` e `tbody`.
- `.card-grid`, `.card`: grid responsivo de cards; hover eleva 2px.
- `.figure`: estilos para imagens e legendas.
- `.sources`: bloco de fontes com fundo `--color-surface-muted` e borda tracejada.
- `.conclusao-*`: gradiente leve para seções finais.
- `.hr`: separador fino.
- `.container`: helper de largura (layout).
- `.full-bleed`: seção full width dentro do post.

Variantes/Utilitários:
- `.highlight-box--primary`, `.note--primary`: borda-esquerda com `--color-primary`.
- `.highlight-box--success`, `.note--success`: borda-esquerda com `--color-success`.
- `.u-mb-0`, `.u-mb-s2`, `.u-mb-s3`, `.u-mb-s4`, `.u-mt-s3`, `.u-p-s4`
- `.u-text-center`, `.u-text-right`, `.u-visually-hidden`

---

## Integração no Elementor (passo a passo)

1) Template Single Post:
   - Envolver o widget “Post Content” com um Container/Section:
     - Tag: `article`
     - CSS Classes: `article`
     - Atributos: `itemscope itemtype="https://schema.org/Article" data-theme="cdn-intelexia"`

2) Custom Code (Elementor → Custom Code):
   - Adicionar cada `<link rel="stylesheet" ...>` conforme ordem de import.
   - Definir Condition: `singular/posts` (apenas posts).

3) Conteúdo:
   - Usar as classes conforme documentação acima.
   - Manter hierarquia de headings (H1 único; depois H2/H3).

Exemplo simplificado dentro de `<article class="article" ...>`:
```html
<div class="kicker">Categoria • Subcategoria</div>
<h1>Título do Post</h1>
<div class="meta">
  <span class="badge">Sem comentários</span>
  <time datetime="2025-01-01">1 jan 2025</time>
</div>

<section class="highlight-box resumo-executivo">
  <strong>Ponto Central —</strong> Resumo do artigo em 2-3 frases.
</section>

<div class="cta-row">
  <a class="btn btn--whatsapp" href="#">💬 Falar no WhatsApp</a>
  <a class="btn btn--primary" href="#ancora">Chamada Principal</a>
</div>

<h2 id="secao-1">Seção</h2>
<p>Parágrafo com conteúdo.</p>

<figure class="table">
  <table>
    <thead><tr><th>Coluna 1</th><th>Coluna 2</th></tr></thead>
    <tbody>
      <tr><td>Valor 1</td><td>Valor 2</td></tr>
      <tr><td>Valor 3</td><td>Valor 4</td></tr>
    </tbody>
  </table>
</figure>

<figure class="figure">
  <img src="..." width="1200" height="628" alt="Descrição detalhada" loading="lazy" decoding="async">
  <figcaption>Legenda da imagem</figcaption>
</figure>

<aside class="info-box note">
  <strong>Observação:</strong> Nota importante contextualizada.
</aside>

<section class="sources">
  <h2>Fontes de referência</h2>
  <ul>
    <li><a href="#" rel="noopener nofollow">Fonte 1</a></li>
  </ul>
</section>
```

---

## Boas práticas, Acessibilidade e Performance
- Tipografia base mínima: `--fs-400 >= 1.0625rem`.
- Links com texto descritivo; evitar “clique aqui”.
- Imagens secundárias com `loading="lazy"`, `decoding="async"`, `width`/`height` definidos.
- Usar apenas variáveis CSS nos componentes (não usar valores HEX diretos).
- Evitar sobrescrever estilos fora do `.article`.

---

## Versionamento
- Versão atual: `/css/v1/…`
- Mudanças com quebra de compatibilidade devem ir para `/css/v2/…`.
- Manter compatibilidade retroativa sempre que possível.

---

## Criar um novo tema de cliente
1) Copie `css/v1/themes/cdn-intelexia.css` para `css/v1/themes/cliente-x.css`.
2) Ajuste variáveis necessárias (`--color-brand`, `--color-heading`, `--color-surface-highlight`, etc.).
3) No template, troque `data-theme="cdn-intelexia"` por `data-theme="cliente-x"` no `<article class="article">`.

---

## Uso com bundle (produção)
- Em produção, recomenda-se incluir apenas o bundle minificado:
```html
<link rel="stylesheet" href="https://cdn.seu-dominio.com/css/v1/bundle/cdn-intelexia.min.css">
```
- Em homologação/depuração, pode-se usar o bundle legível:
```html
<link rel="stylesheet" href="https://cdn.seu-dominio.com/css/v1/bundle/cdn-intelexia.css">
```
- Observação: o bundle já respeita a ordem correta (tokens → base → componentes → tema). Mantenha o wrapper do post com `data-theme="cdn-intelexia"`.

---

Checklist rápido de validação
- [ ] CSS carregado apenas em `singular/posts`.
- [ ] Wrapper `<article class="article" ... data-theme="...">` presente.
- [ ] H1 único, hierarquia H2/H3 correta.
- [ ] Tabela com `<thead>` obrigatório.
- [ ] Imagens com `alt`, `width`, `height`.
- [ ] Caixas de destaque com classes `.highlight-box`, `.info-box` ou `.note`.
- [ ] CTAs com `.btn`, `.btn--primary` ou `.btn--whatsapp`.
- [ ] Fontes listadas em `.sources`.
