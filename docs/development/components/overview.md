# Documentação de Componentes

Esta seção documenta todos os componentes React do OitoPorOito.

## Estrutura de Componentes

```
src/components/
├── Core/                    # Componentes principais
│   ├── Navbar.jsx
│   ├── Footer.jsx
│   └── Section.jsx
│
├── Chess/                   # Componentes de xadrez
│   ├── ChessBoardWithCTA.jsx
│   ├── MoveHistory.jsx
│   └── PieceSelector.jsx
│
├── Puzzle/                  # Puzzles
│   ├── ChessPuzzleCard.jsx
│   ├── PuzzleChessBoard.jsx
│   └── PuzzleChessCard.jsx
│
├── Social/                  # Recursos sociais
│   ├── ChessFriends/
│   ├── ChessClubs/
│   ├── ChessForum/
│   ├── ChessMembers/
│   └── ChessBlogs/
│
├── News/                    # Notícias e conteúdo
│   ├── ChessNewsGrid.jsx
│   └── ArticleCard.jsx
│
├── Events/                  # Eventos
│   ├── ChessTVSchedule.jsx
│   ├── EventoCard.jsx
│   └── RankingList.jsx
│
└── UI/                      # Componentes de UI
    ├── Button.jsx
    ├── Card.jsx
    ├── Avatar.jsx
    └── Modal.jsx
```

## Componentes Principais

### Navbar

Barra de navegação responsiva principal.

**Localização:** `src/components/Navbar.jsx`

**Props:**
```typescript
interface NavbarProps {
  user?: User | null;
  onLogin?: () => void;
  onLogout?: () => void;
}
```

**Exemplo:**
```jsx
import Navbar from '@/components/Navbar';

<Navbar 
  user={currentUser}
  onLogin={handleLogin}
  onLogout={handleLogout}
/>
```

**Recursos:**
- Logo clicável
- Links de navegação
- Dropdown de usuário
- Menu hamburger (mobile)
- Indicador de notificações

---

### Footer

Rodapé da aplicação com links e informações.

**Localização:** `src/components/Footer.jsx`

**Props:** Nenhuma

**Exemplo:**
```jsx
import Footer from '@/components/Footer';

<Footer />
```

**Conteúdo:**
- Links de navegação
- Redes sociais
- Copyright
- Links legais

---

### ChessBoardWithCTA

Tabuleiro de xadrez interativo com call-to-action.

**Localização:** `src/components/ChessBoardWithCTA.jsx`

**Props:**
```typescript
interface ChessBoardProps {
  initialPosition?: string; // FEN
  onMove?: (move: Move) => void;
  editable?: boolean;
  showCTA?: boolean;
  ctaText?: string;
  onCTAClick?: () => void;
}
```

**Exemplo:**
```jsx
<ChessBoardWithCTA
  initialPosition="rnbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1"
  onMove={(move) => console.log(move)}
  editable={true}
  showCTA={true}
  ctaText="Jogar Agora"
  onCTAClick={() => navigate('/play')}
/>
```

**Recursos:**
- Drag & drop de peças
- Validação de movimentos
- Destaque de casas
- Movimentos válidos
- Animações

---

## Componentes de Puzzle

### PuzzleChessBoard

Tabuleiro específico para puzzles.

**Localização:** `src/components/ChessPuzzle/PuzzleChessBoard.jsx`

**Props:**
```typescript
interface PuzzleChessBoardProps {
  fen: string;
  solution: string[];
  onSolve: (solved: boolean) => void;
  onGiveUp: () => void;
  showHints?: boolean;
}
```

**Exemplo:**
```jsx
<PuzzleChessBoard
  fen="r1bqkbnr/pppp1ppp/2n5/4p3/4P3/5N2/PPPP1PPP/RNBQKB1R w KQkq -"
  solution={['Nxe5', 'Nxe5', 'Qe2']}
  onSolve={(solved) => handleSolve(solved)}
  onGiveUp={handleGiveUp}
  showHints={true}
/>
```

---

## Componentes Sociais

### FriendList

Lista de amigos do usuário.

**Localização:** `src/components/ChessFriends/FriendList.jsx`

**Props:**
```typescript
interface FriendListProps {
  friends: Friend[];
  onChallenge: (friendId: string) => void;
  onMessage: (friendId: string) => void;
  onRemove: (friendId: string) => void;
}
```

**Exemplo:**
```jsx
<FriendList
  friends={userFriends}
  onChallenge={(id) => challengeFriend(id)}
  onMessage={(id) => openChat(id)}
  onRemove={(id) => removeFriend(id)}
/>
```

---

### ClubCard

Card de exibição de clube.

**Localização:** `src/components/ChessClubs/ClubItem.jsx`

**Props:**
```typescript
interface ClubCardProps {
  club: Club;
  isMember?: boolean;
  onJoin?: (clubId: string) => void;
  onLeave?: (clubId: string) => void;
  onClick?: (clubId: string) => void;
}
```

---

## Componentes de UI Reutilizáveis

### Button

Botão customizado com variantes.

**Localização:** `src/components/ui/Button.jsx` (se existir)

**Props:**
```typescript
interface ButtonProps {
  variant?: 'primary' | 'secondary' | 'danger' | 'ghost';
  size?: 'sm' | 'md' | 'lg';
  disabled?: boolean;
  loading?: boolean;
  onClick?: () => void;
  children: ReactNode;
}
```

**Exemplo:**
```jsx
<Button 
  variant="primary" 
  size="lg"
  onClick={handleClick}
>
  Jogar Agora
</Button>
```

---

### Card

Container de conteúdo estilizado.

**Props:**
```typescript
interface CardProps {
  title?: string;
  subtitle?: string;
  image?: string;
  children: ReactNode;
  onClick?: () => void;
  className?: string;
}
```

**Exemplo:**
```jsx
<Card 
  title="Puzzle do Dia"
  subtitle="Rating: 1500"
  image="/puzzle-thumbnail.png"
>
  <PuzzleChessBoard {...puzzleProps} />
</Card>
```

---

## Hooks Customizados

### useAuth

Hook de autenticação.

**Localização:** `src/hooks/useAuth.js`

**Uso:**
```javascript
const { user, loading, signIn, signOut, signUp } = useAuth();

// Login
await signIn(email, password);

// Logout
await signOut();

// Verificar autenticação
if (user) {
  // Usuário logado
}
```

---

### useChessGame

Hook para gerenciar estado de jogo de xadrez.

**Localização:** `src/hooks/useChessGame.js` (criar se não existir)

**Exemplo:**
```javascript
const {
  game,
  position,
  turn,
  isCheck,
  isCheckmate,
  makeMove,
  reset,
  undo
} = useChessGame(initialFen);

// Fazer movimento
makeMove({ from: 'e2', to: 'e4' });

// Desfazer
undo();

// Resetar
reset();
```

---

## Utilitários

### fenUtils.js

Funções para trabalhar com notação FEN.

**Localização:** `src/utils/fenUtils.js`

**Funções:**
```javascript
// Validar FEN
isValidFen(fen: string): boolean

// Extrair informações
getFenPieces(fen: string): Piece[]
getTurnFromFen(fen: string): 'w' | 'b'
getCastlingRights(fen: string): string

// Manipular FEN
updateFenPosition(fen: string, position: string): string
```

---

### stockfishLoader.js

Carregar e interagir com Stockfish engine.

**Localização:** `src/utils/stockfishLoader.js`

**Uso:**
```javascript
import { loadStockfish } from '@/utils/stockfishLoader';

const stockfish = await loadStockfish();

// Analisar posição
stockfish.analyze(fen, depth).then(result => {
  console.log(result.bestMove);
  console.log(result.evaluation);
});

// Parar análise
stockfish.stop();
```

---

## Padrões de Desenvolvimento

### Nomenclatura

- **Componentes**: PascalCase (`ChessBoard.jsx`)
- **Hooks**: camelCase com prefixo `use` (`useAuth.js`)
- **Utilidades**: camelCase (`fenUtils.js`)
- **Constantes**: UPPER_SNAKE_CASE (`API_URL`)

### Estrutura de Componente

```jsx
import { useState, useEffect } from 'react';
import PropTypes from 'prop-types';

/**
 * Descrição do componente
 * @param {Object} props - Props do componente
 */
export default function MyComponent({ title, onAction }) {
  // Estados
  const [state, setState] = useState(null);
  
  // Effects
  useEffect(() => {
    // ...
  }, []);
  
  // Handlers
  const handleClick = () => {
    // ...
  };
  
  // Render
  return (
    <div className="my-component">
      {/* JSX */}
    </div>
  );
}

// PropTypes
MyComponent.propTypes = {
  title: PropTypes.string.isrequired,
  onAction: PropTypes.func,
};

// Default Props
MyComponent.defaultProps = {
  onAction: () => {},
};
```

### Estilização

Use TailwindCSS:
```jsx
<div className="flex items-center justify-center bg-chess-dark p-4 rounded-lg">
  {/* Conteúdo */}
</div>
```

Para estilos complexos, use a função `cn()`:
```jsx
import { cn } from '@/lib/utils';

<div className={cn(
  "base-classes",
  isActive && "active-classes",
  className // Prop externa
)}>
```

---

## Próximos Passos

- �️ [Arquitetura Frontend](../architecture/frontend.md)
- 🎯 [Primeiro Projeto](../first-project.md)
