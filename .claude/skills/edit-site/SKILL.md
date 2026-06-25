---
name: edit-site
description: Editar o site pessoal leofn.com (Hugo + hello-friend-ng). Use ao alterar qualquer conteúdo (content/), estilo (assets/css/custom.css), layout, menu ou configuração, e ao buildar/commitar/publicar. Cobre as regras do projeto e o fluxo de deploy.
---

# Editar o site leofn.com

Site pessoal acadêmico de Leonardo F. Nascimento. **Hugo extended + tema `hello-friend-ng` (submódulo git) + GitHub Pages.** Domínio `leofn.com`. Leia `CLAUDE.md` na raiz antes de qualquer mudança.

## Setup (clone novo)

```bash
git submodule update --init --recursive   # tema fica vazio sem isto → homepage em branco
```

## Onde editar o quê

| Quero mudar… | Arquivo |
|---|---|
| Conteúdo de uma página | `content/<seção>/_index.md` |
| Estilo / cores / layout visual | `assets/css/custom.css` (FONTE ÚNICA — nunca `static/css/`) |
| Layout de páginas internas | `layouts/_default/list.html` |
| `<head>` / injeção de CSS | `layouts/partials/extra-head.html` |
| Menu, social links, parâmetros | `hugo.toml` |
| Foto de perfil | `static/img/profile.webp` |

## Regras invioláveis

1. **Conteúdo das páginas em inglês** — títulos de disciplinas, talks, descrições. (Títulos de publicações ficam no idioma original da obra.)
2. **Nunca editar arquivos em `themes/`** — é submódulo; será sobrescrito. Customize via `layouts/`, `assets/`, `static/`.
3. **CSS só em `assets/css/custom.css`** (Hugo Pipes + fingerprint). Use as custom properties existentes (`--accent` etc.); nunca hardcode cores fora dos blocos de token claro/escuro.
4. **Não reintroduzir `[taxonomies]`** no `hugo.toml` — seção vazia quebra a homepage no tema. Tags foram removidas de propósito.
5. **Links de contato/externos**: abrir em nova aba (`target="_blank" rel="noopener"`); e-mail sempre ofuscado (`leofn3[at]gmail.com`, texto puro — nunca `mailto:` nem `@` literal).

## Build e validação

```bash
hugo                 # build para /public — confira "ERROR" na saída
hugo server -D       # preview local com drafts
```

Um `WARN deprecated: css.Sass libsass` é esperado e inofensivo.

## Commit e deploy

- Mensagens de commit **em inglês**, conventional commits: `tipo(escopo): descrição` (ex.: `fix(cv): ...`, `feat(publications): ...`).
- **Push para `main` dispara o deploy** (workflow `.github/workflows/render.yml`). Não há branch de deploy separada — o histórico commita direto na `main`.
- Antes do push, faça `git fetch` + rebase se a remota divergiu (outros pushes acontecem direto na `main`):
  ```bash
  git fetch origin && git rebase origin/main && git push origin main
  ```
- Não versionar `public/`, `.DS_Store`, nem arquivos avulsos não relacionados ao site. Stage seletivo.

## Páginas existentes

`/` (home), `/cv/`, `/publications/`, `/projects/`, `/talks/`, `/teaching/`, `/press/`, `/contact/`, `/slides/`.

Para sincronizar publicações com o Google Scholar ou verificar DOIs, use a skill **sync-publications**.
