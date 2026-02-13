# Arquitetura Frontend

## Visão Geral

O frontend do OitoPorOito é uma Single Page Application (SPA) construída com React, utilizando Vite como bundler e desenvolvimento. A arquitetura é modular, componentizada e segue as melhores práticas da comunidade React.

## Stack Tecnológica

### Core
- **React 18**: Framework UI com Hooks e Concurrent Features
- **Vite 4**: Build tool moderna e rápida
- **React Router 7**: Roteamento client-side

### UI/UX
- **TailwindCSS**: Framework CSS utilitário
- **Radix UI**: Componentes acessíveis e sem estilo
- **Framer Motion**: Animações e transições
- **Lucide React**: Ícones modernos

### Xadrez
- **Chess.js**: Lógica de xadrez (validação, movimentos)
- **Stockfish**: Motor de análise e IA
- **Stockfish.wasm**: Versão WebAssembly do Stockfish

### Estado e Dados
- **Supabase Client**: Integração com backend
- **React Hooks**: Gerenciamento de estado local

### Ferramentas
- **date-fns**: Manipulação de datas
- **clsx**: Utilitário para classes CSS
- **recharts**: Gráficos e visualizações

## Estrutura de Diretórios

```
frontend/
├── public/                      # Assets estáticos
│   ├── assets/
│   │   ├── img/                # Imagens
│   │   └── pieces/             # Peças de xadrez (SVG)
│   └── stockfish/              # Engine Stockfish
│       ├── stockfish.js
│       └── stockfish.wasm.js
│
├── src/
│   ├── main.jsx                # Entry point
│   ├── App.jsx                 # Componente raiz (Home)
│   ├── AppRoutes.jsx           # Configuração de rotas
│   ├── index.css               # Estilos globais
│   │
│   ├── components/             # Componentes reutilizáveis
│   │   ├── Navbar.jsx
│   │   ├── Footer.jsx
│   │   ├── ChessBoardWithCTA.jsx
│   │   ├── ChessNewsGrid.jsx
│   │   ├── ChessPuzzle/
│   │   ├── ChessSocial/
│   │   ├── ChessEvents/
│   │   └── ...
│   │
│   ├── pages/                  # Páginas da aplicação
│   │   ├── Login.jsx
│   │   ├── Signup.jsx
│   │   ├── PlayComputer.jsx
│   │   ├── PuzzleChess.jsx
│   │   ├── ChessSocial.jsx
│   │   └── ...
│   │
│   ├── hooks/                  # Custom hooks
│   │   └── useAuth.js
│   │
│   ├── lib/                    # Bibliotecas e configurações
│   │   ├── supabaseClient.js  # Cliente Supabase
│   │   └── utils.js           # Utilitários gerais
│   │
│   ├── utils/                  # Utilitários específicos
│   │   ├── fenUtils.js        # Manipulação FEN
│   │   └── stockfishLoader.js # Loader do Stockfish
│   │
│   └── data/                   # Dados mockados/estáticos
│       └── chessData.js
│
├── plugins/                    # Plugins Vite customizados
│   └── visual-editor/
│
├── index.html                  # HTML raiz
├── vite.config.js             # Configuração Vite
├── tailwind.config.js         # Configuração Tailwind
└── package.json               # Dependências
```

## Roteamento

O roteamento é gerenciado pelo React Router v7. Todas as rotas são definidas em `AppRoutes.jsx`:

```jsx
// Rotas principais
/                    → Homepage (App.jsx)
/login               → Login
/signup              → Cadastro
/play                → Jogar online
/play-computer       → Jogar vs computador
/puzzle-chess        → Puzzles
/learn               → Aprender xadrez
/chessnews           → Notícias
/chess-events        → Eventos
/ratings-players     → Rankings

// Rotas sociais
/social              → Hub social
/social/friends      → Amigos
/social/clubs        → Clubes
/social/forums       → Fóruns
/social/members      → Membros
/social/blogs        → Blogs

// Fallback
*                    → 404 Page
```

## Componentes Principais

### 1. Navbar

Barra de navegação responsiva com:
- Logo e branding
- Links principais
- Botões de autenticação
- Menu mobile hamburger

### 2. ChessBoardWithCTA

Tabuleiro de xadrez interativo:
- Renderização de posições FEN
- Drag & drop de peças
- Validação de movimentos
- Integração com Chess.js

### 3. Authentication Components

Componentes de login e cadastro:
- Formulários validados
- Integração com Supabase Auth
- Gerenciamento de sessão
- Redirecionamentos

### 4. Puzzle Components

Componentes para puzzles de xadrez:
- Carregamento de posições
- Validação de soluções
- Sistema de hints
- Progressão de níveis

## Gerenciamento de Estado

### Estado Local (useState)
Usado para estado de componentes específicos:
```jsx
const [position, setPosition] = useState('start');
const [moves, setMoves] = useState([]);
```

### Estado Global (Context API)
Para dados compartilhados entre componentes:
```jsx
// AuthContext
const { user, signIn, signOut } = useAuth();
```

### Estado de Servidor (Supabase)
Queries em tempo real via Supabase:
```jsx
const { data, error } = await supabase
  .from('games')
  .select('*')
  .eq('user_id', user.id);
```

## Integração com Stockfish

O motor Stockfish é carregado como Web Worker:

```javascript
// stockfishLoader.js
export const loadStockfish = () => {
  const worker = new Worker('/stockfish/stockfish.wasm.js');
  
  worker.postMessage('uci');
  
  return {
    getMove: (fen, depth) => {
      worker.postMessage(`position fen ${fen}`);
      worker.postMessage(`go depth ${depth}`);
      
      return new Promise(resolve => {
        worker.onmessage = (e) => {
          // Parse bestmove
          resolve(bestMove);
        };
      });
    }
  };
};
```

## Integração com Chess.js

Todas as validações de xadrez usam Chess.js:

```javascript
import { Chess } from 'chess.js';

const chess = new Chess();

// Fazer movimento
const move = chess.move({ from: 'e2', to: 'e4' });

// Validar posição
const isCheck = chess.inCheck();
const isCheckmate = chess.isCheckmate();

// Gerar FEN
const fen = chess.fen();
```

## Estilização

### TailwindCSS
Classes utilitárias para estilização rápida:
```jsx
<div className="flex items-center justify-center bg-[#1e1e1e] text-white">
  <button className="px-4 py-2 bg-amber-500 hover:bg-amber-600 rounded">
    Jogar
  </button>
</div>
```

### Tema Customizado
Cores definidas em `tailwind.config.js`:
```javascript
theme: {
  extend: {
    colors: {
      'chess-dark': '#1e1e1e',
      'chess-light': '#2c2c2c',
      'chess-accent': '#f59e0b', // amber-500
    }
  }
}
```

## Performance

### Code Splitting
```jsx
const Login = lazy(() => import('./pages/Login'));
const Signup = lazy(() => import('./pages/Signup'));
```

### Memoization
```jsx
const MemoizedBoard = React.memo(ChessBoard, (prev, next) => {
  return prev.position === next.position;
});
```

### Lazy Loading
```jsx
<img loading="lazy" src="/assets/piece.svg" alt="Peça" />
```

## Testes (Planejado)

- **Unit**: Vitest para componentes
- **Integration**: React Testing Library
- **E2E**: Playwright

## Build e Deploy

### Desenvolvimento
```bash
npm run dev
# Servidor em http://localhost:5173
```

### Produção
```bash
npm run build
# Output em dist/
```

### Preview
```bash
npm run preview
# Preview da build de produção
```

## Próximos Passos

- 🔧 [Backend](backend.md)
- 💾 [Banco de Dados](database.md)
- 🧩 [Componentes](../components/overview.md)
