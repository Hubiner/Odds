# Design Spec — Odds Arena: Futebol Brasileiro
**Data:** 2026-05-04  
**Status:** Aprovado pelo usuário  
**Destino:** Portfolio pessoal, hospedado na Vercel  

---

## Visão Geral

Reformulação completa do jogo de previsão "Odds Arena" (originalmente NBA) para o **futebol brasileiro**, focando em times dos estados de MG, SP e RJ. Visual redesenhado com **light theme editorial e clean**, produção-grade para portfolio.

A aplicação permanece um **único arquivo HTML** (sem backend, sem build step), compatível com deploy direto na Vercel via drag-and-drop ou GitHub.

---

## Abordagem Escolhida

**B — Redesign com identidade:**  
Substituição completa dos dados (times, jogadores, props) + redesign visual full (light theme, nova tipografia, nova paleta, nova hierarquia). A mecânica do jogo é preservada; o que muda é tudo que o usuário vê e sente.

---

## Design System

### Tema
- Light, editorial, clean
- Fundo: off-white quente (`#F8F8F6`), não branco puro

### Tipografia
| Papel | Fonte | Uso |
|---|---|---|
| Display / Títulos | **Syne** (Bold 700–800) | Nome do jogo, headings principais |
| Corpo / Labels | **Inter** (400–600) | Textos, labels, descrições |
| Numérico / Dados | **JetBrains Mono** (400–700) | Odds, placar, valores $ |

### Paleta de Cores
| Token CSS | Valor | Uso |
|---|---|---|
| `--bg` | `#F8F8F6` | Fundo da página |
| `--surface` | `#FFFFFF` | Cards, painéis |
| `--surface-2` | `#F2F2EF` | Fundo de tabelas, hover |
| `--border` | `#E8E8E4` | Bordas, divisores |
| `--text-primary` | `#111110` | Conteúdo principal |
| `--text-muted` | `#6B6B63` | Labels, secundário |
| `--accent` | `#1A6B3C` | Verde futebol — CTAs, destaques |
| `--accent-hover` | `#155730` | Estado hover do accent |
| `--hit` | `#16A34A` | Prop acertada (HIT) |
| `--miss` | `#DC2626` | Prop errada (MISS) |
| `--warning` | `#D97706` | Alertas, odds altas |

### Cores por Estado (badges dos times)
| Estado | Cor | Hex |
|---|---|---|
| MG | Azul mineiro | `#007BC2` |
| SP | Vermelho paulista | `#CC1014` |
| RJ | Preto carioca | `#1A1A1A` |

### Componentes Base
- `border-radius`: 12px (cards), 8px (botões), 6px (badges)
- `box-shadow`: `0 1px 3px rgba(0,0,0,0.08)` (cards), `0 4px 16px rgba(0,0,0,0.12)` (modais)
- Espaçamento: grid de 8px
- Transições: `200ms ease` padrão

---

## Dados — Times

8 times participantes dos 4 jogos, todos de MG, SP e RJ:

| Abreviação | Nome Completo | Estado | Cor Primária | Cor Secundária |
|---|---|---|---|---|
| CAM | Atlético Mineiro | MG | `#000000` | `#FFFFFF` |
| CRU | Cruzeiro | MG | `#0038A8` | `#FFFFFF` |
| COR | Corinthians | SP | `#000000` | `#FFFFFF` |
| PAL | Palmeiras | SP | `#006437` | `#FFFFFF` |
| SAO | São Paulo | SP | `#CC1014` | `#000000` |
| FLA | Flamengo | RJ | `#CC1014` | `#000000` |
| FLU | Fluminense | RJ | `#6B2D8B` | `#C8102E` |
| BOT | Botafogo | RJ | `#1A1A1A` | `#FFFFFF` |

> MG: 2 times · SP: 3 times · RJ: 3 times. Todos os 8 aparecem nos 4 jogos simultâneos.

---

## Dados — Jogos Simultâneos (4 partidas)

| # | Mandante | Visitante | Tipo |
|---|---|---|---|
| **Destaque** | CRU | CAM | Clássico Mineiro |
| 2 | FLA | PAL | Nacional |
| 3 | COR | SAO | Derby Paulista |
| 4 | FLU | BOT | Clássico Carioca |

---

## Dados — Props (Draft Board)

Baseadas no jogo em destaque CRU × CAM:

| ID | Descrição | Tipo | Odds | Custo | Longshot |
|---|---|---|---|---|---|
| p1 | Atlético vence | Resultado | -125 | $80 | false |
| p2 | Cruzeiro vence | Resultado | +130 | $70 | false |
| p3 | Empate | Resultado | +240 | $45 | false |
| p4 | Hulk marca 1+ | Jogador | +150 | $68 | false |
| p5 | Matheus Pereira dá assistência | Jogador | +175 | $62 | false |
| p6 | Kaio Jorge marca 1+ | Jogador | +210 | $52 | false |
| p7 | Mais de 2.5 gols | Total | -110 | $90 | false |
| p8 | Menos de 2.5 gols | Total | -118 | $84 | false |
| p9 | Atlético vence por 2+ | Resultado | +340 | $32 | false |
| p10 | Hulk marca de falta | Jogador | +680 | $22 | true |
| p11 | Nenhum gol no 1º tempo | Total | +520 | $27 | true |
| p12 | Hat-trick na partida | Especial | +1200 | $15 | true |

**Salary cap:** $500 por jogador, máximo 5 props por draft.

---

## Dados — Jogadores IA

| Nome | Cor | Personalidade |
|---|---|---|
| Você (Host) | `#1A6B3C` (verde accent) | — |
| Galo_Fan | `#0038A8` (azul CRU) | Apostador agressivo |
| CruzeiroBH | `#CC1014` (vermelho SP) | Conservador |
| FlaFlu_RJ | `#6B2D8B` (roxo FLU) | Longshot hunter |

---

## Adaptações de Mecânica

| Basquete (original) | Futebol (novo) |
|---|---|
| 4 quarters | 1º Tempo / 2º Tempo / Acréscimos |
| Placar `87 - 82` | Placar `2 × 1` |
| Timer decrescente por quarter | Minuto crescente (1' → 90'+) |
| "Q3 4:22" | "47'" |
| "Buzzer" no final | Apito final |
| Crowd roar | Sons de torcida adaptados |

---

## Estrutura das Telas

### Fase 1 — Landing Page
- "ODDS ARENA" em Syne 800, grande
- Subtítulo: "Previsão em tempo real · Futebol Brasileiro"
- Badge: `MG · SP · RJ`
- Botão único: "CRIAR LOBBY" (verde accent)
- Fundo off-white, sem imagens, tipografia como elemento visual

### Fase 2 — Lobby
- 4 slots de jogadores (avatar inicial + nome)
- Status: "Aguardando jogadores..."
- Botão "ENTRAR NO DRAFT" ativa quando todos prontos
- Layout centralizado, card branco com borda sutil

### Fase 3 — Draft Board
- **Coluna esquerda:** tabela de props (descrição, odds, custo, botão selecionar)
- **Coluna central:** "Minhas apostas" + saldo do salary cap
- **Coluna direita:** leaderboard dos outros jogadores
- Header fixo: jogo em destaque (CRU × CAM), minuto atual, placar
- Botão "CONFIRMAR PICKS" ativa com ≥ 1 prop selecionada

### Fase 4 — Jogo ao Vivo
- Ticker horizontal (topo): 4 jogos ao vivo com placar + minuto
- Painel principal: placar CRU × CAM + timer simulado (minutos)
- Painel lateral esquerdo: "Minhas apostas" com status HIT/MISS
- Painel lateral direito: leaderboard com animação FLIP
- Live feed (base): eventos do jogo + resoluções de props
  - Exemplo: "⚽ Hulk marca! — CAM 1×0 CRU · 34'"
  - Exemplo: "✅ Hulk marca 1+ — HIT · +$102"

### Fase 5 — Tela Final
- Vencedor com confetti (canvas)
- Ranking completo dos 4 jogadores
- Botão "JOGAR NOVAMENTE"
- Layout centralizado, clean

---

## Texto & Idioma

- Interface principal: **Português do Brasil**
- Termos mantidos em inglês/inglês-BR: "odds", "longshot", "salary cap", "HIT", "MISS", "draft"
- Labels técnicos de apostas mantidos como no mercado ("+130", "-110", etc.)

---

## Tecnologias

| Item | Detalhe |
|---|---|
| Estrutura | Arquivo HTML único (`Odds Arena.html`) |
| Fonts | Google Fonts: Syne, Inter, JetBrains Mono |
| Áudio | Web Audio API (procedural, sem arquivos externos) |
| Animações | CSS transitions + canvas (confetti) + FLIP leaderboard |
| Deploy | Vercel (drag-and-drop ou GitHub) — zero configuração |
| Backend | Nenhum — 100% client-side simulation |

---

## O que NÃO muda

- Mecânica central do jogo (salary cap, draft, live resolution)
- Animações FLIP do leaderboard
- Confetti canvas
- Geração procedural de sons
- Lógica de simulação de jogo

---

## Fora do Escopo

- Dados reais de API (tudo é simulação hardcoded)
- Multiplayer real (simulado com IA)
- Persistência de dados entre sessões
- Autenticação
