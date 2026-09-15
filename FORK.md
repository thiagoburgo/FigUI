# Fork FigUI — thiagoburgo/FigUI

Este repositório é um [fork](https://github.com/thiagoburgo/FigUI) de [figamore/FigUI](https://github.com/figamore/FigUI), a interface web moderna para [FluidNC](https://github.com/bdring/FluidNC).

O upstream oficial continua sendo a fonte de referência. Este fork existe para **desenvolver, testar e distribuir** melhorias antes (ou independentemente) da integração no projeto original.

---

## O que este fork contribui

As contribuições abaixo estão sendo enviadas ao upstream em PRs separadas, seguindo a estratégia de revisão incremental:

| PR | Branch | Descrição |
|----|--------|-----------|
| 1 | `pr/color-scheme` | `color-scheme` nos temas — controles nativos do browser respeitam light/dark |
| 2 | `pr/compact-landscape-tablet` | Layout compact landscape para tablets baixos (<640px de altura visível) |
| 3 | `pr/tablet-height-hooks` | Hooks de altura dinâmica + fix Vite `cssTarget: chrome61` para WebView de tablet |
| 4 | `pr/compact-landscape-polish` | Refinamentos de DRO e dimensionamento do JogPad |

### Layout compact landscape (feature principal)

Em tablets landscape com pouca altura (7–8", barra do browser, split-screen), a UI padrão comprime demais o jog e o DRO. Este fork adiciona:

- Detecção de viewport via `visualViewport` (`src/lib/viewport.tsx`)
- Layout side-by-side POSITION + JOG com tab strip para Viewer/Files/Macros
- Scroll de página para manter alvos de toque utilizáveis
- Componentes dedicados: `TabletMainShell`, `TabletCompactLandscapeLayout`, `TabletTabbedPanel`

Documentação de comportamento já alinhada ao [README](README.md) (secção Responsive Layouts).

---

## Diferenças em relação ao upstream

| Aspecto | figamore/FigUI (upstream) | thiagoburgo/FigUI (este fork) |
|---------|---------------------------|-------------------------------|
| **Código de features** | Baseline oficial | Inclui branches de contribuição acima |
| **Versão** | Ex.: `1.3.2` | Sufixo fork, ex.: `1.3.3-fork.1` |
| **Releases / OTA** | [figamore.github.io/FigUI](https://figamore.github.io/FigUI/) | [thiagoburgo.github.io/FigUI](https://thiagoburgo.github.io/FigUI/) |
| **GitHub repo (update check)** | `figamore/FigUI` | `thiagoburgo/FigUI` |
| **Este arquivo** | Não existe | `FORK.md` — documentação do fork |

As alterações de OTA e versão existem **apenas neste fork** e não são enviadas nos PRs para o upstream.

---

## Como usar este fork

### Demo no browser

Após publicar GitHub Pages (Settings → Pages → GitHub Actions), acesse:

**https://thiagoburgo.github.io/FigUI/**

### Build e upload manual no ESP32

```bash
npm install
npm run build:esp32
```

Faça upload de `dist/index.html.gz` para o filesystem local do ESP32 via File Manager do FigUI.

### OTA integrado (About → Update)

1. Habilite **GitHub Pages** no fork (fonte: GitHub Actions).
2. Execute o workflow **Release** em Actions (informe versão, ex. `1.3.3-fork.1`).
3. O workflow gera release + `firmware/index.html.gz` no Pages.
4. No ESP32 com este build instalado, use **About → Check for updates**.

---

## Sincronizar com o upstream

```bash
git fetch upstream
git checkout main
git merge upstream/main
# Reaplicar o commit fork-only (OTA/versão) se necessário
git push origin main
```

---

## Enviar contribuições ao upstream

PRs devem partir das branches `pr/*` deste fork para `figamore/FigUI:main`:

```bash
gh pr create --repo figamore/FigUI --base main --head thiagoburgo:pr/color-scheme
```

Não incluir em PRs upstream: `FORK.md`, alterações de `GITHUB_REPO`/`FIRMWARE_URL`, `.env`, ou mudanças locais em `package-lock.json`.

---

## Licença

Mesma licença do upstream: **GPLv3**. Ver [LICENSE](LICENSE).
