# Começando com o Desenvolvimento

Este guia irá ajudá-lo a configurar o ambiente de desenvolvimento do OitoPorOito em sua máquina local.

## Pré-requisitos

Antes de começar, certifique-se de ter instalado:

### Obrigatórios

- **Node.js** 20.x ou superior ([Download](https://nodejs.org/))
- **npm** 9.x ou superior (vem com Node.js)
- **Git** ([Download](https://git-scm.com/))

### Recomendados

- **VS Code** ([Download](https://code.visualstudio.com/))
- **Extensões VS Code:**
    - ESLint
    - Prettier
    - Tailwind CSS IntelliSense
    - ES7+ React/Redux/React-Native snippets

### Verificar Instalação

```bash
# Verificar versões
node --version  # Deve ser v20.x.x ou superior
npm --version   # Deve ser 9.x.x ou superior
git --version
```

## Configuração do Projeto

### 1. Clone o Repositório

```bash
# Clone o frontend
git clone https://github.com/Oito-Por-Oito/frontend.git
cd frontend
```

### 2. Instale as Dependências

```bash
npm install
```

Este comando irá:
- Instalar todas as dependências do `package.json`
- Baixar o engine Stockfish WASM
- Configurar os hooks do Git (se houver)

**Tempo estimado:** 2-5 minutos dependendo da conexão

### 3. Configure as Variáveis de Ambiente

Crie um arquivo `.env` na raiz do projeto:

```bash
# Windows
copy .env.example .env

# Linux/Mac
cp .env.example .env
```

Edite o arquivo `.env` com suas credenciais:

```ini
# Supabase
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key-here

# Opcional: Outros serviços
VITE_STOCKFISH_PATH=/stockfish/
```

!!! warning "Credenciais do Supabase"
    Para obter as credenciais do Supabase:
    1. Crie uma conta em [supabase.com](https://supabase.com)
    2. Crie um novo projeto
    3. Vá em Settings > API
    4. Copie a URL e a chave `anon/public`

### 4. Inicie o Servidor de Desenvolvimento

```bash
npm run dev
```

O servidor iniciará em [http://localhost:5173](http://localhost:5173)

Você verá uma saída similar a:

```
  VITE v4.4.5  ready in 523 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h to show help
```

## Scripts Disponíveis

### Desenvolvimento

```bash
# Iniciar servidor de desenvolvimento
npm run dev

# Iniciar com host network (acessível na rede local)
npm run dev -- --host
```

### Build

```bash
# Criar build de produção
npm run build

# Preview da build de produção
npm run preview
```

### Linting e Formatação

```bash
# Verificar erros de linting
npm run lint

# Corrigir problemas automaticamente
npm run lint:fix

# Formatar código com Prettier
npm run format
```

### Testes (quando implementados)

```bash
# Rodar testes
npm test

# Testes em modo watch
npm test:watch

# Coverage
npm test:coverage
```

## Estrutura do Projeto

Após a instalação, sua estrutura será:

```
frontend/
├── node_modules/           # Dependências (não commitar)
├── public/                 # Assets estáticos
│   ├── assets/
│   └── stockfish/
├── src/                    # Código-fonte
│   ├── components/        # Componentes React
│   ├── pages/             # Páginas
│   ├── hooks/             # Custom hooks
│   ├── lib/               # Bibliotecas e utils
│   ├── utils/             # Utilitários
│   ├── data/              # Dados estáticos
│   ├── App.jsx            # Componente raiz
│   ├── AppRoutes.jsx      # Rotas
│   ├── main.jsx           # Entry point
│   └── index.css          # Estilos globais
├── .env                    # Variáveis de ambiente (não commitar)
├── .gitignore             # Arquivos ignorados pelo Git
├── index.html             # HTML raiz
├── package.json           # Dependências e scripts
├── vite.config.js         # Configuração Vite
└── tailwind.config.js     # Configuração Tailwind
```

## Próximos Passos

Agora que você configurou o projeto:

1. 📖 **Leia a documentação:**
   - [Arquitetura](architecture/overview.md)
   - [Componentes](components/overview.md)
   - [Configuração Avançada](configuration.md)

2. 🎯 **Faça seu primeiro projeto:**
   - [Tutorial: Primeiro Projeto](first-project.md)

3. 🤝 **Contribua:**
   - [Como Contribuir](../contributing/how-to-contribute.md)
   - [Guia de Estilo](../contributing/style-guide.md)

## Solução de Problemas

### Erro: "Cannot find module"

```bash
# Limpe o cache e reinstale
rm -rf node_modules package-lock.json
npm install
```

### Erro: "Port 5173 is already in use"

```bash
# Use uma porta diferente
npm run dev -- --port 3000
```

### Erro de Importação do Stockfish

```bash
# Verifique se o stockfish foi baixado
ls public/stockfish/

# Se não existir, reinstale
npm install stockfish.wasm
```

### Problemas com ESM

Se encontrar erros de módulos ES, verifique:
- `"type": "module"` está em `package.json`
- Imports usam `.js` ou `.jsx` nas extensões
- Vite config está correto

### Limpeza Completa

```bash
# Windows
rmdir /s /q node_modules
del package-lock.json
npm install

# Linux/Mac
rm -rf node_modules package-lock.json
npm install
```

## Suporte

Encontrou um problema? 

- 📚 [FAQ](../resources/faq.md)
- 🐛 [Reportar Bug](https://github.com/Oito-Por-Oito/frontend/issues)
- 💬 [Discussions](https://github.com/Oito-Por-Oito/discussions)

---

**Próximo:** [Configuração Avançada](configuration.md)