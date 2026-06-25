---
name: sync-publications
description: Sincronizar e verificar a página de publicações (content/publications/_index.md) do site leofn.com contra o Google Scholar e validar DOIs via Crossref. Use ao adicionar publicações, conferir se o site está atualizado com o Scholar, ou corrigir links de DOI quebrados/errados.
---

# Sincronizar publicações com Google Scholar + verificar DOIs

Mantém `content/publications/_index.md` em dia com o perfil do Scholar e garante que todo DOI aponta para o artigo certo. Identificadores do autor:

- **Google Scholar:** `essj6yQAAAAJ` → `https://scholar.google.com/citations?user=essj6yQAAAAJ`
- **ORCID:** `0000-0003-2907-8338`

## 1. Puxar a lista completa do Scholar

Use WebFetch nesta URL (força lista completa, ordenada por data):

```
https://scholar.google.com/citations?user=essj6yQAAAAJ&hl=en&cstart=0&pagesize=100&view_op=list_works&sortby=pubdate
```

Peça no prompt a **enumeração de TODAS as linhas** (título, coautores, venue, ano) — sem filtro de "selected", senão o modelo resumidor corta a lista. Anote também h-index, i10-index e citações totais (para o CV).

## 2. Comparar com o site

Mapeie cada item do Scholar contra as seções de `content/publications/_index.md`:
`### Books`, `### Peer-Reviewed Articles`, `### Book Chapters`, `### Technical Reports & Conference Papers`, `### Preprints`, `### Essays & Public Writing`, `### Theses & Dissertations`.

O Scholar costuma ter **mais** itens (preprints, duplicatas published/preprint). O objetivo é achar o que está **no Scholar mas falta no site**. Classifique cada novo item na seção correta (não jogue tudo em Peer-Reviewed).

## 3. Verificar DOIs via Crossref (autoritativo)

**Nunca confie no DOI sem resolver.** Para cada DOI, confira via API do Crossref que título/autores batem com a entrada:

```bash
curl -s "https://api.crossref.org/works/<DOI>" | python3 -c "import sys,json; d=json.load(sys.stdin)['message']; print('Title :', d.get('title',['?'])[0]); print('Authors:', ', '.join(a.get('family','?') for a in d.get('author',[]))); print('Journal:', (d.get('container-title') or ['?'])[0]); print('Year  :', d.get('issued',{}).get('date-parts',[['?']])[0][0])"
```

Para **achar** o DOI correto de um artigo (quando o atual está errado):

```bash
curl -s "https://api.crossref.org/works?query.bibliographic=<termos+do+titulo+e+autor>&rows=5" | python3 -c "import sys,json; [print(d.get('DOI'),'|',d.get('title',['?'])[0]) for d in json.load(sys.stdin)['message']['items']]"
```

Erros típicos já vistos: DOI que dá 404, ou que resolve para **outro artigo** (mesmo periódico/volume, paper diferente). Sempre cruzar título E autores.

## 4. Formato das entradas

Estilo APA-ish, periódico em itálico, link ao final. Exemplos:

```markdown
- Sobrenome, A. B., & Nascimento, L. F. (2024). Título do artigo. *Periódico em Itálico*, 31(4), 530–554. [DOI](https://doi.org/10.xxxx/yyyy)
- Nascimento, L. F., ... (2026). Título. *Proceedings ...*. Association for Computational Linguistics. [PDF](https://aclanthology.org/...)
```

- Ordem **reverso-cronológica** dentro de cada seção.
- Sufixos `a`/`b` no ano só quando há 2+ obras do mesmo autor no mesmo ano; reavalie ao mudar anos.
- Preprints (OSF etc.) vão em `### Preprints`, com `[DOI](https://doi.org/10.31235/osf.io/...)`.

## 5. Atualizar métricas no CV

Se as métricas do Scholar mudaram, atualize o bloco `## Impact Metrics` em `content/cv/_index.md` (h-index, i10-index, Citations).

## 6. Fechar

Build (`hugo`) e commit em inglês: `feat(publications): ...` ou `fix(publications): ...`. Push para `main` publica (ver skill **edit-site**).
