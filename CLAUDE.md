# CLAUDE.md — leofn.github.io

Instruções de projeto para o Claude Code. Leia antes de qualquer modificação.

## Skills do projeto

Há skills versionadas em `.claude/skills/` que detalham os fluxos de trabalho — prefira-as:

- **`edit-site`** — fluxo geral de edição (onde editar o quê, regras, build, commit, deploy).
- **`sync-publications`** — sincronizar `content/publications/_index.md` com o Google Scholar e validar DOIs via Crossref.

## Stack

| Camada | Tecnologia |
|--------|-----------|
| SSG | Hugo v0.160.1 extended (Homebrew) |
| Hospedagem | GitHub Pages (branch `main`) |
| CI/CD | `.github/workflows/render.yml` (usa Hugo v0.124.1 extended) |
| Domínio | `leofn.com` (CNAME em `static/CNAME`) |
| Formulário | Formspree (endpoint configurado em `content/contact/_index.md`) |
| Tema | `hello-friend-ng` (submódulo git em `themes/hello-friend-ng`) |

## Comandos

```bash
hugo server -D          # dev local com drafts
hugo                    # build para /public
git submodule update --init --recursive  # inicializar tema após clone
```

## Estrutura de arquivos críticos

```
assets/css/custom.css       # FONTE ÚNICA de estilos customizados (via Hugo Pipes)
layouts/_default/list.html  # override do template padrão — aplica layout flat a todas as páginas internas
layouts/partials/extra-head.html  # injeta custom.css com fingerprint (cache busting)
layouts/partials/javascript.html  # injeta back-to-top button + script
hugo.toml                   # config principal: menus, social links, parâmetros do tema
content/_index.md           # homepage
content/cv/_index.md        # página de CV com link para PDF
content/talks/_index.md     # apresentações de trabalho (em inglês, por ano)
content/press/_index.md     # cobertura de imprensa via Knight Lab Timeline (iframe)
content/teaching/_index.md  # histórico de disciplinas por semestre (tabelas)
static/cv/nascimento-cv.pdf # PDF do CV
static/img/profile.webp     # foto de perfil
```

## Padrões de CSS

O CSS usa **custom properties** (variáveis CSS) para suportar o theme toggle (claro/escuro) do tema.
- Tokens de cor ficam em `:root, html[data-theme="light"]` e `html[data-theme="dark"]`
- Acento principal: `--accent` (azul `#2563eb` no light, `#60a5fa` no dark)
- Nunca usar cores hardcoded fora dos blocos de tokens
- Seletor de páginas internas: `.page-content` (via `layouts/_default/list.html`)
- Seletor da homepage: `.content-center`

## Taxonomias

Tags foram **removidas** intencionalmente. A seção `[taxonomies]` foi **removida por completo** do `hugo.toml` — deixá-la vazia quebra a homepage no tema `hello-friend-ng`. Não reintroduzir.

## Tema — submódulo git

O tema está em `themes/hello-friend-ng` como submódulo git. Em um clone novo, a pasta fica vazia (homepage renderiza vazia). Sempre rodar:

```bash
git submodule update --init --recursive
```

## Imagens / Favicon

- Favicon gerado pelo tema a partir de `[params.favicon.color]` no `hugo.toml`
- Foto de perfil: `static/img/profile.webp` — referenciada via `[params.portrait]`

## Deploy

Push para `main` dispara o workflow automaticamente. Não há branch separada para deploy.

## Idioma do conteúdo

Todo o conteúdo das páginas deve estar em **inglês**, incluindo títulos de disciplinas e apresentações. Exceção: títulos de publicações mantêm o idioma original da obra.

## Links de contato e e-mail

- Links externos (CV, contato) abrem em nova aba: `target="_blank" rel="noopener"`.
- E-mail sempre **ofuscado** contra spam harvesting: `leofn3[at]gmail.com` em texto puro. Nunca usar `mailto:` nem `@` literal.

## Publicações e DOIs

- `content/publications/_index.md` é mantido em sincronia com o Google Scholar (`essj6yQAAAAJ`).
- **Todo DOI deve ser verificado via Crossref antes de publicar** — já houve DOIs que davam 404 ou resolviam para outro artigo. Ver skill `sync-publications`.
