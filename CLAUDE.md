# CLAUDE.md, G2Martins (perfil do GitHub)

> **Spec viva.** Porta de entrada lida pelo agente toda sessão. Atualize quando uma regra, asset ou armadilha mudar.
>
> **Última revisão:** 2026-11-10
> **Fonte dos fatos:** `G2Portfolio/src/app/data/content.ts` e `projects.ts` (repo [G2Portfolio](https://github.com/G2Martins/G2Portfolio))

---

## 1. O que é

Repo especial `G2Martins/G2Martins`: o `README.md` aparece em <https://github.com/G2Martins>. Cartão de visita para recrutador, legível em 20 segundos, na linguagem visual do portfólio (<https://g2portfolio.grovicdata.com>): papel quente `#FAF9F6` / escuro `#171614`, acento `#003ADD`, gradiente `#001C80 → #003ADD → #668FFF`, Geist.

## 2. Mapa

| Caminho | O quê |
| --- | --- |
| `README.md` | Banner, links rápidos, pitch, Agora, projetos (grade 3x2), stack, GitHub, formação, rodapé |
| `assets/header-light.svg`, `header-dark.svg` | Banner com Geist + Geist Mono embutidas (base64, latin). Mesmo layout, só as cores mudam |
| `assets/g2-mark.svg` | Marca G2 (cópia de `G2Portfolio/public/favicon.svg`) |
| `assets/projects/*.webp` | Miniaturas 640px (cópia de `G2Portfolio/public/img/projects/<slug>-640.webp`) |
| `.github/workflows/snake.yml` | Gera a cobrinha (claro/escuro) diária e publica no branch `output` |

## 3. Editar e pré-visualizar

- **Texto do banner:** editar os `<text>` nos DOIS SVGs igualmente (cada grupo está numa linha própria). Fonte embutida cobre todo o Latin, então qualquer texto PT-BR renderiza.
- **Fato novo** (cargo, projeto, número): mudar primeiro no `content.ts`/`projects.ts` do portfólio, depois aqui.
- **Preview:** `gh api markdown -f mode=gfm -f context=G2Martins/G2Martins -F text=@README.md > .shots/readme.html` e abrir com o CSS `github-markdown-css` (claro e escuro). Prints em `.shots/` (gitignored).

## 4. Regras SEMPRE-ATIVAS

- **Só fatos do portfólio.** Nada inventado. Primeira pessoa ("Sou Gustavo..."), PT-BR, uma linha em EN no topo.
- **Sem travessão (U+2014)** em lugar nenhum (README, alt, SVG). Usar ":", ",", "." ou "·".
- **Grovic Data:** produtos (Valerium, ProntuSMART) linkam **só o site**, nunca repo da Grovic. Exceções públicas: ProntuSMART e Routify.
- **Toda imagem com `alt`; toda URL absoluta.** Assets do repo via `https://raw.githubusercontent.com/G2Martins/G2Martins/main/...`.
- **Claro/escuro via `<picture>`** + `prefers-color-scheme`, com as cores do portfólio.
- **Animação no SVG só `transform`/`opacity`**, desligada em `prefers-reduced-motion`.
- **Workflow:** só o `GITHUB_TOKEN` automático, actions fixadas por SHA, `permissions` mínimas.
- **Enxuto:** README abaixo de ~150 linhas.

## 5. Common Hurdles (armadilhas conhecidas)

- **`srcset` quebra em vírgula:** URL do skillicons dentro de `<source srcset>` precisa de `%2C` no lugar de `,` (senão só o 1º ícone aparece no tema escuro).
- **Caminho relativo em `srcset` não é reescrito** pelo GitHub e quebra na página do perfil. Usar URL absoluta do raw.
- **Imagens 404 até o push** (raw `main`) e a cobrinha até o 1º run do workflow (Actions > snake > Run workflow).
- **github-readme-stats (503) e activity-graph (402)** públicos estão fora do ar (limite da Vercel, nov/2026). `streak-stats.demolab.com` funciona.
- **simple-icons tirou LinkedIn, Power BI e Azure:** os badges do shields usam ícone em data URI (base64 com `+` e `=` codificados como `%2B` e `%3D`).
- **Print headless:** SVG fora da viewport não anima (card de streak sai vazio). Ajustar a viewport para a altura total da página antes do print.
- **`→` não existe na Geist latin:** o navegador usa a fonte do sistema para a seta. Normal.
