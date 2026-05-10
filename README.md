# Odds Arena · Futebol Brasileiro

Jogo de previsão em tempo real focado no futebol brasileiro. Escolha suas props, monte seu draft e acompanhe o Clássico Mineiro (Cruzeiro × Atlético Mineiro) ao vivo enquanto disputa pontos contra outros "torcedores-apostadores" simulados por IA.

---

## Demo

> https://odds-one.vercel.app/#landing

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

## Notas

- Todos os dados são **fictícios e hardcoded** — sem API real
- O multiplayer é **simulado por IA** — não há conexão entre navegadores
- Não há persistência entre sessões
- Projeto não representa um serviço de apostas real

---

*Simulação · Dados fictícios*
