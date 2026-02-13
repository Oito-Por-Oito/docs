# Primeiro Projeto: Criando um Component de Xadrez

Neste tutorial, você aprenderá a criar um componente simples de tabuleiro de xadrez no OitoPorOito.

## Objetivo

Criar um componente `MiniBoard` que exibe uma posição de xadrez e permite movimentos básicos.

## Passo 1: Criar o Componente

Crie um novo arquivo em `src/components/MiniBoard.jsx`:

```jsx
import { useState } from 'react';
import { Chess } from 'chess.js';

export default function MiniBoard({ initialFen = 'start' }) {
  const [chess] = useState(new Chess(initialFen));
  const [position, setPosition] = useState(initialFen);

  return (
    <div className="miniboard">
      <h3>Mini Chess Board</h3>
      <div className="board-container">
        {/* Tabuleiro será renderizado aqui */}
      </div>
    </div>
  );
}
```

## Passo 2: Renderizar o Tabuleiro

Adicione a lógica para renderizar as casas:

```jsx
function MiniBoard({ initialFen = 'start' }) {
  const [chess] = useState(new Chess(initialFen));
  const [position, setPosition] = useState(chess.fen());

  const squares = [];
  const files = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h'];
  const ranks = ['8', '7', '6', '5', '4', '3', '2', '1'];

  // Gerar casas
  ranks.forEach((rank) => {
    files.forEach((file) => {
      const square = file + rank;
      const piece = chess.get(square);
      const isLight = (files.indexOf(file) + ranks.indexOf(rank)) % 2 === 0;

      squares.push(
        <div
          key={square}
          className={`square ${isLight ? 'light' : 'dark'}`}
          data-square={square}
        >
          {piece && (
            <div className="piece">
              {getPieceSymbol(piece)}
            </div>
          )}
        </div>
      );
    });
  });

  return (
    <div className="miniboard">
      <div className="board-grid">
        {squares}
      </div>
    </div>
  );
}

// Helper para símbolos de peças
function getPieceSymbol(piece) {
  const symbols = {
    'wp': '♙', 'wn': '♘', 'wb': '♗', 'wr': '♖', 'wq': '♕', 'wk': '♔',
    'bp': '♟', 'bn': '♞', 'bb': '♝', 'br': '♜', 'bq': '♛', 'bk': '♚',
  };
  return symbols[piece.color + piece.type] || '';
}
```

## Passo 3: Adicionar Estilos

Adicione estilos no mesmo arquivo ou em um CSS separado:

```jsx
<style jsx>{`
  .miniboard {
    display: inline-block;
    padding: 1rem;
    background: #2c2c2c;
    border-radius: 8px;
  }

  .board-grid {
    display: grid;
    grid-template-columns: repeat(8, 60px);
    grid-template-rows: repeat(8, 60px);
    border: 2px solid #1e1e1e;
  }

  .square {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 40px;
    user-select: none;
  }

  .square.light {
    background-color: #f0d9b5;
  }

  .square.dark {
    background-color: #b58863;
  }

  .piece {
    cursor: pointer;
    transition: transform 0.1s;
  }

  .piece:hover {
    transform: scale(1.1);
  }
`}</style>
```

Ou usando TailwindCSS:

```jsx
<div className="inline-block p-4 bg-chess-medium rounded-lg">
  <div className="grid grid-cols-8 grid-rows-8 border-2 border-chess-dark">
    {squares}
  </div>
</div>

// Classes para casas
className={`
  flex items-center justify-center
  w-[60px] h-[60px] text-4xl
  ${isLight ? 'bg-[#f0d9b5]' : 'bg-[#b58863]'}
`}
```

## Passo 4: Adicionar Interatividade

Adicione a capacidade de selecionar e mover peças:

```jsx
function MiniBoard({ initialFen = 'start' }) {
  const [chess] = useState(new Chess(initialFen));
  const [position, setPosition] = useState(chess.fen());
  const [selectedSquare, setSelectedSquare] = useState(null);

  const handleSquareClick = (square) => {
    if (!selectedSquare) {
      // Selecionar peça
      const piece = chess.get(square);
      if (piece && piece.color === chess.turn()) {
        setSelectedSquare(square);
      }
    } else {
      // Tentar fazer movimento
      try {
        chess.move({
          from: selectedSquare,
          to: square,
          promotion: 'q', // sempre promover para rainha
        });
        setPosition(chess.fen());
        setSelectedSquare(null);
      } catch (error) {
        // Movimento inválido
        setSelectedSquare(null);
      }
    }
  };

  // Adicionar onClick nas casas
  <div
    key={square}
    className={`square ${isLight ? 'light' : 'dark'} ${
      selectedSquare === square ? 'selected' : ''
    }`}
    onClick={() => handleSquareClick(square)}
  >
    {/* ... */}
  </div>
}
```

## Passo 5: Usar o Componente

Agora use o componente em qualquer página:

```jsx
// Em src/pages/Home.jsx
import MiniBoard from '@/components/MiniBoard';

function Home() {
  return (
    <div>
      <h1>Bem-vindo ao OitoPorOito</h1>
      
      {/* Posição inicial */}
      <MiniBoard />
      
      {/* Posição customizada */}
      <MiniBoard initialFen="r1bqkbnr/pppp1ppp/2n5/4p3/4P3/5N2/PPPP1PPP/RNBQKB1R w KQkq - 2 3" />
    </div>
  );
}
```

## Passo 6: Melhorias Opcionais

### Mostrar Movimentos Válidos

```jsx
const [validMoves, setValidMoves] = useState([]);

const handleSquareClick = (square) => {
  if (!selectedSquare) {
    const piece = chess.get(square);
    if (piece && piece.color === chess.turn()) {
      setSelectedSquare(square);
      // Obter movimentos válidos
      const moves = chess.moves({ square, verbose: true });
      setValidMoves(moves.map(m => m.to));
    }
  }
  // ...
};

// Destacar movimentos válidos
<div className={`
  square ${isLight ? 'light' : 'dark'}
  ${selectedSquare === square ? 'selected' : ''}
  ${validMoves.includes(square) ? 'valid-move' : ''}
`}>
```

### Animações de Movimento

```jsx
import { motion } from 'framer-motion';

<motion.div
  className="piece"
  initial={{ scale: 0 }}
  animate={{ scale: 1 }}
  exit={{ scale: 0 }}
  transition={{ duration: 0.2 }}
>
  {getPieceSymbol(piece)}
</motion.div>
```

### Histórico de Movimentos

```jsx
const [history, setHistory] = useState([]);

const handleMove = (from, to) => {
  const move = chess.move({ from, to, promotion: 'q' });
  if (move) {
    setHistory([...history, move.san]);
    setPosition(chess.fen());
  }
};

// Mostrar histórico
<div className="move-history">
  {history.map((move, i) => (
    <span key={i}>{i + 1}. {move}</span>
  ))}
</div>
```

## Teste seu Componente

1. Salve os arquivos
2. O servidor Vite recarregará automaticamente
3. Navegue para a página onde você adicionou o componente
4. Teste fazendo alguns movimentos

## Próximos Desafios

- 🎨 Adicionar temas de tabuleiro (madeira, pedra, etc.)
- 🔊 Adicionar sons de movimento
- ⏱️ Adicionar relógio de xadrez
- 📊 Mostrar avaliação da posição
- 🤖 Integrar com Stockfish para sugestões

## Recursos

- [Chess.js Documentation](https://github.com/jhlywa/chess.js)
- [Componentes do OitoPorOito](components/overview.md)
- [Framer Motion Docs](https://www.framer.com/motion/)

---

**Próximo:** [Componentes](components/overview.md) | [Arquitetura](architecture/overview.md)
