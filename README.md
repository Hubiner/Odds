# Odds Arena · Futebol Brasileiro

Jogo de previsão em tempo real focado no futebol brasileiro. Escolha suas props, monte seu draft e acompanhe o Clássico Mineiro (Cruzeiro × Atlético Mineiro) ao vivo enquanto disputa pontos contra outros "torcedores-apostadores" simulados por IA.

Projeto de portfólio pessoal — hospedado na Vercel, zero dependências, zero backend.

---

## Demo

> Adicione aqui o link após o deploy na Vercel.

---

## Sobre o projeto

### O que é

Odds Arena é uma simulação client-side de um jogo de previsão esportiva. O usuário monta um "draft" de apostas (props) com um salary cap de $500, confirma seus picks e assiste à partida ser simulada em tempo real — gols, resoluções de props e leaderboard animado incluídos.

### Times participantes

| Abreviação | Nome | Estado |
|---|---|---|
| CAM | Atlético Mineiro | MG |
| CRU | Cruzeiro | MG |
| COR | Corinthians | SP |
| PAL | Palmeiras | SP |
| SAO | São Paulo | SP |
| FLA | Flamengo | RJ |
| FLU | Fluminense | RJ |
| BOT | Botafogo | RJ |

### Partidas simultâneas

| Jogo | Tipo |
|---|---|
| CRU × CAM | Clássico Mineiro ⭐ destaque |
| FLA × PAL | Nacional |
| COR × SAO | Derby Paulista |
| FLU × BOT | Clássico Carioca |

### Mecânica do jogo

1. **Lobby** — 4 jogadores (você + 3 IAs) entram na sala
2. **Draft** — escolha até 5 props dentro do salary cap de $500
3. **Jogo ao vivo** — partida simulada em minutos crescentes (1'→90'+), com gols, eventos e leaderboard em tempo real
4. **Resultado** — ranking final com confetti para o vencedor

### Props disponíveis (12 mercados)

| Prop | Odds | Custo |
|---|---|---|
| Atlético vence | -125 | $80 |
| Cruzeiro vence | +130 | $70 |
| Empate | +240 | $45 |
| Hulk marca 1+ | +150 | $68 |
| Matheus Pereira dá assistência | +175 | $62 |
| Kaio Jorge marca 1+ | +210 | $52 |
| Mais de 2.5 gols | -110 | $90 |
| Menos de 2.5 gols | -118 | $84 |
| Atlético vence por 2+ | +340 | $32 |
| Hulk marca de falta 🎯 | +680 | $22 |
| Nenhum gol no 1º tempo 🎯 | +520 | $27 |
| Hat-trick na partida 🎯 | +1200 | $15 |

🎯 = longshot

---

## Design

- **Tema:** Light editorial, clean — fundo off-white `#F8F8F6`
- **Acento:** Verde futebol `#1A6B3C`
- **Tipografia:**
  - Syne 700–800 — títulos e display
  - Inter 400–600 — corpo e labels
  - JetBrains Mono 400–800 — odds, placares, dados numéricos
- **Animações:** FLIP leaderboard, confetti canvas, feed ao vivo
- **Áudio:** Web Audio API procedural (sem arquivos externos)

---

## Stack técnica

| Item | Detalhe |
|---|---|
| Estrutura | Arquivo HTML único (`index.html`) |
| Dependências | Nenhuma — 100% vanilla JS |
| Fontes | Google Fonts (CDN) |
| Áudio | Web Audio API |
| Animações | CSS transitions + canvas + FLIP |
| Backend | Nenhum — simulação client-side |
| Deploy | Vercel — zero configuração |

---

## Rodar localmente

O projeto é um único arquivo HTML estático. Três formas de abrir:

### Opção 1 — Abrir direto no navegador (mais simples)

```bash
# Clone ou baixe o repositório
git clone https://github.com/seu-usuario/odds-arena.git
cd odds-arena

# Abra o arquivo no navegador
# Windows
start index.html

# macOS
open index.html

# Linux
xdg-open index.html
```

> ⚠️ Algumas funcionalidades (Web Audio API) podem ser bloqueadas pelo navegador em `file://`. Se o som não funcionar, use um servidor local abaixo.

### Opção 2 — Servidor local com Python (recomendado)

```bash
# Python 3
python -m http.server 8080

# Python 2 (legado)
python -m SimpleHTTPServer 8080
```

Acesse: [http://localhost:8080](http://localhost:8080)

### Opção 3 — Servidor local com Node.js

```bash
# Com npx (sem instalar nada)
npx serve .

# Ou com http-server
npm install -g http-server
http-server -p 8080
```

Acesse: [http://localhost:8080](http://localhost:8080)

### Opção 4 — VS Code Live Server

1. Instale a extensão [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
2. Abra a pasta do projeto no VS Code
3. Clique em **Go Live** na barra de status inferior
4. O navegador abre automaticamente com hot-reload

---

## Deploy na Vercel

### Via drag-and-drop (sem conta GitHub)

1. Acesse [vercel.com](https://vercel.com) e faça login
2. Na dashboard, clique em **Add New → Project**
3. Arraste a pasta do projeto (ou só o `index.html`) para a área indicada
4. Clique em **Deploy**

### Via GitHub (recomendado para portfólio)

```bash
# Inicialize o repositório
git init
git add index.html README.md
git commit -m "feat: odds arena futebol brasileiro"

# Suba para o GitHub
git remote add origin https://github.com/seu-usuario/odds-arena.git
git push -u origin main
```

Depois no Vercel:
1. **Add New → Project → Import Git Repository**
2. Selecione o repositório
3. Clique em **Deploy** — nenhuma configuração necessária

A Vercel detecta automaticamente que é um site estático.

---

## Estrutura do projeto

```
odds-arena/
├── index.html          # Aplicação completa (HTML + CSS + JS)
├── README.md           # Este arquivo
└── docs/
    └── superpowers/
        ├── specs/      # Design spec aprovado
        └── plans/      # Plano de implementação
```

---

## Notas

- Todos os dados são **fictícios e hardcoded** — sem API real
- O multiplayer é **simulado por IA** — não há conexão entre navegadores
- Não há persistência entre sessões
- Projeto de portfólio pessoal — não representa um serviço de apostas real

---

*Simulação · Dados fictícios · Projeto de portfólio*
