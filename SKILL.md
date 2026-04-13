# SKILL.md — Padrões e técnicas do projeto

Registro das técnicas e decisões de implementação adotadas neste site.

## Hugo Pipes — CSS com fingerprint

`assets/css/custom.css` é processado via Hugo Pipes (minify + fingerprint) para cache busting automático:

```html
{{- with resources.Get "css/custom.css" | minify | fingerprint }}
  <link rel="stylesheet" href="{{ .RelPermalink }}" integrity="{{ .Data.Integrity }}" crossorigin="anonymous">
{{- end }}
```

Arquivo deve ficar em `assets/css/`, **não** em `static/css/`. O arquivo em `static/css/custom.css` é um resquício — não é usado.

## Layout override para páginas internas

O tema `hello-friend-ng` renderiza páginas de lista com card/shadow por padrão. Para obter layout flat igual à homepage, criamos `layouts/_default/list.html`:

```html
{{ define "main" }}
  <div class="content">
    <main class="posts">
      <h1 class="page-title">{{ .Title }}</h1>
      {{ if .Content }}
        <div class="page-content">{{ .Content }}</div>
      {{ end }}
    </main>
  </div>
{{ end }}
```

Isso remove o card/box-shadow das páginas de conteúdo (CV, Publications, Teaching, etc.) e aplica o seletor `.page-content` para os estilos custom.

## Design system — custom properties

Toda a paleta usa CSS custom properties para compatibilidade com o theme toggle do tema:

- Tokens definidos em `:root` (light) e `html[data-theme="dark"]`
- O tema alterna o atributo `data-theme` no elemento `html` via JS
- Usar sempre `var(--token)` nos seletores; nunca hardcodar cor fora dos blocos de token

## Back-to-top button

Injetado via `layouts/partials/javascript.html` com JS inline mínimo:
- Aparece após scroll > 300px
- Animação com `transform + opacity` (respeitando `prefers-reduced-motion`)
- Botão circular com `var(--accent)` como background

## Formspree — formulário de contato

- HTML raw no markdown: habilitado via `markup.goldmark.renderer.unsafe = true` no `hugo.toml`
- Honeypot field (`name="_gotcha"`) para anti-spam básico
- Endpoint Formspree configurado diretamente no HTML do `content/contact/_index.md`

## Remoção de taxonomias

Tags foram removidas em três etapas:
1. Seção `[taxonomies]` **removida por completo** do `hugo.toml` (deixá-la vazia quebra a homepage)
2. `tags:` removido dos front matters de todos os arquivos de conteúdo
3. Override do `layouts/_default/list.html` eliminou o bloco de tags do layout

## Knight Lab Timeline — embed via iframe

A página Press embeds uma timeline do Knight Lab Timeline JS diretamente no markdown via iframe (funciona pois `markup.goldmark.renderer.unsafe = true`):

```html
<div style="width:100%;overflow:hidden;border-radius:8px;margin-top:1rem;">
  <iframe
    src="https://cdn.knightlab.com/libs/timeline3/latest/embed/index.html?source=SHEET_ID&font=Lustria-Lato&lang=en&initial_zoom=2&height=650"
    width="100%"
    height="650"
    frameborder="0"
    allowfullscreen>
  </iframe>
</div>
```

O `source` é o ID de uma Google Sheet pública com os dados da timeline.

## Conteúdo acadêmico — estrutura de páginas

- **Talks** (`content/talks/_index.md`): apresentações organizadas por ano (mais recente primeiro), em inglês, formato lista com bullets. Tipo de apresentação após o travessão.
- **Press** (`content/press/_index.md`): cobertura de imprensa via iframe Knight Lab Timeline.
- **Teaching** (`content/teaching/_index.md`): histórico de disciplinas por semestre em tabelas (`| Course | Hours | Level |`), sem cabeçalhos extras, mais recente primeiro.

## Inicialização do tema (submódulo git)

O tema `hello-friend-ng` está como submódulo. Em clone novo a pasta `themes/` fica vazia — o build gera `index.html` vazio. Solução:

```bash
git submodule update --init --recursive
```
