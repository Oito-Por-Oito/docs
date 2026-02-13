# API - Introdução

Bem-vindo à documentação da API do OitoPorOito. Esta API REST fornece acesso programático a todas as funcionalidades da plataforma.

## Base URL

```
https://api.oitoporoito.com/v1
```

Desenvolvimento:
```
http://localhost:3000/v1
```

## Autenticação

A API usa **Bearer Token** (JWT) para autenticação via Supabase.

### Obter Token

```bash
POST /auth/login
Content-Type: application/json

{
  "email": "usuario@example.com",
  "password": "senha123"
}
```

Resposta:
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "refresh_token": "...",
  "expires_in": 3600,
  "user": {
    "id": "uuid",
    "email": "usuario@example.com",
    "username": "jogador123"
  }
}
```

### Usar Token

Inclua o token no header `Authorization`:

```bash
GET /api/users/me
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

## Formato de Resposta

### Sucesso

```json
{
  "success": true,
  "data": {
    // Dados da resposta
  }
}
```

### Erro

```json
{
  "success": false,
  "error": {
    "code": "INVALID_CREDENTIALS",
    "message": "Email ou senha incorretos",
    "details": {}
  }
}
```

## Códigos de Status HTTP

| Código | Significado |
|--------|-------------|
| 200 | OK - Sucesso |
| 201 | Created - Recurso criado |
| 204 | No Content - Sucesso sem conteúdo |
| 400 | Bad Request - Requisição inválida |
| 401 | Unauthorized - Não autenticado |
| 403 | Forbidden - Sem permissão |
| 404 | Not Found - Recurso não encontrado |
| 429 | Too Many Requests - Rate limit excedido |
| 500 | Internal Server Error - Erro no servidor |

## Rate Limiting

Limites por endpoint:

- **Autenticação**: 5 requisições/minuto
- **Leitura**: 100 requisições/minuto
- **Escrita**: 30 requisições/minuto

Headers de rate limit:
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1609459200
```

## Paginação

Endpoints que retornam listas usam paginação:

```bash
GET /api/games?page=2&limit=20
```

Resposta:
```json
{
  "success": true,
  "data": [...],
  "pagination": {
    "page": 2,
    "limit": 20,
    "total": 150,
    "totalPages": 8,
    "hasNext": true,
    "hasPrev": true
  }
}
```

## Filtros e Ordenação

### Filtros

```bash
GET /api/games?status=finished&result=1-0
```

### Ordenação

```bash
GET /api/games?sort=-created_at  # DESC
GET /api/games?sort=rating        # ASC
```

### Busca

```bash
GET /api/users?search=jogador
```

## Versionamento

A API usa versionamento via URL:

- Atual: `/v1/`
- Próxima: `/v2/` (quando disponível)

Versões antigas são mantidas por pelo menos 6 meses após nova versão.

## SDKs e Bibliotecas

### JavaScript/TypeScript

```bash
npm install @oitoporoito/sdk
```

```javascript
import { OitoPorOito } from '@oitoporoito/sdk';

const client = new OitoPorOito({
  apiKey: 'your-api-key',
  baseURL: 'https://api.oitoporoito.com/v1'
});

// Buscar perfil
const user = await client.users.me();

// Buscar partidas
const games = await client.games.list({ limit: 10 });
```

### Python

```bash
pip install oitoporoito
```

```python
from oitoporoito import Client

client = Client(api_key='your-api-key')

# Buscar perfil
user = client.users.me()

# Buscar partidas
games = client.games.list(limit=10)
```

## Endpoints Principais

### Autenticação

- `POST /auth/login` - Login
- `POST /auth/signup` - Cadastro
- `POST /auth/logout` - Logout
- `POST /auth/refresh` - Renovar token

[📖 Documentação completa](authentication.md)

### Usuários

- `GET /users/me` - Perfil atual
- `GET /users/:id` - Perfil por ID
- `PATCH /users/me` - Atualizar perfil
- `GET /users/search` - Buscar usuários


### Partidas

- `POST /games` - Criar partida
- `GET /games/:id` - Buscar partida
- `PATCH /games/:id/move` - Fazer movimento
- `POST /games/:id/resign` - Resignar
- `POST /games/:id/draw` - Oferecer empate

[📖 Documentação completa](games.md)

### Puzzles

- `GET /puzzles` - Listar puzzles
- `GET /puzzles/:id` - Buscar puzzle
- `POST /puzzles/:id/attempt` - Tentar resolver
- `GET /puzzles/daily` - Puzzle do dia

### Social

- `GET /friends` - Listar amigos
- `POST /friends/:id` - Adicionar amigo
- `DELETE /friends/:id` - Remover amigo
- `GET /clubs` - Listar clubes
- `POST /clubs` - Criar clube

## Webhooks

Configure webhooks para receber eventos em tempo real:

```javascript
POST /webhooks
{
  "url": "https://seu-site.com/webhook",
  "events": ["game.finished", "friend.request"],
  "secret": "seu-secret"
}
```

Eventos disponíveis:
- `game.started`
- `game.finished`
- `game.move`
- `friend.request`
- `friend.accepted`
- `club.invite`
- `tournament.started`

## Realtime (WebSocket)

Para atualizações em tempo real, use WebSocket:

```javascript
const ws = new WebSocket('wss://api.oitoporoito.com/realtime');

ws.onopen = () => {
  ws.send(JSON.stringify({
    type: 'subscribe',
    channel: 'game:123',
    token: 'seu-jwt-token'
  }));
};

ws.onmessage = (event) => {
  const data = JSON.parse(event.data);
  console.log('Nova jogada:', data);
};
```

## Erros Comuns

### 401 Unauthorized

```json
{
  "error": {
    "code": "UNAUTHORIZED",
    "message": "Token inválido ou expirado"
  }
}
```

**Solução:** Renovar token com `/auth/refresh`

### 429 Rate Limit

```json
{
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "Muitas requisições",
    "retryAfter": 60
  }
}
```

**Solução:** Aguardar antes de nova requisição

### 400 Validation Error

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Dados inválidos",
    "details": {
      "email": ["Email inválido"],
      "password": ["Mínimo 8 caracteres"]
    }
  }
}
```

## Ambientes

### Produção
```
https://api.oitoporoito.com/v1
```

### Staging
```
https://api-staging.oitoporoito.com/v1
```

### Desenvolvimento Local
```
http://localhost:3000/v1
```

## Recursos

- [Postman Collection](https://postman.oitoporoito.com)
- [API Playground](https://playground.oitoporoito.com)
- [Status Page](https://status.oitoporoito.com)
- [Changelog](../resources/changelog.md)

## Suporte

- 📧 Email: api@oitoporoito.com
- 💬 Discord: [OitoPorOito Community](https://discord.gg/oitoporoito)
- 🐛 Issues: [GitHub](https://github.com/Oito-Por-Oito/api/issues)

## Próximos Passos

<div class="grid cards" markdown>

- **[Autenticação](authentication.md)**
  
    Como autenticar e gerenciar sessões

- **[Partidas](games.md)**
  
    Endpoints de partidas de xadrez

- **[Changelog](../resources/changelog.md)**
  
    Histórico de mudanças

</div>
