# Odds Arena — Melhorias (19 itens) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Aplicar 19 melhorias visuais, técnicas e de conteúdo ao arquivo `index.html` do projeto Odds Arena.

**Architecture:** Aplicação single-file (HTML + CSS + JS inline). Todas as mudanças ocorrem em `index.html`. Nenhuma dependência nova é introduzida. Grupos ordenados por risco: fixes triviais primeiro, lógica de jogo por último.

**Tech Stack:** Vanilla HTML5 / CSS3 / ES6+, Web Audio API, Canvas API, Google Fonts CDN.

---

## Arquivo envolvido

- Modify: `C:\ws\Odds\index.html` — único arquivo, todas as tarefas o modificam

---

## Task 1: Meta tags — favicon, OG e Twitter card

**Melhoria #6**

**Files:**
- Modify: `C:\ws\Odds\index.html` (seção `<head>`, linhas 1–14)

- [ ] **Step 1: Adicionar favicon SVG inline, og:image, og:url e twitter:card**

Localizar o bloco de meta tags no `<head>` (antes da linha `<link rel="preconnect"...>`) e substituir:

```html
<title>Odds Arena · Futebol Brasileiro</title>
<meta name="description" content="Previsão em tempo real do futebol brasileiro. Monte seu draft, escolha suas apostas e acompanhe o Clássico Mineiro ao vivo.">
<meta property="og:title" content="Odds Arena · Futebol Brasileiro">
<meta property="og:description" content="Jogo de previsão em tempo real — Clássico Mineiro, Derby Paulista e mais. Escolha suas props e dispute com outros torcedores.">
<meta property="og:type" content="website">
<meta name="theme-color" content="#1A6B3C">
```

Por:

```html
<title>Odds Arena · Futebol Brasileiro</title>
<meta name="description" content="Previsão em tempo real do futebol brasileiro. Monte seu draft, escolha suas apostas e acompanhe o Clássico Mineiro ao vivo.">
<meta property="og:title" content="Odds Arena · Futebol Brasileiro">
<meta property="og:description" content="Jogo de previsão em tempo real — Clássico Mineiro, Derby Paulista e mais. Escolha suas props e dispute com outros torcedores.">
<meta property="og:type" content="website">
<meta property="og:url" content="https://odds-arena.vercel.app">
<meta property="og:image" content="https://odds-arena.vercel.app/preview.png">
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Odds Arena · Futebol Brasileiro">
<meta name="twitter:description" content="Jogo de previsão em tempo real — Clássico Mineiro, Derby Paulista e mais.">
<meta name="theme-color" content="#1A6B3C">
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>⚽</text></svg>">
```

- [ ] **Step 2: Verificar no browser**

Abrir `index.html` no browser e verificar que o favicon ⚽ aparece na aba.

---

## Task 2: Google Fonts não-bloqueante

**Melhoria #13**

**Files:**
- Modify: `C:\ws\Odds\index.html` (linhas 12–14)

- [ ] **Step 1: Tornar o carregamento das fontes não-bloqueante**

Substituir:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@700;800&family=Inter:wght@400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500;600;700;800&display=swap" rel="stylesheet">
```

Por:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Syne:wght@700;800&family=Inter:wght@400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500;600;700;800&display=swap" media="print" onload="this.media='all'">
<noscript><link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Syne:wght@700;800&family=Inter:wght@400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500;600;700;800&display=swap"></noscript>
```

- [ ] **Step 2: Verificar que as fontes carregam**

Recarregar no browser — Syne, Inter e JetBrains Mono devem aparecer normalmente após o carregamento.

---

## Task 3: Ticker — cores escuras de times visíveis

**Melhoria #1**

**Files:**
- Modify: `C:\ws\Odds\index.html` (função `buildTicker`, JS)

- [ ] **Step 1: Usar cor alt para texto de times no ticker escuro**

Localizar a função `buildTicker()` no JS e substituir o template literal do `ticker-item`:

```js
html += `<div class="ticker-item">
  <span class="team-abbr" style="color:${BR_TEAMS[g.away].color}">${g.away}</span>
  <span class="score">${g.awayScore}</span>
  <span style="color:rgba(255,255,255,0.3)">×</span>
  <span class="score">${g.homeScore}</span>
  <span class="team-abbr" style="color:${BR_TEAMS[g.home].color}">${g.home}</span>
  <span class="period">${g.period} ${g.minute}'</span>
</div>`;
```

Por:

```js
html += `<div class="ticker-item">
  <span class="team-abbr" style="color:${BR_TEAMS[g.away].alt}">${g.away}</span>
  <span class="score">${g.awayScore}</span>
  <span style="color:rgba(255,255,255,0.3)">×</span>
  <span class="score">${g.homeScore}</span>
  <span class="team-abbr" style="color:${BR_TEAMS[g.home].alt}">${g.home}</span>
  <span class="period">${g.period} ${g.minute}'</span>
</div>`;
```

- [ ] **Step 2: Verificar no browser**

No ticker escuro no topo, todos os nomes de times (CAM, BOT, COR, etc.) devem ser legíveis em branco.

---

## Task 4: Confetti — remover branco da paleta

**Melhoria #15**

**Files:**
- Modify: `C:\ws\Odds\index.html` (função `startConfetti`, JS)

- [ ] **Step 1: Remover `#FFFFFF` do array de cores do confetti**

Localizar em `startConfetti()`:

```js
const teamColors = ['#000000', '#0038A8', '#006437', '#CC1014', '#6B2D8B', '#1A6B3C', '#FFFFFF', '#C8102E'];
```

Substituir por:

```js
const teamColors = ['#000000', '#0038A8', '#006437', '#CC1014', '#6B2D8B', '#1A6B3C', '#F5C518', '#C8102E'];
```

(troca o branco por amarelo-ouro, que é vibrante sobre o modal branco e remete às cores do troféu)

- [ ] **Step 2: Verificar no browser**

Completar uma partida e confirmar que o confetti é visível sobre o modal branco — sem partículas invisíveis.

---

## Task 5: Badge Corinthians — visibilidade no scoreboard

**Melhoria #11**

**Files:**
- Modify: `C:\ws\Odds\index.html` (CSS, seção `.team-badge`)

- [ ] **Step 1: Adicionar border fallback para badges com fundo branco**

Localizar a regra `.team-badge` no CSS:

```css
.team-badge {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-mono);
  font-size: 11px;
  font-weight: 800;
  letter-spacing: 0.04em;
  padding: 2px 6px;
  border-radius: 3px;
  line-height: 1;
  box-shadow: inset 0 0 0 1px rgba(0,0,0,0.12);
}
```

Substituir por:

```css
.team-badge {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-mono);
  font-size: 11px;
  font-weight: 800;
  letter-spacing: 0.04em;
  padding: 2px 6px;
  border-radius: 3px;
  line-height: 1;
  box-shadow: inset 0 0 0 1px rgba(0,0,0,0.18);
  border: 1px solid rgba(0,0,0,0.10);
}
```

- [ ] **Step 2: Verificar no browser**

O badge de COR (Corinthians, fundo branco) deve ter uma borda sutil visível no scoreboard strip branco.

---

## Task 6: CSS — jogo em destaque no scoreboard

**Melhoria #2**

**Files:**
- Modify: `C:\ws\Odds\index.html` (CSS, após regra `.sb-game:hover`)

- [ ] **Step 1: Adicionar regra CSS para `.sb-game.featured`**

Após a regra `.sb-game:hover { background: var(--surface-alt); }`, adicionar:

```css
.sb-game.featured {
  background: var(--accent-light);
  border-right: 1px solid var(--border);
  position: relative;
}
.sb-game.featured::after {
  content: '★';
  position: absolute;
  top: 3px;
  right: 6px;
  font-size: 8px;
  color: var(--accent);
  opacity: 0.7;
}
```

- [ ] **Step 2: Verificar no browser**

No scoreboard strip, o jogo CRU × CAM deve ter fundo verde-claro e um ★ discreto no canto superior direito.

---

## Task 7: Mute button — reposicionamento visual

**Melhoria #9**

**Files:**
- Modify: `C:\ws\Odds\index.html` (CSS, regra `.mute-btn`)

- [ ] **Step 1: Mover o botão para dentro da scoreboard strip**

Localizar `.mute-btn` no CSS:

```css
.mute-btn {
  position: fixed;
  top: 4px;
  right: 12px;
  z-index: 200;
  width: 28px; height: 28px;
  border-radius: 50%;
  border: 1px solid var(--border);
  background: var(--surface);
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background var(--transition-interactive),
              border-color var(--transition-interactive);
}
```

Substituir por:

```css
.mute-btn {
  position: fixed;
  top: 50px;
  right: 12px;
  z-index: 200;
  width: 28px; height: 28px;
  border-radius: 50%;
  border: 1px solid var(--border);
  background: var(--surface);
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background var(--transition-interactive),
              border-color var(--transition-interactive);
  box-shadow: 0 1px 4px rgba(0,0,0,0.08);
}
```

(`top: 50px` centraliza o botão verticalmente dentro da scoreboard strip que vai de 36px a 92px)

- [ ] **Step 2: Verificar no browser**

O botão de mute deve aparecer na borda direita da scoreboard strip, sem sobrepor o ticker escuro.

---

## Task 8: Landing — reordenar stats antes do CTA

**Melhoria #8**

**Files:**
- Modify: `C:\ws\Odds\index.html` (HTML do `#screen-landing`)

- [ ] **Step 1: Mover `.landing-stats` para antes do botão CTA**

Localizar o HTML da landing page dentro de `#screen-landing`. A estrutura atual é:

```html
<div class="landing-badge">MG · SP · RJ</div>
<button class="btn-primary" id="btn-create-lobby" ...>CRIAR LOBBY</button>
<div class="landing-stats">
  ...
</div>
```

Reorganizar para:

```html
<div class="landing-stats">
  ...
</div>
<div class="landing-badge">MG · SP · RJ</div>
<button class="btn-primary" id="btn-create-lobby" ...>CRIAR LOBBY</button>
```

(stats → badge → CTA: o usuário vê os números primeiro, depois o badge de estados, depois o botão)

- [ ] **Step 2: Ajustar margin-top dos stats**

O `.landing-stats` tinha `margin-top: 48px` (pois ficava abaixo do botão). Agora precisa de margem abaixo. No CSS, substituir:

```css
.landing-stats {
  display: flex;
  gap: 40px;
  margin-top: 48px;
}
```

Por:

```css
.landing-stats {
  display: flex;
  gap: 40px;
  margin-bottom: 36px;
}
```

- [ ] **Step 3: Verificar no browser**

Na landing: título → subtítulo → **stats (4 / $500 / 12)** → badge MG·SP·RJ → botão CRIAR LOBBY.

---

## Task 9: Landing — count-up animation nos stats

**Melhoria #7**

**Files:**
- Modify: `C:\ws\Odds\index.html` (JS, função init e nova função `animateStats`)

- [ ] **Step 1: Adicionar IDs aos elementos de stat na landing**

Localizar os três `.landing-stat-val` no HTML e adicionar IDs:

```html
<div class="landing-stats">
  <div class="landing-stat">
    <div class="landing-stat-val" id="stat-players">4</div>
    <div class="landing-stat-label">Jogadores</div>
  </div>
  <div class="landing-stat">
    <div class="landing-stat-val" id="stat-cap">$500</div>
    <div class="landing-stat-label">Salary Cap</div>
  </div>
  <div class="landing-stat">
    <div class="landing-stat-val" id="stat-markets">12</div>
    <div class="landing-stat-label">Mercados</div>
  </div>
</div>
```

- [ ] **Step 2: Adicionar função `animateStats` no JS**

Logo antes da seção `/* INIT */` no final do JS, adicionar:

```js
/* ============================================
   STAT COUNT-UP ANIMATION
   ============================================ */
function animateCountUp(el, target, prefix, duration) {
  const start = performance.now();
  function step(now) {
    const elapsed = now - start;
    const progress = Math.min(elapsed / duration, 1);
    const eased = 1 - Math.pow(1 - progress, 3); // ease-out cubic
    const current = Math.round(eased * target);
    el.textContent = prefix + current;
    if (progress < 1) requestAnimationFrame(step);
    else el.textContent = prefix + target;
  }
  requestAnimationFrame(step);
}

function animateStats() {
  setTimeout(() => animateCountUp(document.getElementById('stat-players'), 4, '', 600), 100);
  setTimeout(() => animateCountUp(document.getElementById('stat-cap'), 500, '$', 800), 200);
  setTimeout(() => animateCountUp(document.getElementById('stat-markets'), 12, '', 700), 300);
}
```

- [ ] **Step 3: Chamar `animateStats()` na inicialização**

No final do script, após `buildScoreboard()`, adicionar:

```js
animateStats();
```

- [ ] **Step 4: Verificar no browser**

Ao carregar a página, os três stats devem animar de 0 até o valor final com um leve easing escalonado.

---

## Task 10: Lock draft button — `disabled` attribute real

**Melhoria #4**

**Files:**
- Modify: `C:\ws\Odds\index.html` (HTML e JS)

- [ ] **Step 1: Adicionar `disabled` no HTML inicial do botão**

Localizar no HTML:

```html
<button class="btn-primary btn-disabled" id="btn-lock-draft">CONFIRMAR PICKS</button>
```

Substituir por:

```html
<button class="btn-primary btn-disabled" id="btn-lock-draft" disabled>CONFIRMAR PICKS</button>
```

- [ ] **Step 2: Atualizar `updateDraftUI` para gerenciar o atributo**

Localizar em `updateDraftUI()`:

```js
const lockBtn = document.getElementById('btn-lock-draft');
if (state.selectedPicks.length > 0) {
  lockBtn.classList.remove('btn-disabled');
} else {
  lockBtn.classList.add('btn-disabled');
}
```

Substituir por:

```js
const lockBtn = document.getElementById('btn-lock-draft');
if (state.selectedPicks.length > 0) {
  lockBtn.classList.remove('btn-disabled');
  lockBtn.disabled = false;
} else {
  lockBtn.classList.add('btn-disabled');
  lockBtn.disabled = true;
}
```

- [ ] **Step 3: Garantir que o CSS de `btn-disabled` funciona com `button:disabled`**

No CSS, após a regra `.btn-disabled`, adicionar:

```css
.btn-primary:disabled {
  opacity: 0.45;
  cursor: not-allowed;
  transform: none;
}
```

- [ ] **Step 4: Verificar no browser**

Com nenhuma prop selecionada, o botão "CONFIRMAR PICKS" não deve ser ativável por Tab+Enter. Ao selecionar uma prop, deve ativar normalmente.

---

## Task 11: Lobby — randomizar número da sala

**Melhoria #10**

**Files:**
- Modify: `C:\ws\Odds\index.html` (HTML e JS)

- [ ] **Step 1: Adicionar ID ao título da sala no HTML**

Localizar:

```html
<div class="lobby-title">Sala #4821</div>
```

Substituir por:

```html
<div class="lobby-title" id="lobby-room-title">Sala #4821</div>
```

- [ ] **Step 2: Randomizar o número no `buildLobby()`**

No início da função `buildLobby()`, antes de `const list = ...`, adicionar:

```js
const roomNum = Math.floor(Math.random() * 9000) + 1000;
document.getElementById('lobby-room-title').textContent = `Sala #${roomNum}`;
```

- [ ] **Step 3: Verificar no browser**

Jogar duas vezes e confirmar que o número da sala muda a cada partida.

---

## Task 12: Lobby — animação de entrada dos players

**Melhoria #18**

**Files:**
- Modify: `C:\ws\Odds\index.html` (CSS e função `buildLobby`)

- [ ] **Step 1: Adicionar CSS para animação de entrada**

No bloco de CSS do lobby, após `.player-slot.you { ... }`, adicionar:

```css
@keyframes slot-appear {
  from { opacity: 0; transform: translateY(8px); }
  to   { opacity: 1; transform: translateY(0); }
}
.player-slot {
  animation: slot-appear 300ms var(--ease-out) both;
}
.player-slot[data-delay="0"] { animation-delay: 0ms; }
.player-slot[data-delay="1"] { animation-delay: 350ms; }
.player-slot[data-delay="2"] { animation-delay: 700ms; }
.player-slot[data-delay="3"] { animation-delay: 1050ms; }
```

- [ ] **Step 2: Adicionar tags e delays escalonados no `buildLobby()`**

Localizar o template literal do `player-slot` em `buildLobby()`:

```js
html += `<div class="player-slot${i === 0 ? ' you' : ''}">
  <div class="player-avatar" style="background:${p.color}">${p.initial}</div>
  <div class="player-name">${p.name}</div>
  <div class="player-tag">${p.tag}</div>
</div>`;
```

Substituir por:

```js
const tag = i === 0 ? p.tag : '...';
html += `<div class="player-slot${i === 0 ? ' you' : ''}" data-delay="${i}">
  <div class="player-avatar" style="background:${p.color}">${p.initial}</div>
  <div class="player-name">${p.name}</div>
  <div class="player-tag" id="player-tag-${i}">${tag}</div>
</div>`;
```

- [ ] **Step 3: Atualizar o status dos players com delay**

No final de `buildLobby()`, após `list.innerHTML = html;`, adicionar:

```js
// Simular players entrando na sala com delay
PLAYERS.forEach((p, i) => {
  if (i === 0) return; // "Você" já está pronto
  setTimeout(() => {
    const tagEl = document.getElementById(`player-tag-${i}`);
    if (tagEl) tagEl.textContent = p.tag;
  }, 400 + i * 350);
});
```

- [ ] **Step 4: Verificar no browser**

Ao entrar no lobby, os 4 players devem aparecer um a um, com "..." substituído por "Pronto" para os IAs após um pequeno delay.

---

## Task 13: Nomes dos goleadores — elenco atual

**Melhoria #19**

**Files:**
- Modify: `C:\ws\Odds\index.html` (função `startLiveGame`, JS)

- [ ] **Step 1: Atualizar listas de jogadores dos gols**

Localizar em `startLiveGame()`:

```js
const players = isAway
  ? ['Matheus Pereira', 'Kaio Jorge', 'Barreal', 'Ramiro', 'Lautaro']
  : ['Hulk', 'Paulinho', 'Vargas', 'Guilherme Arana', 'Júnior Alonso'];
```

Substituir por:

```js
const players = isAway
  ? ['Matheus Pereira', 'Kaio Jorge', 'Gabriel Barbosa', 'Lautaro Díaz', 'William']
  : ['Hulk', 'Paulinho', 'Vargas', 'Guilherme Arana', 'Eduardo Sasha'];
```

(Lautaro Díaz é argentino do Cruzeiro; removidos Barreal e Ramiro que não pertencem ao clube)

- [ ] **Step 2: Verificar no browser**

Durante o jogo ao vivo, os nomes dos goleadores no feed devem ser todos plausíveis para CRU e CAM.

---

## Task 14: FINAL period — corrigir timing

**Melhoria #3**

**Files:**
- Modify: `C:\ws\Odds\index.html` (função `startLiveGame`, JS)

- [ ] **Step 1: Aumentar `totalTicks` e ajustar progressão de minutos**

Localizar no início de `startLiveGame()`:

```js
state.liveSecond = 0;
const totalTicks = 30; // ~30 seconds of game time
```

Substituir por:

```js
state.liveSecond = 0;
const totalTicks = 56; // 34' → 90' = 56 minutos simulados em ~56 segundos reais
```

- [ ] **Step 2: Ajustar a condição de resolução de apostas para o novo total**

Localizar:

```js
if (state.liveSecond > 5 && resolvedCount < totalBets) {
  const activeBets = state.selectedPicks.filter(id => state.betStatuses[id] === 'active');
  if (activeBets.length > 0 && (Math.random() > 0.5 || state.liveSecond > 22)) {
```

Substituir por:

```js
if (state.liveSecond > 8 && resolvedCount < totalBets) {
  const activeBets = state.selectedPicks.filter(id => state.betStatuses[id] === 'active');
  if (activeBets.length > 0 && (Math.random() > 0.5 || state.liveSecond > 40)) {
```

(o threshold de força-resolução sobe de 22 para 40, mantendo a proporção com o novo total de 56 ticks)

- [ ] **Step 3: Verificar no browser**

O jogo ao vivo deve agora mostrar 1T, 2T e FINAL sequencialmente. O live clock deve chegar a `90'` e depois `FINAL` antes da tela de resultado.

---

## Task 15: Null checks no loop de jogo

**Melhoria #14**

**Files:**
- Modify: `C:\ws\Odds\index.html` (função `startLiveGame`, JS)

- [ ] **Step 1: Adicionar null checks nos `getElementById` do loop**

Localizar dentro do `setInterval` de `startLiveGame()`:

```js
document.getElementById('live-clock').textContent = state.period === 'FINAL' ? `90'` : minuteDisplay;
document.getElementById('live-quarter').textContent = state.period;

// Game progress bar
const progress = Math.min(100, (state.liveSecond / totalTicks) * 100);
document.getElementById('game-progress-bar').style.width = progress + '%';
```

Substituir por:

```js
const clockEl = document.getElementById('live-clock');
const quarterEl = document.getElementById('live-quarter');
const progressEl = document.getElementById('game-progress-bar');

if (clockEl) clockEl.textContent = state.period === 'FINAL' ? `90'` : minuteDisplay;
if (quarterEl) quarterEl.textContent = state.period;

const progress = Math.min(100, (state.liveSecond / totalTicks) * 100);
if (progressEl) progressEl.style.width = progress + '%';
```

- [ ] **Step 2: Verificar que o jogo ainda funciona normalmente**

Jogar uma partida completa e confirmar que relógio, período e barra de progresso atualizam corretamente.

---

## Task 16: AI scoring — rebalancear pontuação

**Melhoria #5**

**Files:**
- Modify: `C:\ws\Odds\index.html` (função `startLiveGame`, JS)

- [ ] **Step 1: Reduzir e escalar o score de IA por tick**

Localizar:

```js
// AI player score bumps
for (let i = 1; i < 4; i++) {
  if (Math.random() > 0.5) {
    state.playerScores[i] += Math.floor(Math.random() * 40) + 5;
  }
}
```

Substituir por:

```js
// AI player score bumps — escalonado por personalidade
const aiPersonality = [
  { chance: 0.35, min: 5,  max: 25 },  // Galo_Fan: agressivo mas inconsistente
  { chance: 0.55, min: 3,  max: 15 },  // CruzeiroBH: conservador, ganhos menores mas frequentes
  { chance: 0.25, min: 0,  max: 60 },  // FlaFlu_RJ: longshot, ou nada ou muito
];
for (let i = 1; i < 4; i++) {
  const p = aiPersonality[i - 1];
  if (Math.random() < p.chance) {
    state.playerScores[i] += Math.floor(Math.random() * (p.max - p.min)) + p.min;
  }
}
```

Médias por tick com `totalTicks = 56`:
- Galo_Fan: `0.35 * 15 = 5.25/tick` × 56 = ~294 total
- CruzeiroBH: `0.55 * 9 = 4.95/tick` × 56 = ~277 total
- FlaFlu_RJ: `0.25 * 30 = 7.5/tick` × 56 = ~420 total (mas alta variância)

Jogador humano com salary cap completo gasto e 60% de acerto: ~$450–$600 total. Competição realista.

- [ ] **Step 2: Verificar no browser**

Jogar 3 partidas e confirmar que o placar final é competitivo — o jogador humano pode vencer, mas não é garantido.

---

## Task 17: AI personalidades — estilo no leaderboard

**Melhoria #17 — visual**

**Files:**
- Modify: `C:\ws\Odds\index.html` (função `buildLeaderboard` e `updateLeaderboardSmooth`, JS)

- [ ] **Step 1: Adicionar tag de personalidade no leaderboard**

As personalidades já existem no `PLAYERS` array mas não são exibidas. Adicionar um campo `style` ao array `PLAYERS`:

```js
const PLAYERS = [
  { name: 'Você', tag: 'Host', color: '#1A6B3C', initial: 'V', style: '' },
  { name: 'Galo_Fan', tag: 'Pronto', color: '#0038A8', initial: 'G', style: 'Agressivo' },
  { name: 'CruzeiroBH', tag: 'Pronto', color: '#CC1014', initial: 'C', style: 'Conservador' },
  { name: 'FlaFlu_RJ', tag: 'Pronto', color: '#6B2D8B', initial: 'F', style: 'Longshot' },
];
```

- [ ] **Step 2: Exibir o estilo no leaderboard durante o jogo**

Localizar o template do `lb-row` em `buildLeaderboard()`:

```js
html += `<div class="lb-row" data-player-idx="${p.idx}" style="order:${rank}">
  <span class="lb-rank${rank === 0 ? ' lb-rank-1' : ''}">${rank + 1}</span>
  <div class="lb-player">
    <div class="lb-player-avatar" style="background:${p.color}">${p.initial}</div>
    <span class="lb-player-name${p.idx === 0 ? ' you' : ''}">${p.name}</span>
  </div>
  <span class="lb-score-val">${p.score}</span>
</div>`;
```

Substituir por:

```js
html += `<div class="lb-row" data-player-idx="${p.idx}" style="order:${rank}">
  <span class="lb-rank${rank === 0 ? ' lb-rank-1' : ''}">${rank + 1}</span>
  <div class="lb-player">
    <div class="lb-player-avatar" style="background:${p.color}">${p.initial}</div>
    <div>
      <span class="lb-player-name${p.idx === 0 ? ' you' : ''}">${p.name}</span>
      ${p.style ? `<span class="lb-player-style">${p.style}</span>` : ''}
    </div>
  </div>
  <span class="lb-score-val">${p.score}</span>
</div>`;
```

- [ ] **Step 3: Adicionar CSS para `.lb-player-style`**

Após `.lb-player-name` no CSS, adicionar:

```css
.lb-player-style {
  display: block;
  font-size: 10px;
  color: var(--text-faint);
  font-weight: 500;
  letter-spacing: 0.04em;
  line-height: 1;
}
```

- [ ] **Step 4: Verificar no browser**

No leaderboard durante o jogo, cada IA deve mostrar sua tag de estilo (Agressivo / Conservador / Longshot) abaixo do nome.

---

## Task 18: Game story — narrativa mais rica

**Melhoria #16**

**Files:**
- Modify: `C:\ws\Odds\index.html` (função `showResolution`, JS)

- [ ] **Step 1: Substituir a geração do game story por versão com mais variação**

Localizar em `showResolution()`:

```js
// Game story
const hits = state.selectedPicks.filter(id => state.betStatuses[id] === 'hit');
const bigHit = hits.map(id => MARKETS.find(m => m.id === id)).sort((a, b) => b.payout - a.payout)[0];

let story = `Clássico Mineiro encerrado: CAM ${state.gameScore.home} × ${state.gameScore.away} CRU. `;
if (hits.length > 0 && bigHit) {
  story += `Sua maior aposta foi "${bigHit.prop}" a ${bigHit.payout}x, rendendo $${Math.round(bigHit.payout * bigHit.cost)}. `;
}
story += `Você acertou ${hits.length} de ${state.selectedPicks.length} apostas. `;
if (sorted[0].name === 'Você') {
  story += `Performance dominante — você leu o jogo melhor que qualquer um na sala.`;
} else {
  story += `${sorted[0].name} assumiu a liderança nos minutos finais com escolhas decisivas.`;
}
document.getElementById('game-story-text').textContent = story;
```

Substituir por:

```js
// Game story — narrativa rica
const hits = state.selectedPicks.filter(id => state.betStatuses[id] === 'hit');
const misses = state.selectedPicks.filter(id => state.betStatuses[id] === 'miss');
const bigHit = hits.map(id => MARKETS.find(m => m.id === id)).sort((a, b) => b.payout - a.payout)[0];
const userScore = state.playerScores[0];
const totalGoals = state.gameScore.away + state.gameScore.home;

const scoreLine = `CAM ${state.gameScore.home} × ${state.gameScore.away} CRU`;

const matchIntros = [
  `Clássico Mineiro encerrado em ${scoreLine}.`,
  `O apito final soou: ${scoreLine} no Mineirão.`,
  `Fim de jogo no Clássico — ${scoreLine}.`,
];
let story = matchIntros[Math.floor(Math.random() * matchIntros.length)] + ' ';

if (totalGoals === 0) {
  story += 'Jogo de muita marcação, sem gols. ';
} else if (totalGoals >= 4) {
  story += `Uma partida de gols — ${totalGoals} no total. `;
}

if (hits.length === 0) {
  story += 'Nenhuma das suas apostas se concretizou — o futebol é implacável. ';
} else if (hits.length === state.selectedPicks.length) {
  story += `Aproveitamento perfeito: ${hits.length}/${state.selectedPicks.length} apostas certas. `;
} else {
  story += `Você acertou ${hits.length} de ${state.selectedPicks.length} apostas. `;
}

if (bigHit) {
  const earned = Math.round(bigHit.payout * bigHit.cost);
  story += `Destaque para "${bigHit.prop}" a ${bigHit.payout}x — $${earned} de retorno. `;
}

if (sorted[0].name === 'Você') {
  const margin = userScore - state.playerScores[1];
  if (margin > 200) {
    story += `Vitória dominante com ${userScore} pontos — os rivais não chegaram perto.`;
  } else {
    story += `Vitória apertada por ${margin} pontos. Você leu o jogo na hora certa.`;
  }
} else {
  story += `${sorted[0].name} assumiu a liderança com ${sorted[0].score} pontos. Próxima vez o Clássico é seu.`;
}
document.getElementById('game-story-text').textContent = story;
```

- [ ] **Step 2: Verificar no browser**

Jogar 3 partidas com resultados diferentes (vitória, derrota, perfeito) e confirmar que o texto varia e é narrativamente interessante.

---

## Task 19: Browser back button — history API

**Melhoria #12**

**Files:**
- Modify: `C:\ws\Odds\index.html` (função `showScreen` e seção `INIT`, JS)

- [ ] **Step 1: Adicionar `pushState` na navegação**

Localizar a função `showScreen`:

```js
function showScreen(name) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  const el = document.getElementById('screen-' + name);
  if (el) el.classList.add('active');
  state.screen = name;
}
```

Substituir por:

```js
function showScreen(name, pushHistory = true) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  const el = document.getElementById('screen-' + name);
  if (el) el.classList.add('active');
  state.screen = name;
  if (pushHistory) {
    history.pushState({ screen: name }, '', '#' + name);
  }
}
```

- [ ] **Step 2: Registrar listener do `popstate`**

No final do script, após `animateStats()`, adicionar:

```js
window.addEventListener('popstate', e => {
  const screen = e.state?.screen;
  if (screen && ['landing', 'lobby', 'draft'].includes(screen)) {
    // Só permite navegar para telas sem estado de jogo ativo
    if (state.gameInterval) {
      clearInterval(state.gameInterval);
      state.gameInterval = null;
    }
    showScreen(screen, false);
  }
});
// Estado inicial para a landing
history.replaceState({ screen: 'landing' }, '', '#landing');
```

- [ ] **Step 3: Verificar no browser**

Navegar: landing → lobby → draft. Pressionar o botão voltar do browser — deve retornar ao lobby, depois à landing, sem travar ou jogar o usuário para fora da aplicação.

---

## Ordem de implementação

Implementar na sequência das tasks — cada task é independente, exceto:
- Task 9 (count-up) depende dos IDs adicionados na Task 8 (reordenação)
- Task 14 (FINAL timing) e Task 16 (AI scoring) devem ser feitas antes de verificação final de gameplay

## Self-Review

**Spec coverage:**
- ✅ #1 Ticker cores → Task 3
- ✅ #2 Featured CSS → Task 6
- ✅ #3 FINAL timing → Task 14
- ✅ #4 Disabled button → Task 10
- ✅ #5 AI balance → Task 16
- ✅ #6 Favicon/OG → Task 1
- ✅ #7 Count-up → Task 9
- ✅ #8 Stats order → Task 8
- ✅ #9 Mute button → Task 7
- ✅ #10 Sala # → Task 11
- ✅ #11 COR badge → Task 5
- ✅ #12 Back button → Task 19
- ✅ #13 Fonts → Task 2
- ✅ #14 Null checks → Task 15
- ✅ #15 Confetti branco → Task 4
- ✅ #16 Game story → Task 18
- ✅ #17 AI personalidades → Tasks 16 + 17
- ✅ #18 Lobby animação → Task 12
- ✅ #19 Nomes goleadores → Task 13

**Placeholder scan:** Nenhum TBD/TODO no plano.

**Type consistency:** Todos os IDs, nomes de funções e variáveis são consistentes entre tasks.
