# Odds Arena — Futebol Brasileiro Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Reformular o jogo "Odds Arena" de NBA para futebol brasileiro (MG/SP/RJ) com redesign visual clean/light e identidade profissional para portfolio.

**Architecture:** Arquivo HTML único (`Odds Arena.html`) com todas as mudanças feitas inline — sem build step, deploy direto na Vercel. As mudanças são: design tokens CSS, fonte Syne adicionada, SVG do fundo substituído, constantes JS de dados trocadas, strings de texto atualizadas, lógica de clock adaptada para minutos de futebol.

**Tech Stack:** HTML5, CSS3 (custom properties), JavaScript vanilla, Google Fonts (Syne + Inter + JetBrains Mono), Web Audio API, Canvas API.

---

## Mapa de Arquivos

| Arquivo | Ação | Responsabilidade |
|---|---|---|
| `Odds Arena.html` | Modificar | Tudo — único arquivo da aplicação |

Seções do arquivo a tocar (por linha aproximada):
- `L2`: `lang="en"` → `lang="pt-BR"`
- `L6`: `<title>` → "Odds Arena · Futebol Brasileiro"
- `L9`: Google Fonts — adicionar Syne
- `L14–58`: Design tokens CSS — trocar accent, adicionar `--font-display`, vars de times BR
- `L77–119`: `.court-bg` SVG — substituir linhas de basquete por campo de futebol
- `L1060–1082`: HTML do court-bg — atualizar SVG inline
- `L1124–1143`: Landing HTML — atualizar textos
- `L1146–1170`: Lobby HTML — atualizar textos
- `L1173–1207`: Draft HTML — atualizar labels
- `L1210–1262`: Live screen HTML — atualizar matchup hardcoded, labels Q1-Q4
- `L1267–1276`: Resolution HTML — atualizar textos
- `L1285–1335`: `NBA_TEAMS`, `LIVE_GAMES`, `PLAYERS`, `MARKETS` — substituir completamente
- `L1340–1356`: `state` inicial — atualizar `gameScore`, `clockSec`, `quarter`
- `L1682–1830`: `startLiveGame()` — adaptar lógica de quarters para minutos
- `L1835–1880`: `showResolution()` — atualizar game story
- `L1869–1880`: Game story text hardcoded — atualizar para futebol
- `L1886–1940`: `startConfetti()` — atualizar cores das equipes BR
- `L1996–2057`: Script Perplexity inline edit — **remover completamente**

---

## Task 1: Head, fonts e meta

**Arquivos:**
- Modify: `Odds Arena.html:2,6,9`

- [ ] **Step 1: Atualizar lang e title**

Substituir:
```html
<html lang="en">
```
Por:
```html
<html lang="pt-BR">
```

Substituir:
```html
<title>Odds Arena</title>
```
Por:
```html
<title>Odds Arena · Futebol Brasileiro</title>
```

- [ ] **Step 2: Adicionar Syne ao Google Fonts**

Substituir:
```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500;600;700;800&display=swap" rel="stylesheet">
```
Por:
```html
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@700;800&family=Inter:wght@400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500;600;700;800&display=swap" rel="stylesheet">
```

- [ ] **Step 3: Verificar no browser**

Abrir `Odds Arena.html` no browser. O title na aba deve mostrar "Odds Arena · Futebol Brasileiro". Inspecionar elemento `<html>` e confirmar `lang="pt-BR"`.

---

## Task 2: Design tokens CSS — paleta e tipografia

**Arquivos:**
- Modify: `Odds Arena.html:14–58`

- [ ] **Step 1: Atualizar tokens raiz**

Substituir o bloco completo `:root { --bg: ... }` (linhas 14–37) por:

```css
:root {
  --bg: #F8F8F6;
  --bg-warm: #F2F2EF;
  --surface: #FFFFFF;
  --surface-alt: #F5F5F2;
  --border: #E8E8E4;
  --border-strong: #D0CFC9;
  --text: #111110;
  --text-muted: #6B6B63;
  --text-faint: #A8A8A0;
  --accent: #1A6B3C;
  --accent-hover: #155730;
  --accent-light: rgba(26, 107, 60, 0.08);
  --red: #DC2626;
  --green: #16A34A;
  --blue: #1A6B3C;
  --ticker-bg: #111111;
  --ticker-text: #E8E6E0;
  --font-sans: 'Inter', system-ui, -apple-system, sans-serif;
  --font-display: 'Syne', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', 'Courier New', monospace;
  --ease-out: cubic-bezier(0.16, 1, 0.3, 1);
  --ease-in: cubic-bezier(0.4, 0, 1, 1);
  --ease-in-out: cubic-bezier(0.4, 0, 0.2, 1);
  --transition-interactive: 180ms cubic-bezier(0.16, 1, 0.3, 1);
}
```

- [ ] **Step 2: Substituir cores de times NBA por times brasileiros**

Substituir o bloco `/* NBA team colors */` (linhas 40–58) por:

```css
/* Brazilian football team colors */
:root {
  --br-cam: #000000; --br-cam-alt: #FFFFFF;
  --br-cru: #0038A8; --br-cru-alt: #FFFFFF;
  --br-cor: #000000; --br-cor-alt: #FFFFFF;
  --br-pal: #006437; --br-pal-alt: #FFFFFF;
  --br-sao: #CC1014; --br-sao-alt: #000000;
  --br-fla: #CC1014; --br-fla-alt: #000000;
  --br-flu: #6B2D8B; --br-flu-alt: #C8102E;
  --br-bot: #1A1A1A; --br-bot-alt: #FFFFFF;
}
```

- [ ] **Step 3: Atualizar `.landing-title` para usar Syne**

Localizar a regra `.landing-title` (aproximadamente linha 343) e substituir:
```css
.landing-title {
  font-family: var(--font-mono);
  font-size: 52px;
  font-weight: 800;
  letter-spacing: -0.04em;
  line-height: 1;
  color: var(--text);
  margin-bottom: 8px;
}
```
Por:
```css
.landing-title {
  font-family: var(--font-display);
  font-size: 56px;
  font-weight: 800;
  letter-spacing: -0.03em;
  line-height: 1;
  color: var(--text);
  margin-bottom: 8px;
}
```

- [ ] **Step 4: Verificar no browser**

Abrir o arquivo. A landing page deve ter fundo `#F8F8F6` (off-white quente), título "ODDS ARENA" em Syne (fonte geométrica, diferente da mono anterior), e o botão em verde escuro.

---

## Task 3: Substituir SVG do fundo (basquete → futebol)

**Arquivos:**
- Modify: `Odds Arena.html` — seção `.court-bg::before` e o SVG inline

- [ ] **Step 1: Atualizar gradiente do court-bg::before**

Localizar `.court-bg::before` (aproximadamente linha 84) e substituir o background por:

```css
.court-bg::before {
  content: '';
  position: absolute;
  inset: 0;
  background:
    repeating-linear-gradient(
      90deg,
      transparent 0px,
      transparent 39px,
      rgba(26, 107, 60, 0.04) 39px,
      rgba(26, 107, 60, 0.04) 40px
    ),
    repeating-linear-gradient(
      0deg,
      transparent 0px,
      transparent 39px,
      rgba(26, 107, 60, 0.03) 39px,
      rgba(26, 107, 60, 0.03) 40px
    ),
    linear-gradient(180deg, rgba(200, 230, 210, 0.08) 0%, rgba(240, 248, 242, 0.04) 100%);
  background-color: var(--bg);
}
```

- [ ] **Step 2: Substituir SVG inline do campo**

Localizar o bloco HTML `<div class="court-bg">` (aproximadamente linha 1061) e substituir o SVG interno (as linhas de basquete) por linhas de campo de futebol:

```html
<div class="court-bg">
  <div class="court-lines">
    <svg viewBox="0 0 1600 900" fill="none" xmlns="http://www.w3.org/2000/svg">
      <!-- Field border -->
      <rect x="60" y="60" width="1480" height="780" stroke="#1A6B3C" stroke-width="2" fill="none"/>
      <!-- Center line -->
      <line x1="800" y1="60" x2="800" y2="840" stroke="#1A6B3C" stroke-width="2"/>
      <!-- Center circle -->
      <circle cx="800" cy="450" r="110" stroke="#1A6B3C" stroke-width="2" fill="none"/>
      <circle cx="800" cy="450" r="5" fill="#1A6B3C"/>
      <!-- Left penalty area -->
      <rect x="60" y="270" width="200" height="360" stroke="#1A6B3C" stroke-width="1.5" fill="none"/>
      <!-- Right penalty area -->
      <rect x="1340" y="270" width="200" height="360" stroke="#1A6B3C" stroke-width="1.5" fill="none"/>
      <!-- Left goal area -->
      <rect x="60" y="360" width="70" height="180" stroke="#1A6B3C" stroke-width="1.5" fill="none"/>
      <!-- Right goal area -->
      <rect x="1470" y="360" width="70" height="180" stroke="#1A6B3C" stroke-width="1.5" fill="none"/>
      <!-- Left penalty arc -->
      <path d="M 260 340 Q 320 450 260 560" stroke="#1A6B3C" stroke-width="1.5" fill="none"/>
      <!-- Right penalty arc -->
      <path d="M 1340 340 Q 1280 450 1340 560" stroke="#1A6B3C" stroke-width="1.5" fill="none"/>
      <!-- Corner arcs -->
      <path d="M 60 90 Q 90 60 120 60" stroke="#1A6B3C" stroke-width="1.5" fill="none"/>
      <path d="M 1480 60 Q 1510 60 1540 90" stroke="#1A6B3C" stroke-width="1.5" fill="none"/>
      <path d="M 60 810 Q 60 840 90 840" stroke="#1A6B3C" stroke-width="1.5" fill="none"/>
      <path d="M 1510 840 Q 1540 840 1540 810" stroke="#1A6B3C" stroke-width="1.5" fill="none"/>
    </svg>
  </div>
</div>
```

- [ ] **Step 3: Verificar no browser**

O fundo da aplicação deve mostrar linhas de campo de futebol em verde muito sutil (opacidade 0.06). Não deve parecer um campo literal — apenas textura de fundo.

---

## Task 4: Dados JS — times, jogos, jogadores, props

**Arquivos:**
- Modify: `Odds Arena.html:1285–1335`

- [ ] **Step 1: Substituir NBA_TEAMS por BR_TEAMS**

Substituir o bloco `const NBA_TEAMS = { ... };` (linhas 1285–1302) por:

```javascript
const BR_TEAMS = {
  CAM: { name: 'Atlético Mineiro', city: 'Belo Horizonte', color: '#000000', alt: '#FFFFFF' },
  CRU: { name: 'Cruzeiro', city: 'Belo Horizonte', color: '#0038A8', alt: '#FFFFFF' },
  COR: { name: 'Corinthians', city: 'São Paulo', color: '#111111', alt: '#FFFFFF' },
  PAL: { name: 'Palmeiras', city: 'São Paulo', color: '#006437', alt: '#FFFFFF' },
  SAO: { name: 'São Paulo', city: 'São Paulo', color: '#CC1014', alt: '#000000' },
  FLA: { name: 'Flamengo', city: 'Rio de Janeiro', color: '#CC1014', alt: '#000000' },
  FLU: { name: 'Fluminense', city: 'Rio de Janeiro', color: '#6B2D8B', alt: '#C8102E' },
  BOT: { name: 'Botafogo', city: 'Rio de Janeiro', color: '#1A1A1A', alt: '#FFFFFF' },
};
```

- [ ] **Step 2: Substituir LIVE_GAMES**

Substituir o bloco `const LIVE_GAMES = [ ... ];` (linhas 1304–1313) por:

```javascript
const LIVE_GAMES = [
  { away: 'CRU', home: 'CAM', awayScore: 0, homeScore: 1, minute: 34, period: '1T', featured: true },
  { away: 'FLA', home: 'PAL', awayScore: 2, homeScore: 1, minute: 67, period: '2T' },
  { away: 'COR', home: 'SAO', awayScore: 0, homeScore: 0, minute: 12, period: '1T' },
  { away: 'FLU', home: 'BOT', awayScore: 1, homeScore: 2, minute: 78, period: '2T' },
];
```

- [ ] **Step 3: Substituir PLAYERS**

Substituir o bloco `const PLAYERS = [ ... ];` (linhas 1315–1320) por:

```javascript
const PLAYERS = [
  { name: 'Você', tag: 'Host', color: '#1A6B3C', initial: 'V' },
  { name: 'Galo_Fan', tag: 'Pronto', color: '#0038A8', initial: 'G' },
  { name: 'CruzeiroBH', tag: 'Pronto', color: '#CC1014', initial: 'C' },
  { name: 'FlaFlu_RJ', tag: 'Pronto', color: '#6B2D8B', initial: 'F' },
];
```

- [ ] **Step 4: Substituir MARKETS**

Substituir o bloco `const MARKETS = [ ... ];` (linhas 1322–1335) por:

```javascript
const MARKETS = [
  { id: 1, prop: 'Atlético vence', teams: ['CAM','CRU'], odds: '-125', payout: 1.8, cost: 80, longshot: false },
  { id: 2, prop: 'Cruzeiro vence', teams: ['CRU','CAM'], odds: '+130', payout: 2.3, cost: 70, longshot: false },
  { id: 3, prop: 'Empate', teams: ['CRU','CAM'], odds: '+240', payout: 3.4, cost: 45, longshot: false },
  { id: 4, prop: 'Hulk marca 1+', teams: ['CAM','CRU'], odds: '+150', payout: 2.5, cost: 68, longshot: false },
  { id: 5, prop: 'Matheus Pereira dá assistência', teams: ['CRU','CAM'], odds: '+175', payout: 2.8, cost: 62, longshot: false },
  { id: 6, prop: 'Kaio Jorge marca 1+', teams: ['CRU','CAM'], odds: '+210', payout: 3.1, cost: 52, longshot: false },
  { id: 7, prop: 'Mais de 2.5 gols', teams: ['CRU','CAM'], odds: '-110', payout: 1.9, cost: 90, longshot: false },
  { id: 8, prop: 'Menos de 2.5 gols', teams: ['CRU','CAM'], odds: '-118', payout: 1.85, cost: 84, longshot: false },
  { id: 9, prop: 'Atlético vence por 2+', teams: ['CAM','CRU'], odds: '+340', payout: 4.4, cost: 32, longshot: false },
  { id: 10, prop: 'Hulk marca de falta', teams: ['CAM','CRU'], odds: '+680', payout: 7.8, cost: 22, longshot: true },
  { id: 11, prop: 'Nenhum gol no 1º tempo', teams: ['CRU','CAM'], odds: '+520', payout: 6.2, cost: 27, longshot: true },
  { id: 12, prop: 'Hat-trick na partida', teams: ['CRU','CAM'], odds: '+1200', payout: 13.0, cost: 15, longshot: true },
];
```

- [ ] **Step 5: Atualizar todas as referências a NBA_TEAMS no JS**

Usar busca global e substituir todas as ocorrências de `NBA_TEAMS` por `BR_TEAMS` no arquivo. Há ocorrências em: `buildTicker()`, `buildScoreboard()`, `buildDraftTable()`, e na live screen HTML (linha ~1215).

- [ ] **Step 6: Verificar no browser**

Abrir o arquivo. Na landing, clicar em "CRIAR LOBBY" → "ENTRAR NO DRAFT". O draft board deve mostrar as 12 props de futebol com times CRU/CAM. O ticker deve mostrar os 4 jogos com times brasileiros.

---

## Task 5: Estado inicial do jogo

**Arquivos:**
- Modify: `Odds Arena.html:1340–1356`

- [ ] **Step 1: Atualizar state inicial**

Localizar o bloco `const state = { ... };` e substituir as propriedades de clock/score:

```javascript
const state = {
  screen: 'landing',
  salaryCap: 500,
  salaryRemaining: 500,
  maxPicks: 5,
  selectedPicks: [],
  playerScores: [0, 0, 0, 0],
  liveOdds: {},
  betStatuses: {},
  muted: false,
  audioCtx: null,
  gameInterval: null,
  liveSecond: 0,
  gameScore: { away: 0, home: 1 },
  period: '1T',
  minute: 34,
};
```

---

## Task 6: HTML strings — todas as telas

**Arquivos:**
- Modify: `Odds Arena.html` — seções HTML das 5 telas

- [ ] **Step 1: Landing page — logo SVG e textos**

Substituir o SVG do logo (bola de basquete, linhas ~1117–1123) por um SVG de bola de futebol minimalista:

```html
<div class="landing-logo">
  <svg viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg">
    <circle cx="32" cy="32" r="30" stroke="#1A6B3C" stroke-width="2.5"/>
    <polygon points="32,14 38,24 48,24 42,34 46,44 32,38 18,44 22,34 16,24 26,24" stroke="#1A6B3C" stroke-width="1.8" fill="none"/>
  </svg>
</div>
```

Substituir:
```html
<p class="landing-sub">Real-time multiplayer NBA prediction game</p>
<button class="btn-primary" id="btn-create-lobby" aria-label="Create a new game lobby">CREATE LOBBY</button>
```
Por:
```html
<p class="landing-sub">Previsão em tempo real · Futebol Brasileiro</p>
<div class="landing-badge">MG · SP · RJ</div>
<button class="btn-primary" id="btn-create-lobby" aria-label="Criar uma nova sala">CRIAR LOBBY</button>
```

Substituir labels das landing stats:
```html
<div class="landing-stat-label">Players</div>
```
Por:
```html
<div class="landing-stat-label">Jogadores</div>
```

```html
<div class="landing-stat-label">Salary Cap</div>
```
Manter como "Salary Cap" (termo técnico mantido em inglês conforme spec).

```html
<div class="landing-stat-label">Markets</div>
```
Por:
```html
<div class="landing-stat-label">Mercados</div>
```

- [ ] **Step 2: Adicionar estilo do badge MG·SP·RJ**

No CSS, após `.landing-stats { ... }`, adicionar:

```css
.landing-badge {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-family: var(--font-mono);
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 0.12em;
  color: var(--text-muted);
  border: 1px solid var(--border);
  padding: 4px 14px;
  border-radius: 20px;
  margin-bottom: 32px;
  background: var(--surface);
}
```

- [ ] **Step 3: Lobby — textos**

Substituir:
```html
<div class="section-header">Lobby</div>
```
Manter como "Lobby" (termo técnico).

Substituir:
```html
<div class="lobby-title">Game #4821</div>
<div class="lobby-desc">Waiting for players to ready up...</div>
```
Por:
```html
<div class="lobby-title">Sala #4821</div>
<div class="lobby-desc">Aguardando jogadores...</div>
```

Substituir:
```html
<div class="setting-value">BOS vs NYK</div>
```
Por:
```html
<div class="setting-value">CRU vs CAM</div>
```

Substituir:
```html
<div class="setting-label">Format</div>
<div class="setting-value">Live Props</div>
```
Por:
```html
<div class="setting-label">Formato</div>
<div class="setting-value">Props ao Vivo</div>
```

Substituir:
```html
<button class="btn-primary" id="btn-start-draft" style="width:100%">ENTER DRAFT</button>
```
Por:
```html
<button class="btn-primary" id="btn-start-draft" style="width:100%">ENTRAR NO DRAFT</button>
```

- [ ] **Step 4: Draft — labels**

Substituir:
```html
<div class="section-header">Draft Board</div>
```
Manter como "Draft Board" (termo técnico).

Substituir label da coluna `<th>Prop</th><th>Matchup</th>`:
```html
<th>Prop</th>
<th>Matchup</th>
<th>Odds</th>
<th>Payout</th>
<th>Cost</th>
```
Por:
```html
<th>Prop</th>
<th>Jogo</th>
<th>Odds</th>
<th>Retorno</th>
<th>Custo</th>
```

Substituir:
```html
<button class="btn-secondary" id="btn-clear-draft">CLEAR</button>
<button class="btn-primary btn-disabled" id="btn-lock-draft">LOCK PICKS</button>
```
Por:
```html
<button class="btn-secondary" id="btn-clear-draft">LIMPAR</button>
<button class="btn-primary btn-disabled" id="btn-lock-draft">CONFIRMAR PICKS</button>
```

- [ ] **Step 5: Live screen — matchup hardcoded e labels**

Substituir o bloco do matchup hardcoded (aproximadamente linhas 1214–1224):
```html
<div class="live-matchup">
  <span class="team-badge" style="background:var(--nba-bos)">BOS</span>
  <span>vs</span>
  <span class="team-badge" style="background:var(--nba-nyk)">NYK</span>
</div>
<div class="live-game-score" id="live-main-score">87 - 82</div>
```
Por:
```html
<div class="live-matchup">
  <span class="team-badge" style="background:var(--br-cru)">CRU</span>
  <span>×</span>
  <span class="team-badge" style="background:var(--br-cam)">CAM</span>
</div>
<div class="live-game-score" id="live-main-score">0 × 1</div>
```

Substituir:
```html
<div class="live-period-label" id="live-quarter">Q3</div>
<div class="live-period-clock" id="live-clock">4:22</div>
```
Por:
```html
<div class="live-period-label" id="live-quarter">1T</div>
<div class="live-period-clock" id="live-clock">34'</div>
```

Substituir:
```html
<div class="section-header">Your Bets</div>
```
Por:
```html
<div class="section-header">Suas Apostas</div>
```

Substituir:
```html
<div class="section-header">Live Feed</div>
```
Por:
```html
<div class="section-header">Ao Vivo</div>
```

Substituir:
```html
<div class="section-header">Leaderboard</div>
```
Manter como "Leaderboard" (termo técnico).

Substituir as labels do progress bar (Q1/Q2/Q3/Q4):
```html
<div class="progress-labels">
  <span>Q1</span><span>Q2</span><span>Q3</span><span>Q4</span>
</div>
```
Por:
```html
<div class="progress-labels">
  <span>Início</span><span>1T</span><span>2T</span><span>Final</span>
</div>
```

- [ ] **Step 6: Resolution — textos**

Substituir:
```html
<button class="btn-primary" id="btn-play-again">PLAY AGAIN</button>
```
Por:
```html
<button class="btn-primary" id="btn-play-again">JOGAR NOVAMENTE</button>
```

- [ ] **Step 7: Verificar no browser — todas as telas**

Percorrer todas as telas e confirmar que todos os textos estão em português, exceto termos técnicos mantidos (odds, longshot, salary cap, HIT, MISS, draft, leaderboard).

---

## Task 7: Lógica do jogo — clock de futebol

**Arquivos:**
- Modify: `Odds Arena.html:1682–1830`

- [ ] **Step 1: Atualizar startLiveGame() — progressão de tempo**

Localizar a função `startLiveGame()` e substituir a lógica de quarter/clock por minutos de futebol. Substituir o bloco interno do `setInterval` onde está a lógica de quarter (aproximadamente linhas 1692–1706):

```javascript
// Progressão de minutos (34' → 90'+)
const startMinute = 34;
const currentMinute = Math.min(90, startMinute + state.liveSecond);
const isStoppage = currentMinute >= 90;

if (currentMinute <= 45) {
  state.period = '1T';
} else if (currentMinute <= 90) {
  state.period = '2T';
} else {
  state.period = 'FINAL';
}

const minuteDisplay = isStoppage
  ? `90'+`
  : `${currentMinute}'`;

document.getElementById('live-clock').textContent = state.period === 'FINAL' ? '90\'' : minuteDisplay;
document.getElementById('live-quarter').textContent = state.period;
```

- [ ] **Step 2: Atualizar score display para formato futebol**

Localizar onde o placar principal é atualizado (linha ~1720):
```javascript
document.getElementById('live-main-score').textContent =
  `${state.gameScore.away} - ${state.gameScore.home}`;
```
Substituir por:
```javascript
document.getElementById('live-main-score').textContent =
  `${state.gameScore.away} × ${state.gameScore.home}`;
```

- [ ] **Step 3: Atualizar feed de eventos — jogadores e times**

Localizar o bloco que gera eventos de score no feed (aproximadamente linhas 1726–1731):

```javascript
const scorer = isAway ? 'CRU' : 'CAM';
const players = isAway
  ? ['Matheus Pereira', 'Kaio Jorge', 'Barreal', 'Ramiro', 'Lautaro']
  : ['Hulk', 'Paulinho', 'Vargas', 'Guilherme Arana', 'Júnior Alonso'];
const player = players[Math.floor(Math.random() * players.length)];
addFeedEvent('score', `<strong>⚽ ${player}</strong> (${scorer} ${state.gameScore.away}×${state.gameScore.home} · ${minuteDisplay})`);
```

- [ ] **Step 4: Atualizar reset em btnPlayAgain**

Localizar o event listener do `btn-play-again` (aproximadamente linhas 1970–1988) e atualizar os valores de reset:

```javascript
state.gameScore = { away: 0, home: 1 };
state.period = '1T';
state.minute = 34;
state.liveSecond = 0;
```

Remover as linhas que resetam `clockSec` e `quarter` pois essas propriedades não existem mais no novo state.

- [ ] **Step 5: Verificar no browser**

Iniciar o jogo completo: landing → lobby → draft (selecionar 2-3 props) → confirmar → jogo ao vivo. Confirmar que:
- O timer mostra minutos crescentes (34', 35', ...)
- O placar usa `×` em vez de `-`
- O feed mostra nomes de jogadores brasileiros
- O período muda de "1T" para "2T" após os 45 minutos

---

## Task 8: showResolution() — game story em português

**Arquivos:**
- Modify: `Odds Arena.html:1835–1880`

- [ ] **Step 1: Atualizar game story**

Localizar a função `showResolution()` e substituir o bloco de geração da `story` (aproximadamente linhas 1869–1879):

```javascript
const winner = sorted[0];
document.getElementById('resolution-title').textContent = winner.name === 'Você' ? 'VITÓRIA!' : 'FINAL';
document.getElementById('resolution-subtitle').textContent =
  `${winner.name} dominou com ${winner.score} pontos`;

const hits = state.selectedPicks.filter(id => state.betStatuses[id] === 'hit');
const misses = state.selectedPicks.filter(id => state.betStatuses[id] === 'miss');
const bigHit = hits.map(id => MARKETS.find(m => m.id === id)).sort((a, b) => b.payout - a.payout)[0];

const scoreStr = `${state.gameScore.away}×${state.gameScore.home}`;
let story = `Clássico Mineiro encerrado: CAM ${state.gameScore.home} × ${state.gameScore.away} CRU. `;
if (hits.length > 0 && bigHit) {
  story += `Sua maior acerto foi "${bigHit.prop}" a ${bigHit.payout}x, rendendo $${Math.round(bigHit.payout * bigHit.cost)}. `;
}
story += `Você acertou ${hits.length} de ${state.selectedPicks.length} apostas. `;
if (sorted[0].name === 'Você') {
  story += `Performance dominante — você leu o jogo melhor que qualquer um na sala.`;
} else {
  story += `${sorted[0].name} assumiu a liderança nos minutos finais com escolhas decisivas.`;
}
document.getElementById('game-story-text').textContent = story;
```

- [ ] **Step 2: Atualizar label "Game Story"**

Localizar no HTML:
```html
<div class="game-story-title">Game Story</div>
```
Substituir por:
```html
<div class="game-story-title">Resumo da Partida</div>
```

- [ ] **Step 3: Verificar no browser**

Completar uma partida inteira até a tela final. Confirmar que:
- O título mostra "VITÓRIA!" quando o usuário vence, "FINAL" caso contrário
- O subtítulo está em português
- O resumo menciona "Clássico Mineiro" e os placares corretos
- O botão mostra "JOGAR NOVAMENTE"

---

## Task 9: Confetti — cores dos times brasileiros

**Arquivos:**
- Modify: `Odds Arena.html:1891`

- [ ] **Step 1: Substituir array de cores do confetti**

Localizar a linha:
```javascript
const teamColors = ['#007A33', '#006BB6', '#ea5a20', '#FDB927', '#CE1141', '#552583', '#FFC72C', '#98002E'];
```
Substituir por:
```javascript
const teamColors = ['#000000', '#0038A8', '#006437', '#CC1014', '#6B2D8B', '#1A6B3C', '#FFFFFF', '#C8102E'];
```

---

## Task 10: Remover script Perplexity e limpeza final

**Arquivos:**
- Modify: `Odds Arena.html:1996–2057`

- [ ] **Step 1: Remover script de inline edit da Perplexity**

Localizar e remover completamente o bloco (aproximadamente linhas 1996–2057):
```html
<script data-pplx-inline-edit>
(function(){
  ...
})();
</script>
```
O arquivo deve terminar com `</body></html>` logo após o fechamento do script principal.

- [ ] **Step 2: Atualizar ticker e scoreboard para futebol**

Verificar a função `buildTicker()`. O ticker usa `g.quarter` e `g.clock` — no novo `LIVE_GAMES`, esses campos passam a ser `g.minute` e `g.period`. Atualizar a linha do ticker-item dentro de `buildTicker()`:

```javascript
html += `<div class="ticker-item">
  <span class="team-abbr" style="color:${BR_TEAMS[g.away].color}">${g.away}</span>
  <span class="score">${g.awayScore}</span>
  <span style="color:rgba(255,255,255,0.3)">×</span>
  <span class="score">${g.homeScore}</span>
  <span class="team-abbr" style="color:${BR_TEAMS[g.home].color}">${g.home}</span>
  <span class="period">${g.period} ${g.minute}'</span>
</div>`;
```

E na função `buildScoreboard()`, atualizar:
```javascript
<span class="sb-quarter">${g.period}</span>
<span class="sb-clock">${g.minute}'</span>
```

- [ ] **Step 3: Verificar ticker no browser**

O ticker preto no topo deve mostrar: `CRU × CAM`, `FLA × PAL`, `COR × SAO`, `FLU × BOT` com minutos e período (1T/2T).

- [ ] **Step 4: Verificação final completa**

Percorrer o fluxo completo uma vez:
1. Landing — logo, título Syne, badge MG·SP·RJ, botão verde
2. Lobby — Sala #4821, 4 jogadores com nomes BR, CRU vs CAM
3. Draft — 12 props em português, times CRU/CAM, CONFIRMAR PICKS ativo
4. Jogo ao vivo — placar `0×1`, timer em minutos, feed com nomes BR
5. Final — "VITÓRIA!" ou "FINAL", resumo em português, "JOGAR NOVAMENTE"

Confirmar que não aparecem referências a NBA, Lakers, Celtics, BOS, NYK, ou quaisquer dados originais.

- [ ] **Step 5: Verificar no mobile (resize da janela)**

Redimensionar o browser para ~390px de largura. Confirmar que as telas não quebram (o layout já é responsivo no original — apenas garantir que as mudanças não introduziram overflow horizontal).

---

## Checklist de Spec Coverage

| Requisito da Spec | Task |
|---|---|
| Light theme `#F8F8F6` | Task 2 |
| Fonte Syne nos títulos | Task 1 + Task 2 |
| Accent verde `#1A6B3C` | Task 2 |
| Campo de futebol no fundo | Task 3 |
| 8 times MG/SP/RJ | Task 4 |
| Jogo destaque CRU×CAM | Task 4 + Task 6 |
| 12 props de futebol | Task 4 |
| Jogadores IA BR | Task 4 |
| Interface em português | Task 6 |
| Termos EN mantidos | Task 6 |
| Timer em minutos | Task 7 |
| Placar `×` em vez de `-` | Task 7 |
| Feed com jogadores BR | Task 7 |
| Game story em PT-BR | Task 8 |
| Confetti com cores BR | Task 9 |
| Remoção script Perplexity | Task 10 |
| Ticker futebol | Task 10 |
