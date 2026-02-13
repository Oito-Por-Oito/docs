# Games API

Gerenciamento de partidas de xadrez.

## Base URL

```
https://api.oitoporoito.com/v1/games
```

## Endpoints

### Listar Partidas

Obter lista de partidas.

**Endpoint:** `GET /games`

**Query Parameters:**

| Parâmetro | Tipo | Descrição |
|-----------|------|-----------|
| `status` | string | Filtrar por status: `active`, `finished`, `abandoned` |
| `player_id` | uuid | Filtrar por jogador específico |
| `time_control` | string | Filtrar por controle de tempo: `bullet`, `blitz`, `rapid`, `classical` |
| `page` | integer | Número da página (padrão: 1) |
| `limit` | integer | Itens por página (padrão: 20, máx: 100) |
| `sort` | string | Campo de ordenação: `created_at`, `updated_at` |
| `order` | string | Ordem: `asc`, `desc` (padrão: desc) |

**Request:**

```bash
curl -X GET "https://api.oitoporoito.com/v1/games?status=active&limit=10" \
  -H "Authorization: Bearer YOUR_TOKEN"
```

**Response:** `200 OK`

```json
{
  "success": true,
  "data": [
    {
      "id": "123e4567-e89b-12d3-a456-426614174000",
      "white_player": {
        "id": "user-123",
        "username": "GrandMaster2024",
        "rating": 2100,
        "avatar_url": "https://..."
      },
      "black_player": {
        "id": "user-456",
        "username": "ChessNinja",
        "rating": 2050,
        "avatar_url": "https://..."
      },
      "status": "active",
      "time_control": "blitz",
      "initial_time": 300,
      "increment": 3,
      "current_turn": "white",
      "move_count": 12,
      "fen": "rnbqkb1r/pppppppp/5n2/8/4P3/8/PPPP1PPP/RNBQKBNR w KQkq - 1 3",
      "pgn": "1. e4 Nf6 2. e5 Nd5 ...",
      "white_time_remaining": 245,
      "black_time_remaining": 268,
      "created_at": "2024-02-13T14:30:00Z",
      "updated_at": "2024-02-13T14:38:22Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 156,
    "total_pages": 16
  }
}
```

---

### Obter Partida

Detalhes de uma partida específica.

**Endpoint:** `GET /games/:id`

**Request:**

```bash
curl -X GET "https://api.oitoporoito.com/v1/games/123e4567-e89b-12d3-a456-426614174000" \
  -H "Authorization: Bearer YOUR_TOKEN"
```

**Response:** `200 OK`

```json
{
  "success": true,
  "data": {
    "id": "123e4567-e89b-12d3-a456-426614174000",
    "white_player": {
      "id": "user-123",
      "username": "GrandMaster2024",
      "rating": 2100,
      "country": "BR",
      "avatar_url": "https://..."
    },
    "black_player": {
      "id": "user-456",
      "username": "ChessNinja",
      "rating": 2050,
      "country": "PT",
      "avatar_url": "https://..."
    },
    "status": "active",
    "result": null,
    "winner": null,
    "termination": null,
    "time_control": "blitz",
    "initial_time": 300,
    "increment": 3,
    "rated": true,
    "current_turn": "white",
    "move_count": 12,
    "fen": "rnbqkb1r/pppppppp/5n2/8/4P3/8/PPPP1PPP/RNBQKBNR w KQkq - 1 3",
    "pgn": "1. e4 Nf6 2. e5 Nd5 3. d4 d6 ...",
    "moves": [
      {
        "number": 1,
        "white": "e4",
        "black": "Nf6",
        "white_time": 300,
        "black_time": 297
      },
      {
        "number": 2,
        "white": "e5",
        "black": "Nd5",
        "white_time": 298,
        "black_time": 294
      }
    ],
    "white_time_remaining": 245,
    "black_time_remaining": 268,
    "last_move_at": "2024-02-13T14:38:22Z",
    "created_at": "2024-02-13T14:30:00Z",
    "updated_at": "2024-02-13T14:38:22Z"
  }
}
```

**Erros:**

- `404 Not Found`: Partida não encontrada

---

### Criar Partida

Criar nova partida (desafio ou matchmaking).

**Endpoint:** `POST /games`

**Body:**

```json
{
  "type": "challenge",
  "opponent_id": "user-456",
  "time_control": "blitz",
  "initial_time": 300,
  "increment": 3,
  "rated": true,
  "color": "random"
}
```

**Campos:**

| Campo | Tipo | Obrigatório | Descrição |
|-------|------|-------------|-----------|
| `type` | string | Sim | `challenge` ou `matchmaking` |
| `opponent_id` | uuid | Condicional | Obrigatório se `type=challenge` |
| `time_control` | string | Sim | `bullet`, `blitz`, `rapid`, `classical` |
| `initial_time` | integer | Sim | Tempo inicial em segundos |
| `increment` | integer | Sim | Incremento por jogada em segundos |
| `rated` | boolean | Não | Se partida é ranqueada (padrão: true) |
| `color` | string | Não | `white`, `black`, `random` (padrão: random) |

**Request:**

```bash
curl -X POST "https://api.oitoporoito.com/v1/games" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "type": "challenge",
    "opponent_id": "user-456",
    "time_control": "blitz",
    "initial_time": 300,
    "increment": 3,
    "rated": true
  }'
```

**Response:** `201 Created`

```json
{
  "success": true,
  "data": {
    "id": "123e4567-e89b-12d3-a456-426614174000",
    "status": "pending",
    "expires_at": "2024-02-13T14:35:00Z",
    "invite_url": "https://oitoporoito.com/game/123e4567"
  }
}
```

**Erros:**

- `400 Bad Request`: Dados inválidos
- `404 Not Found`: Oponente não encontrado
- `409 Conflict`: Jogador já está em partida

---

### Fazer Movimento

Executar um movimento em uma partida ativa.

**Endpoint:** `POST /games/:id/moves`

**Body:**

```json
{
  "from": "e2",
  "to": "e4",
  "promotion": null
}
```

**Campos:**

| Campo | Tipo | Obrigatório | Descrição |
|-------|------|-------------|-----------|
| `from` | string | Sim | Casa de origem (ex: "e2") |
| `to` | string | Sim | Casa de destino (ex: "e4") |
| `promotion` | string | Condicional | Peça de promoção: `q`, `r`, `b`, `n` |

**Request:**

```bash
curl -X POST "https://api.oitoporoito.com/v1/games/123e4567-e89b-12d3-a456-426614174000/moves" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "from": "e2",
    "to": "e4"
  }'
```

**Response:** `200 OK`

```json
{
  "success": true,
  "data": {
    "move": {
      "from": "e2",
      "to": "e4",
      "san": "e4",
      "piece": "p",
      "captured": null,
      "promotion": null,
      "flags": ""
    },
    "game": {
      "status": "active",
      "fen": "rnbqkbnr/pppppppp/8/8/4P3/8/PPPP1PPP/RNBQKBNR b KQkq e3 0 1",
      "current_turn": "black",
      "move_count": 1,
      "white_time_remaining": 298,
      "black_time_remaining": 300,
      "in_check": false,
      "in_checkmate": false,
      "in_stalemate": false,
      "in_draw": false
    }
  }
}
```

**Erros:**

- `400 Bad Request`: Movimento inválido
- `403 Forbidden`: Não é sua vez
- `404 Not Found`: Partida não encontrada
- `409 Conflict`: Partida não está ativa

---

### Resignar

Desistir de uma partida.

**Endpoint:** `POST /games/:id/resign`

**Request:**

```bash
curl -X POST "https://api.oitoporoito.com/v1/games/123e4567-e89b-12d3-a456-426614174000/resign" \
  -H "Authorization: Bearer YOUR_TOKEN"
```

**Response:** `200 OK`

```json
{
  "success": true,
  "data": {
    "status": "finished",
    "result": "0-1",
    "winner": "black",
    "termination": "resignation",
    "rating_changes": {
      "white": -12,
      "black": +12
    }
  }
}
```

---

### Oferecer Empate

Propor empate ao oponente.

**Endpoint:** `POST /games/:id/draw`

**Request:**

```bash
curl -X POST "https://api.oitoporoito.com/v1/games/123e4567-e89b-12d3-a456-426614174000/draw" \
  -H "Authorization: Bearer YOUR_TOKEN"
```

**Response:** `200 OK`

```json
{
  "success": true,
  "data": {
    "draw_offer": {
      "id": "offer-123",
      "offered_by": "user-123",
      "status": "pending",
      "expires_at": "2024-02-13T14:40:00Z"
    }
  }
}
```

---

### Responder Proposta de Empate

Aceitar ou recusar proposta.

**Endpoint:** `POST /games/:id/draw/:offer_id`

**Body:**

```json
{
  "accept": true
}
```

**Request:**

```bash
curl -X POST "https://api.oitoporoito.com/v1/games/123e4567/draw/offer-123" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{ "accept": true }'
```

**Response:** `200 OK`

```json
{
  "success": true,
  "data": {
    "status": "finished",
    "result": "1/2-1/2",
    "winner": null,
    "termination": "agreement"
  }
}
```

---

### Análise de Partida

Obter análise de uma partida finalizada.

**Endpoint:** `GET /games/:id/analysis`

**Request:**

```bash
curl -X GET "https://api.oitoporoito.com/v1/games/123e4567/analysis" \
  -H "Authorization: Bearer YOUR_TOKEN"
```

**Response:** `200 OK`

```json
{
  "success": true,
  "data": {
    "game_id": "123e4567",
    "analyzed_at": "2024-02-13T15:00:00Z",
    "engine": "Stockfish 16",
    "depth": 20,
    "accuracy": {
      "white": 87.5,
      "black": 82.3
    },
    "mistakes": {
      "white": 2,
      "black": 4
    },
    "blunders": {
      "white": 0,
      "black": 1
    },
    "moves": [
      {
        "move_number": 1,
        "white": {
          "san": "e4",
          "evaluation": 0.3,
          "best_move": "e4",
          "classification": "excellent"
        },
        "black": {
          "san": "e5",
          "evaluation": 0.2,
          "best_move": "c5",
          "classification": "good"
        }
      }
    ],
    "opening": {
      "name": "Italian Game",
      "eco": "C50",
      "moves": "1. e4 e5 2. Nf3 Nc6 3. Bc4"
    }
  }
}
```

## Objetos

### Game Object

```typescript
interface Game {
  id: string;
  white_player: Player;
  black_player: Player;
  status: 'pending' | 'active' | 'finished' | 'abandoned';
  result: string | null; // "1-0", "0-1", "1/2-1/2"
  winner: 'white' | 'black' | null;
  termination: 'checkmate' | 'resignation' | 'timeout' | 'agreement' | 'stalemate' | null;
  time_control: 'bullet' | 'blitz' | 'rapid' | 'classical';
  initial_time: number;
  increment: number;
  rated: boolean;
  current_turn: 'white' | 'black';
  move_count: number;
  fen: string;
  pgn: string;
  white_time_remaining: number;
  black_time_remaining: number;
  created_at: string;
  updated_at: string;
}
```

### Move Object

```typescript
interface Move {
  from: string;
  to: string;
  san: string;
  piece: string;
  captured: string | null;
  promotion: string | null;
  flags: string;
}
```

## Exemplos

### JavaScript/TypeScript

```javascript
// Criar partida
const createGame = async () => {
  const response = await fetch('https://api.oitoporoito.com/v1/games', {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${token}`,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      type: 'matchmaking',
      time_control: 'blitz',
      initial_time: 300,
      increment: 3,
      rated: true
    })
  });
  
  const data = await response.json();
  return data.data;
};

// Fazer movimento
const makeMove = async (gameId, from, to) => {
  const response = await fetch(
    `https://api.oitoporoito.com/v1/games/${gameId}/moves`,
    {
      method: 'POST',
      headers: {
        'Authorization': `Bearer ${token}`,
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({ from, to })
    }
  );
  
  const data = await response.json();
  return data.data;
};
```

### Python

```python
import requests

# Criar partida
def create_game(token):
    response = requests.post(
        'https://api.oitoporoito.com/v1/games',
        headers={
            'Authorization': f'Bearer {token}',
            'Content-Type': 'application/json'
        },
        json={
            'type': 'matchmaking',
            'time_control': 'blitz',
            'initial_time': 300,
            'increment': 3,
            'rated': True
        }
    )
    
    return response.json()['data']

# Fazer movimento
def make_move(token, game_id, from_sq, to_sq):
    response = requests.post(
        f'https://api.oitoporoito.com/v1/games/{game_id}/moves',
        headers={
            'Authorization': f'Bearer {token}',
            'Content-Type': 'application/json'
        },
        json={
            'from': from_sq,
            'to': to_sq
        }
    )
    
    return response.json()['data']
```

## Rate Limiting

- **Matchmaking**: 10 requisições / minuto
- **Create Game**: 5 requisições / minuto  
- **Make Move**: 100 requisições / minuto
- **Get Game**: 60 requisições / minuto

## WebSocket

Para atualizações em tempo real, use WebSocket:

```javascript
const ws = new WebSocket('wss://api.oitoporoito.com/v1/games/123e4567/stream');

ws.onmessage = (event) => {
  const data = JSON.parse(event.data);
  
  switch (data.type) {
    case 'move':
      console.log('Novo movimento:', data.move);
      break;
    case 'time_update':
      console.log('Tempo atualizado:', data.times);
      break;
    case 'game_end':
      console.log('Partida finalizada:', data.result);
      break;
  }
};
```

## Próximos Passos

- [Authentication API](authentication.md)
- [API Introduction](introduction.md)
