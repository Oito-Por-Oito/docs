# Guia de Estilo

Padrões de código e boas práticas para o projeto OitoPorOito.

## JavaScript / React

### Nomenclatura

```javascript
// Componentes: PascalCase
function ChessBoard() { }
export default ChessBoard;

// Variáveis e funções: camelCase
const playerRating = 1500;
function calculateRating() { }

// Constantes: UPPER_SNAKE_CASE
const MAX_PLAYERS = 100;
const API_URL = 'https://api.example.com';

// Arquivos de componentes: PascalCase
ChessBoard.jsx
UserProfile.jsx

// Outros arquivos: camelCase
utils.js
fenParser.js

// Hooks customizados: camelCase com prefixo "use"
useAuth.js
useChessGame.js

// Tipos/Interfaces: PascalCase
interface GameState { }
type PlayerData = { };
```

### Estrutura de Componentes

```jsx
import { useState, useEffect } from 'react';
import PropTypes from 'prop-types';

/**
 * Breve descrição do componente
 * 
 * @param {Object} props - Props do componente
 * @param {string} props.title - Título exibido
 * @param {Function} props.onAction - Callback quando ação ocorre
 */
export default function MyComponent({ title, onAction }) {
  // 1. Estados
  const [isActive, setIsActive] = useState(false);
  
  // 2. Refs
  const boardRef = useRef(null);
  
  // 3. Context
  const { user } = useAuth();
  
  // 4. Effects
  useEffect(() => {
    // Lógica do effect
    return () => {
      // Cleanup
    };
  }, []);
  
  // 5. Handlers e funções
  const handleClick = () => {
    setIsActive(true);
    onAction?.();
  };
  
  // 6. Early returns
  if (!user) {
    return <div>Please login</div>;
  }
  
  // 7. Render
  return (
    <div className="my-component">
      <h2>{title}</h2>
      <button onClick={handleClick}>
        Click me
      </button>
    </div>
  );
}

// PropTypes
MyComponent.propTypes = {
  title: PropTypes.string.isRequired,
  onAction: PropTypes.func,
};

// Default Props
MyComponent.defaultProps = {
  onAction: () => {},
};
```

### Hooks Rules

```javascript
// ✅ Bom: Chamadas no topo
function Component() {
  const [state, setState] = useState();
  const value = useContext(MyContext);
  useEffect(() => { }, []);
  
  return <div />;
}

// ❌ Ruim: Hooks condicionais
function Component({ condition }) {
  if (condition) {
    const [state] = useState(); // ❌ Nunca condicional
  }
  return <div />;
}

// ✅ Bom: Lógica após hooks
function Component({ condition }) {
  const [state, setState] = useState();
  
  if (condition) {
    setState(newValue); // ✅ OK
  }
  
  return <div />;
}
```

### State Management

```javascript
// ✅ Bom: Estado mínimo necessário
const [position, setPosition] = useState('start');

// ❌ Ruim: Estado derivado
const [position, setPosition] = useState('start');
const [isStartPosition, setIsStartPosition] = useState(true); // Derivado!

// ✅ Bom: Computar quando necessário
const [position, setPosition] = useState('start');
const isStartPosition = position === 'start'; // Computed
```

### Event Handlers

```javascript
// ✅ Bom: Nome descritivo começando com "handle"
const handleSubmit = (e) => {
  e.preventDefault();
  // ...
};

const handlePlayerMove = (move) => {
  // ...
};

// ❌ Ruim: Nomes genéricos
const onClick = () => { }; // Muito genérico
const submit = () => { }; // Falta "handle"
```

### Imports

```javascript
// Ordem:
// 1. React
import { useState, useEffect } from 'react';
import PropTypes from 'prop-types';

// 2. Bibliotecas externas
import { Chess } from 'chess.js';
import clsx from 'clsx';

// 3. Componentes
import ChessBoard from '@/components/ChessBoard';
import Button from '@/components/ui/Button';

// 4. Hooks
import { useAuth } from '@/hooks/useAuth';

// 5. Utils
import { fenToObject } from '@/utils/fenUtils';

// 6. Tipos
import type { GameState } from '@/types';

// 7. Estilos
import './MyComponent.css';
```

## CSS / TailwindCSS

### Ordem de Classes

```jsx
// Ordem lógica: Layout → Tamanho → Espaçamento → Visual → Tipografia → Interação
<div className="
  flex items-center justify-center
  w-full h-screen
  p-4 m-2
  bg-gray-900 border border-gray-700 rounded-lg
  text-white text-lg font-bold
  hover:bg-gray-800 cursor-pointer
  transition-colors
">
  Content
</div>
```

### Componentes Reutilizáveis

```javascript
// ✅ Bom: Extrair classes repetidas
const buttonClasses = "px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600";

<button className={buttonClasses}>Click</button>

// ✅ Melhor: Usar cn() helper
import { cn } from '@/lib/utils';

<button className={cn(
  "px-4 py-2 rounded",
  "bg-blue-500 text-white",
  "hover:bg-blue-600",
  isActive && "ring-2 ring-blue-300",
  className // Props externas
)}>
  Click
</button>
```

## Comentários

### JSDoc para Funções

```javascript
/**
 * Calcula o novo rating após uma partida
 * 
 * @param {number} currentRating - Rating atual do jogador
 * @param {number} opponentRating - Rating do oponente
 * @param {number} result - Resultado (1 = vitória, 0.5 = empate, 0 = derrota)
 * @returns {number} Novo rating calculado
 * 
 * @example
 * const newRating = calculateRating(1500, 1600, 1);
 * // newRating: 1516
 */
function calculateRating(currentRating, opponentRating, result) {
  // Implementação
}
```

### Comentários Inline

```javascript
// ✅ Bom: Explicar "porquê", não "o quê"
// Precisamos validar antes porque Chess.js lança exceção
if (!isValidMove(move)) {
  return;
}

// ❌ Ruim: Óbvio
// Incrementa contador
counter++;
```

### TODO Comments

```javascript
// TODO: Implementar sistema de hints
// FIXME: Bug quando peão promove
// HACK: Workaround temporário para issue #123
// NOTE: Esta lógica é complexa devido a...
```

## Git

### Commit Messages

Siga [Conventional Commits](https://www.conventionalcommits.org/):

```bash
# Formato
<type>(<scope>): <description>

[body opcional]

[footer opcional]
```

**Tipos:**
- `feat`: Nova funcionalidade
- `fix`: Correção de bug
- `docs`: Documentação
- `style`: Formatação (não afeta código)
- `refactor`: Refatoração
- `test`: Testes
- `chore`: Tarefas gerais

**Exemplos:**

```bash
feat(chess): adiciona validação de roque

Implementa verificação completa de legalidade do roque,
incluindo:
- Rei e torre não podem ter movido
- Casas entre devem estar vazias
- Rei não pode passar por xeque

Closes #42

---

fix(puzzle): corrige cálculo de rating

Rating estava sendo calculado incorretamente para
puzzles de rating muito alto (>2500).

Fixes #156

---

docs(api): atualiza endpoint de autenticação

Adiciona exemplos de uso e códigos de erro.

---

refactor(board): simplifica lógica de renderização

Reduz complexidade de O(n²) para O(n) usando memoization.

---

test(game): adiciona testes para en passant

Coverage aumentou de 78% para 85%.
```

### Branch Names

```bash
# Features
feature/matchmaking-system
feature/tournament-mode

# Bugfixes
fix/pawn-promotion-bug
fix/auth-token-expiry

# Docs
docs/api-documentation
docs/component-guide

# Refactor
refactor/state-management
refactor/chess-engine
```

## Testes

### Estrutura

```javascript
import { render, screen, fireEvent } from '@testing-library/react';
import ChessBoard from './ChessBoard';

describe('ChessBoard', () => {
  // Setup comum
  beforeEach(() => {
    // ...
  });
  
  describe('rendering', () => {
    it('renders 64 squares', () => {
      render(<ChessBoard />);
      const squares = screen.getAllByRole('button');
      expect(squares).toHaveLength(64);
    });
  });
  
  describe('piece movement', () => {
    it('allows valid moves', () => {
      const onMove = jest.fn();
      render(<ChessBoard onMove={onMove} />);
      
      // Simular movimento
      fireEvent.click(screen.getByTestId('e2'));
      fireEvent.click(screen.getByTestId('e4'));
      
      expect(onMove).toHaveBeenCalledWith({ from: 'e2', to: 'e4' });
    });
    
    it('prevents invalid moves', () => {
      const onMove = jest.fn();
      render(<ChessBoard onMove={onMove} />);
      
      // Movimento inválido
      fireEvent.click(screen.getByTestId('e2'));
      fireEvent.click(screen.getByTestId('e5'));
      
      expect(onMove).not.toHaveBeenCalled();
    });
  });
});
```

## Acessibilidade

```jsx
// ✅ Bom: Semântica apropriada
<button onClick={handleClick}>Click me</button>

// ❌ Ruim: div como botão
<div onClick={handleClick}>Click me</div>

// ✅ Bom: Alt text em imagens
<img src="piece.png" alt="White Queen" />

// ✅ Bom: Labels em forms
<label htmlFor="email">Email</label>
<input id="email" type="email" />

// ✅ Bom: ARIA quando necessário
<div role="button" tabIndex={0} onClick={handleClick}>
  Custom button
</div>

// ✅ Bom: Keyboard navigation
<div
  tabIndex={0}
  onKeyDown={(e) => {
    if (e.key === 'Enter' || e.key === ' ') {
      handleClick();
    }
  }}
>
```

## Performance

```javascript
// ✅ Bom: Memoização
import { memo } from 'react';

const ChessSquare = memo(({ square }) => {
  return <div>{square}</div>;
}, (prev, next) => {
  return prev.square === next.square;
});

// ✅ Bom: useMemo para cálculos pesados
const validMoves = useMemo(() => {
  return chess.moves({ verbose: true });
}, [position]);

// ✅ Bom: useCallback para callbacks
const handleMove = useCallback((move) => {
  // ...
}, [position]);

// ✅ Bom: Lazy loading
const AnalysisBoard = lazy(() => import('./AnalysisBoard'));
```

## Segurança

```javascript
// ✅ Bom: Sanitize user input
import DOMPurify from 'dompurify';

const cleanHTML = DOMPurify.sanitize(userInput);

// ❌ Ruim: dangerouslySetInnerHTML sem sanitização
<div dangerouslySetInnerHTML={{ __html: userInput }} />

// ✅ Bom: Validação de entrada
const isValidUsername = (name) => {
  return /^[a-zA-Z0-9_]{3,20}$/.test(name);
};

// ✅ Bom: Nunca expor secrets
// Use variáveis de ambiente
const apiKey = import.meta.env.VITE_API_KEY;
```

## Revisão de Código

### Checklist do Autor

Antes de abrir PR:

- [ ] Código compila sem erros
- [ ] Testes passam
- [ ] Sem warnings no console
- [ ] Código formatado (Prettier)
- [ ] Lint sem erros  (ESLint)
- [ ] Documentação atualizada
- [ ] Commit messages seguem padrão
- [ ] Self-review realizado

### Checklist do Reviewer

Ao revisar PR:

- [ ] Código é legível e compreensível
- [ ] Lógica está correta
- [ ] Testes são adequados
- [ ] Sem duplicação desnecessária
- [ ] Performance é aceitável
- [ ] Segurança foi considerada
- [ ] docs foram atualizadas

---

**Lembre-se**: Código é lido muito mais vezes do que escrito. Priorize clareza sobre "inteligência".
