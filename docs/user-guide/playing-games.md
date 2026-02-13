# Jogar Partidas Online

Aprenda a jogar xadrez online contra outros jogadores no OitoPorOito.

## Encontrando uma Partida

### Partida Rápida

O jeito mais rápido de começar a jogar:

1. Clique em **"Jogar"** no menu principal
2. Selecione o tempo de jogo:
   - **Bullet** (1+0): Partidas ultra-rápidas
   - **Blitz** (3+0, 5+0): Partidas rápidas
   - **Rápido** (10+0, 15+10): Mais tempo para pensar
   - **Clássico** (30+0): Partidas longas
3. Clique em **"Buscar Oponente"**
4. Aguarde ser pareado (geralmente < 30 segundos)

### Filtros de Matchmaking

Opções avançadas para encontrar oponentes:

```
Jogar > Configurações Avançadas
```

- **Faixa de Rating**: ±100, ±200, Qualquer
- **Cor**: Brancas, Pretas, Aleatório
- **Rating Provisório**: Aceitar ou não iniciantesabsolutos
- **Região**: Mesma região, Qualquer (menor ping)

### Desafiar um Amigo

Desafie alguém específico:

1. Vá para **Amigos** ou **Clubes**
2. Clique no nome do jogador
3. Selecione **"Desafiar"**
4. Escolha o tempo e outras opções
5. Aguarde a aceitação

## Durante a Partida

### Interface do Jogo

```
┌─────────────────────────────────────────┐
│ ⚪ Oponente (1523)        ⏱️ 5:00      │
├─────────────────────────────────────────┤
│                                         │
│          [Tabuleiro 8x8]                │
│                                         │
├─────────────────────────────────────────┤
│ ⚫ Você (1487)            ⏱️ 5:00      │
│                                         │
│ [Oferecer Empate] [Resignar]           │
└─────────────────────────────────────────┘
```

### Fazendo Movimentos

**Mouse:**
1. Clique na peça que deseja mover
2. Clique no destino
3. Ou arraste a peça (drag & drop)

**Teclado (avançado):**
- Digite movimentos em notação algébrica: `e2e4`
- Pressione Enter

### Controles

| Ação | Como Fazer |
|------|------------|
| **Mover** | Clique ou arraste |
| **Promover Peão** | Escolha na caixa que aparece |
| **Oferecer Empate** | Botão "Empate" |
| **Resignar** | Botão "Resignar" |
| **Flip Tabuleiro** | Tecla `F` ou botão 🔄 |
| **Chat** | Ícone 💬 |

### Promoção de Peão

Quando seu peão chega na última fila:

```
┌─────────────────────┐
│  Promover para:     │
│  ♛ Rainha           │
│  ♜ Torre            │
│  ♝ Bispo            │
│  ♞ Cavalo           │
└─────────────────────┘
```

Escolha rapidamente, o relógio continua correndo!

### Relógio de Xadrez

#### Modos de tempo

- **X+0**: X minutos, sem incremento
  - Exemplo: 5+0 = 5 minutos no total
- **X+Y**: X minutos, Y segundos de incremento
  - Exemplo: 10+5 = 10 minutos + 5 segundos por lance

#### Bandeira

Se seu tempo acabar:
- ⏱️ **0:00** = Você perde por tempo
- **Exceto**: Se o oponente não tem material para dar mate (empate)

## Resultado da Partida

### Formas de Terminar

#### Vitória
- ♔ **Xeque-mate**: Rei do oponente está em mate
- ⏱️ **Tempo**: Oponente ficou sem tempo
- 🏳️ **Resignação**: Oponente desistiu
- ❌ **Abandono**: Oponente desconectou e não voltou

#### Empate
- ⚔️ **Stalemate**: Rei não está em xeque mas não tem movimentos legais
- 🤝 **Acordo**: Ambos concordaram com empate
- 🔄 **Repetição**: Mesma posição 3 vezes
- 📏 **50 Movimentos**: 50 movimentos sem captura ou movimento de peão
- ⏱️ **Tempo Insuficiente**: Ambos sem material para dar mate

### Tela de Resultado

```
┌─────────────────────────────────────────┐
│         🏆 Vitória! 1-0                 │
│                                         │
│    Você (Brancas) derrotou              │
│    Oponente (Pretas)                    │
│    por xeque-mate                       │
│                                         │
│    Rating: 1487 → 1502 (+15)            │
│                                         │
│  [Analisar] [Revanche] [Ir para Home]  │
└─────────────────────────────────────────┘
```

## Após a Partida

### Análise

Revise sua partida com o engine Stockfish:

1. Clique em **"Analisar"**
2. Navegue pelos movimentos:
   - `←` : Movimento anterior
   - `→` : Próximo movimento
   - `Home` : Início
   - `End` : Fim
3. Veja avaliação do engine: `+0.7` (brancas um pouco melhor)
4. Encontre **erros** ❌ e **jogadas brilhantes** ⭐

### Erros Comuns

- **?** Inacurácia (perda de -0.3 a -0.7)
- **??** Erro (perda de -0.7 a -2.0)
- **???** Blunder (perda de > -2.0)

### Salvar Partida

- **Favoritar**: ⭐ para revisar depois
- **Notas**: Adicione comentários
- **Compartilhar**: Link público da partida
- **Exportar PGN**: Download em formato PGN

### Revanche

Quer jogar de novo contra o mesmo oponente?

1. Clique em **"Revanche"**
2. Cores são invertidas automaticamente
3. Aguarde a aceitação

## Etiqueta de Jogo

### ✅ Faça

- Seja respeitoso no chat
- Dê "gg" (good game) após partidas
- Aceite derrotas com elegância
- Aguarde o oponente em desconexões temporárias

### ❌ Não Faça

- Usar engines durante a partida (antiético e ilegal)
- Abandonar partidas perdidas sem resignar
- Stall (demorar propositalmente quando perdendo)
- Spam de ofertas de empate
- Insultar oponentes

### Fair Play

O OitoPorOito tem detecção automática de:
- 🤖 **Uso de engines**: Move consistency analysis
- ⏰ **Stallinglento**: Move timing patterns
- 📊 **Sandbagging**: Perder propositalmente para baixar rating

**Consequências:**
1. Aviso
2. Suspensão temporária (1-7 dias)
3. Ban permanente (casos graves)

## Ratings e Rankings

### Como Rating Funciona

Usa o sistema **Glicko-2**:

- **Vitória**: +5 a +30 pontos (depende do rating do oponente)
- **Empate**: -5 a +5 pontos
- **Derrota**: -5 a -30 pontos

### RD (Rating Deviation)

- **Novo jogador**: RD alto (±350)
- **Jogador ativo**: RD baixo (±50)
- **RD baixo = rating mais confiável**

### Leaderboards

Veja rankings em:

```
Rankings > Leaderboards
```

- Global (todos os jogadores)
- Por país
- Por time control (Bullet, Blitz, Rápido)
- Mensal/Semanal/Histórico

## Histórico de Partidas

Acesse todas suas partidas em:

```
Perfil > Partidas
```

Filtros disponíveis:
- Por resultado (vitórias, derrotas, empates)
- Por cor (brancas, pretas)
- Por time control
- Por oponente
- Por data

## Estatísticas

Veja suas estatísticas detalhadas:

```
Perfil > Estatísticas
```

- **Total de partidas**: 152
- **Vitórias/Derrotas/Empates**: 87 / 52 / 13
- **Win Rate**: 57.2%
- **Abertura mais jogada**: Italiana (C50)
- **Taxa de precisão média**: 78.5%
- **Longest winning streak**: 7 partidas

## Modos Especiais

### Arena de Torneio

Partidas simultâneas em formato de arena:
- Tempo limitado (ex: 1 hora)
- Jogue quantas partidas conseguir
- Pontos por vitória: 2, empate: 1
- Ranking ao vivo

### Simulação (Simul)

Jogue contra um mestre simultaneamente:
- Um jogador forte vs múltiplos oponentes
- Revezamento de movimentos
- Experiência educacional

### Partidas Classificadas vs Casual

- **Classificadas** (Ranked): Afetam seu rating
- **Casual**: Apenas por diversão, sem afetar rating

## Dicas para Melhorar

1. **📊 Analise suas partidas**: Aprenda com erros
2. **🧩 Resolva puzzles**: Melhore cálculo tático
3. **📚 Estude aberturas**: Conheça 5-10 lances de cada
4. **⏱️ Gerencie o tempo**: Não gaste tudo no início
5. **🎯 Jogue regularmente**: Consistência é chave

## Problemas Comuns

### Lag / Desconexão

- Verifique sua conexão de internet
- OitoPorOito adiciona tempo extra em desconexões (até 30s)
- Use ethernet em vez de WiFi para menor latency

### Oponente Travou

Se o oponente parar de se mover:
- Aguarde 30 segundos
- Sistema detecta abandono automaticamente
- Vitória é creditada a você

### Não Encontro Oponentes

- Baixo número de jogadores no horário
- Tente expandir a faixa de rating
- Jogue em modo casual
- Participe de torneios agendados

## FAQ

**P: Posso jogar sem conta?**  
R: Não, é necessário criar uma conta gratuita.

**P: Como jogo contra específico rating?**  
R: Use filtros avançados de matchmaking.

**P: O que é "rating provisório"?**  
R: Primeiras 20 partidas têm rating com `?` até estabilizar.

**P: Posso usar opening book?**  
R: Não, é considerado trapaça. Deve jogar de memória.

## Próximos Passos

- 🤖 **[Jogar vs Computador](play-computer.md)**: Pratique sem pressão
- 🧩 **[Resolver Puzzles](solving-puzzles.md)**: Melhore táticas
- 👥 **[Recursos Sociais](social-features.md)**: Conecte-se com jogadores

---

**Boa sorte em suas partidas! ♟️**
