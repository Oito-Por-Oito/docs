# Configuração Avançada

Este guia cobre opções de configuração avançadas para o OitoPorOito.

## Variáveis de Ambiente

### Arquivo `.env`

Todas as variáveis de ambiente devem ser prefixadas com `VITE_` para serem acessíveis no frontend:

```ini
# ====================
# Supabase Configuration
# ====================
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key

# ====================
# Stockfish Configuration
# ====================
VITE_STOCKFISH_PATH=/stockfish/
VITE_STOCKFISH_THREADS=2
VITE_STOCKFISH_HASH=128  # MB de memória

# ====================
# App Configuration
# ====================
VITE_APP_NAME=OitoPorOito
VITE_APP_URL=http://localhost:5173
VITE_APP_VERSION=0.1.0

# ====================
# Feature Flags
# ====================
VITE_ENABLE_SOCIAL=true
VITE_ENABLE_TOURNAMENTS=false
VITE_ENABLE_ANALYSIS=true

# ====================
# Analytics (Opcional)
# ====================
VITE_GA_TRACKING_ID=
VITE_SENTRY_DSN=

# ====================
# API Limits
# ====================
VITE_MAX_GAME_TIME=3600  # segundos
VITE_PUZZLE_DAILY_LIMIT=100
VITE_API_RATE_LIMIT=60  # requests/minuto
```

### Ambientes Separados

#### Desenvolvimento (`.env.development`)

```ini
VITE_SUPABASE_URL=https://dev-project.supabase.co
VITE_SUPABASE_ANON_KEY=dev-key
VITE_APP_URL=http://localhost:5173
VITE_DEBUG=true
```

#### Produção (`.env.production`)

```ini
VITE_SUPABASE_URL=https://prod-project.supabase.co
VITE_SUPABASE_ANON_KEY=prod-key
VITE_APP_URL=https://oitoporoito.com
VITE_DEBUG=false
```

### Acessando Variáveis no Código

```javascript
// Importar variáveis
const supabaseUrl = import.meta.env.VITE_SUPABASE_URL;
const supabaseKey = import.meta.env.VITE_SUPABASE_ANON_KEY;

// Validar se estão definidas
if (!supabaseUrl || !supabaseKey) {
  throw new Error('Missing Supabase credentials');
}

// Usar no código
export const supabase = createClient(supabaseUrl, supabaseKey);
```

## Configuração do Vite

### `vite.config.js`

```javascript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import path from 'path';

export default defineConfig({
  plugins: [react()],
  
  // Aliases de caminho
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
      '@components': path.resolve(__dirname, './src/components'),
      '@pages': path.resolve(__dirname, './src/pages'),
      '@hooks': path.resolve(__dirname, './src/hooks'),
      '@lib': path.resolve(__dirname, './src/lib'),
      '@utils': path.resolve(__dirname, './src/utils'),
      '@data': path.resolve(__dirname, './src/data'),
    },
  },
  
  // Configuração do servidor
  server: {
    port: 5173,
    host: true, // Expor na rede local
    open: true, // Abrir navegador automaticamente
    cors: true,
    
    // Proxy para APIs externas
    proxy: {
      '/api': {
        target: 'http://localhost:3000',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, ''),
      },
    },
  },
  
  // Otimizações de build
  build: {
    outDir: 'dist',
    sourcemap: true,
    minify: 'terser',
    
    // Code splitting
    rollupOptions: {
      output: {
        manualChunks: {
          'react-vendor': ['react', 'react-dom', 'react-router-dom'],
          'ui-vendor': ['@radix-ui/react-dialog', '@radix-ui/react-dropdown-menu'],
          'chess-vendor': ['chess.js', 'stockfish.wasm'],
        },
      },
    },
    
    // Chunk size warnings
    chunkSizeWarningLimit: 1000,
  },
  
  // Otimizações de dependências
  optimizeDeps: {
    include: ['react', 'react-dom', 'react-router-dom', 'chess.js'],
    exclude: ['stockfish.wasm'],
  },
});
```

### Plugins Customizados

O projeto inclui plugins customizados em `plugins/visual-editor/`:

```javascript
// vite.config.js
import visualEditor from './plugins/visual-editor/vite-plugin-edit-mode';

export default defineConfig({
  plugins: [
    react(),
    visualEditor(), // Plugin customizado
  ],
});
```

## Configuração do TailwindCSS

### `tailwind.config.js`

```javascript
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      // Cores customizadas
      colors: {
        'chess-dark': '#1e1e1e',
        'chess-medium': '#2c2c2c',
        'chess-light': '#3a3a3a',
        'chess-accent': '#f59e0b',
        'chess-board-light': '#f0d9b5',
        'chess-board-dark': '#b58863',
      },
      
      // Fontes
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
        mono: ['JetBrains Mono', 'monospace'],
      },
      
      // Animações
      animation: {
        'fade-in': 'fadeIn 0.3s ease-in-out',
        'slide-up': 'slideUp 0.3s ease-out',
        'piece-move': 'pieceMove 0.2s ease-in-out',
      },
      
      keyframes: {
        fadeIn: {
          '0%': { opacity: '0' },
          '100%': { opacity: '1' },
        },
        slideUp: {
          '0%': { transform: 'translateY(10px)', opacity: '0' },
          '100%': { transform: 'translateY(0)', opacity: '1' },
        },
        pieceMove: {
          '0%': { transform: 'scale(1)' },
          '50%': { transform: 'scale(1.1)' },
          '100%': { transform: 'scale(1)' },
        },
      },
      
      // Spacing customizado para tabuleiro
      spacing: {
        'board': '80vh',
        'square': '12.5%',
      },
    },
  },
  plugins: [
    require('tailwindcss-animate'),
  ],
}
```

## Configuração do ESLint

### `.eslintrc.cjs`

```javascript
module.exports = {
  root: true,
  env: {
    browser: true,
    es2021: true,
    node: true,
  },
  extends: [
    'eslint:recommended',
    'plugin:react/recommended',
    'plugin:react/jsx-runtime',
    'plugin:react-hooks/recommended',
  ],
  parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module',
    ecmaFeatures: {
      jsx: true,
    },
  },
  settings: {
    react: {
      version: 'detect',
    },
  },
  plugins: ['react', 'react-hooks', 'react-refresh'],
  rules: {
    'react/prop-types': 'warn',
    'react-hooks/rules-of-hooks': 'error',
    'react-hooks/exhaustive-deps': 'warn',
    'react-refresh/only-export-components': 'warn',
    'no-unused-vars': ['warn', { argsIgnorePattern: '^_' }],
    'no-console': ['warn', { allow: ['warn', 'error'] }],
  },
};
```

## Configuração do Git

### `.gitignore`

```gitignore
# Dependências
node_modules/
package-lock.json
yarn.lock
pnpm-lock.yaml

# Build outputs
dist/
build/
.vite/

# Ambientes
.env
.env.local
.env.development.local
.env.production.local

# IDEs
.vscode/
.idea/
*.swp
*.swo
*~

# OS
.DS_Store
Thumbs.db

# Logs
logs/
*.log
npm-debug.log*

# Testes
coverage/
.nyc_output/

# Temporários
tmp/
temp/
```

### `.gitattributes`

```gitattributes
# Auto detect text files
* text=auto

# Source code
*.js text eol=lf
*.jsx text eol=lf
*.json text eol=lf
*.css text eol=lf
*.html text eol=lf
*.md text eol=lf

# Binary files
*.png binary
*.jpg binary
*.wasm binary
```

## VS Code Settings

### `.vscode/settings.json`

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "files.associations": {
    "*.css": "tailwindcss"
  },
  "tailwindCSS.experimental.classRegex": [
    ["clsx\\(([^)]*)\\)", "(?:'|\"|`)([^']*)(?:'|\"|`)"]
  ],
  "eslint.validate": [
    "javascript",
    "javascriptreact"
  ]
}
```

### `.vscode/extensions.json`

```json
{
  "recommendations": [
    "dbaeumer.vscode-eslint",
    "esbenp.prettier-vscode",
    "bradlc.vscode-tailwindcss",
    "dsznajder.es7-react-js-snippets",
    "formulahendry.auto-rename-tag"
  ]
}
```

## Performance

### Lazy Loading de Componentes

```javascript
import { lazy, Suspense } from 'react';

// Lazy load páginas
const Login = lazy(() => import('./pages/Login'));
const Signup = lazy(() => import('./pages/Signup'));
const Play = lazy(() => import('./pages/Play'));

// Usar com Suspense
<Suspense fallback={<Loading />}>
  <Route path="/login" element={<Login />} />
</Suspense>
```

### Memoização

```javascript
import { memo, useMemo, useCallback } from 'react';

// Memoizar componente
const ChessBoard = memo(({ position, onMove }) => {
  // ...
}, (prev, next) => prev.position === next.position);

// Memoizar valor
const moves = useMemo(() => {
  return chess.moves({ verbose: true });
}, [position]);

// Memoizar callback
const handleMove = useCallback((move) => {
  // ...
}, [position]);
```

## Próximos Passos

- 🎯 [Primeiro Projeto](first-project.md)
- 🏗️ [Arquitetura](architecture/overview.md)
- 🤝 [Como Contribuir](../contributing/how-to-contribute.md)
