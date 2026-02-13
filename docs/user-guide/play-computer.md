# Jogar contra o Computador

Pratique xadrez jogando contra o motor Stockfish, um dos engines mais fortes do mundo.

## Começando

1. Clique em **"Jogar"** no menu
2. Selecione **"Jogar vs Computador"**
3. Escolha nível de dificuldade (1-8)
4. Selecione sua cor (Brancas/Pretas/Aleatório)
5. Clique em **"Iniciar Partida"**

## Níveis de Dificuldade

O OitoPorOito oferece 8 níveis de Stockfish:

| Nível | Rating | Público-Alvo | Depth |
|-------|--------|--------------|-------|
| 1 🌱 | 800 | Iniciantes absolutos | 1-2 |
| 2 🌿 | 1000 | Aprendendo regras | 3-4 |
| 3 🌳 | 1200 | Casual | 5-6 |
| 4 🎯 | 1400 | Intermediário | 7-8 |
| 5 🔥 | 1600 | Avançado | 10-12 |
| 6 💪 | 1800 | Expert | 14-16 |
| 7 🏆 | 2000 | Mestre | 18-20 |
| 8 👑 | 2400+ | Grande Mestre | 22+ |

## Configurações do Jogo

### Tempo de Jogo

Escolha quanto tempo você quer para pensar:

- **Sem Limite**: Pense o quanto quiser
- **5 minutos**: Partida rápida
- **10 minutos**: Moderado
- **15 minutos**: Mais tempo
- **30 minutos**: Clássico

### Cor

- **Brancas**: Você começa
- **Pretas**: Computador começa
- **Aleatório**: Sorteio 50/50

### Hints (Dicas)

Ative para receber ajuda:
- 💡 Movimentos sugeridos
- ⚠️ Avisos de movimentos suspeitos
- 🎯 Melhor lance disponível (máx 3 por partida)

## Durante a Partida

### Computador Pensando...

Enquanto o Stockfish calcula:

```
🤖 Computador pensando...
Profundidade: 18/22
Avaliação: +0.4
Melhor linha: Nf3 d5 c4 e6 g3 Nf6
```

- **Profundidade**: Quantos lances à frente está analisando
- **Avaliação**: Vantagem em "pawns" (peões)
  - `+1.0` = Brancas têm vantagem de 1 peão
  - `-2.5` = Pretas estão ganhando 2.5 peões
- **Melhor linha**: Sequência que o engine considera ótima

### Usar Hints

Se estiver travado:

1. Clique em **"Pedir Dica"** 💡
2. Uma seta verde mostrará o melhor movimento
3. Você ainda pode escolher outro movimento
4. Máximo 3 dicas por partida (para aprendizado)

### Desfazer Movimento

Cometeu um erro?

1. Clique em **"Desfazer"** ↶
2. O computador também desfará seu lance
3. Tente novamente
4. ⚠️ Não abuse! Use para aprendizado, não para "trapacear"

### Análise em Tempo Real

Ative para ver a avaliação enquanto joga:

```
Sua posição:  +0.7 ⚪ (Brancas ligeiramente melhor)
              -1.2 ⚫ (Pretas melhores)
              =0.0 ⚖️ (Igualado)
```

## Tipos de Posições Iniciais

Além da posição padrão, pratique situações específicas:

### Aberturas Comuns

- **Italiana (e4 e5 Nf3 Nc6 Bc4)**
- **Espanhola (e4 e5 Nf3 Nc6 Bb5)**
- **Siciliana (e4 c5)**
- **Francesa (e4 e6)**
- **Caro-Kann (e4 c6)**

### Finais de Partida

- **Rei + Peão vs Rei**
- **Rei + Torre vs Rei**
- **Rei + Rainha vs Rei**
- **Torres e Peões**
- **Lucena Position**
- **Philidor Position**

### Posições Táticas

- **Forques de Cavalo**
- **Pregaduras (Pins)**
- **Espetos (Skewers)**
- **Raio-X (X-rays)**
- **Descobertas**

## Modos de Jogo

### Modo Prática

Jogue livremente sem pressão:
- Sem rating afetado
- Desfazer ilimitado
- Dicas ilimitadas
- Análise em tempo real

### Modo Desafio

Teste suas habilidades:
- Sem desfazer
- Dicas limitadas
- Ganhe rating vs computador
- Compare com outros jogadores

### Modo Exercício

Resolva posições específicas:
- Posição configurada
- Objetivo: "Encontre o mate em 3"
- Stockfish verifica se você achou
- Mostra solução se desistir

## Análise Pós-Partida

Após o jogo:

1. **Gráfico de Avaliação**: Veja como a posição mudou
2. **Erros Destacados**: Movimentos ruins marcados
3. **Movimentos do Engine**: Veja o que deveria ter jogado
4. **Abertura Jogada**: Qual abertura você usou

```
┌─────────────────────────────────────────┐
│     Análise da Partida                  │
├─────────────────────────────────────────┤
│                                         │
│  Movimento 8: d4?? Blunder             │
│  Melhor: Nf3                           │
│  Perda: -2.3                           │
│                                         │
│  [Ver Posição] [Continuar Análise]     │
└─────────────────────────────────────────┘
```

## Aprenda com o Stockfish

### Use como Treinador

1. Jogue movimentos questionáveis propositalmente
2. Veja como o computador pune
3. Aprenda por que o movimento foi ruim
4. Tente de novo com a correção

### Teste Aberturas

1. Configure a abertura que quer estudar
2. Jogue contra Stockfish
3. Veja onde sua preparação falha
4. Ajuste e tente novamente

### Pratique Finais

1. Selecione uma posição de final
2. Tente vencer
3. Veja a técnica perfeita do engine
4. Repita até dominar

## Limitações

### O que o Stockfish NÃO faz

- ❌ Não comete erros óbvios (mesmo em nível 1-2, erros são calculados)
- ❌ Não tem "estilo" humano
- ❌ Não se cansa ou fica nervoso
- ❌ Não faz movimentos psicológicos

### Diferenças vs Humanos

Stockfish:
- ✅ Perfeito em cálculo tático
- ✅ Nunca erra finais técnicos
- ❌ Pode ser "não-humano" em escolhas estratégicas

Humanos:
- ❌ Cometem erros táticos
- ❌ Blunders por pressão de tempo
- ✅ Jogam psicologicamente
- ✅ Criativos em posições complexas

## Configurações Avançadas

### Personalizar Engine

```
Jogar vs Computador > Configurações Stockfish
```

- **Hash Size**: Memória usada (MB)
- **Threads**: Número de threads de CPU
- **Contempt**: "Desprezo" por empates
- **Skill Level**: Erro introduzido propositalmente

### Engine Personality (Futuro)

Planejado: diferentes "personalidades":
- 🛡️ **Defensivo**: Prefere posições sólidas
- ⚔️ **Agressivo**: Busca ataque constantemente
- 🎨 **Criativo**: Sacrifícios especulativos
- 📏 **Posicional**: Estratégia de longo prazo

## Benchmarking

Compare seu nível:

| Se você vence consistentemente | Seu nível aproximado |
|-------------------------------|----------------------|
| Nível 1-2 | 800-1000 |
| Nível 3-4 | 1000-1400 |
| Nível 5-6 | 1400-1800 |
| Nível 7 | 1800-2000 |
| Nível 8 | 2000+ (parabéns!) |

## Dicas

1. **Comece baixo**: Mesmo jogadores experientes devem começar no nível 3-4
2. **Foque no processo**: Não apenas ganhar, mas jogar bem
3. **Use análise**: Sempre revise após a partida
4. **Repita posições**: Pratique a mesma abertura/final várias vezes
5. **Graduamente suba**: Quando vencer 70%+, suba de nível

## FAQ

**P: Posso pausar a partida?**  
R: Sim, na modalidade "Sem Limite de Tempo"

**P: O computador sempre faz o mesmo movimento?**  
R: Não, há randomização em níveis mais baixos. Níveis altos tendem a ser consistentes.

**P: Posso configurar posições customizadas?**  
R: Sim, use o editor FEN em "Configurações > Posição Inicial"

**P: O computador "sabe" que estou usando hints?**  
R: Não, o engine não adapta seu jogo baseado nisso

**P: Posso jogar offline?**  
R: O Stockfish roda no seu navegador (WebAssembly), então sim após carregar uma vez

## Próximos Passos

- 🎮 **[Jogar Online](playing-games.md)**: Enfrente jogadores reais
- 🧩 **[Resolver Puzzles](solving-puzzles.md)**: Treine táticas
- 📚 **[Aprender](learning.md)**: Lições estruturadas

---

**Boa sorte contra a máquina! 🤖♟️**
