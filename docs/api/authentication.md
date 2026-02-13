# API - Autenticação

Documentação completa dos endpoints de autenticação.

## Visão Geral

A autenticação é gerenciada pelo **Supabase Auth** e usa **JWT (JSON Web Tokens)**.

## Cadastro

### Criar Conta

```http
POST /auth/signup
Content-Type: application/json

{
  "email": "usuario@example.com",
  "password": "senha123",
  "username": "jogador123",
  "full_name": "João Silva"
}
```

**Resposta (201 Created):**
```json
{
  "success": true,
  "data": {
    "user": {
      "id": "123e4567-e89b-12d3-a456-426614174000",
      "email": "usuario@example.com",
      "username": "jogador123",
      "created_at": "2024-01-15T10:30:00Z"
    },
    "session": {
      "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
      "refresh_token": "v1.MXNlc3Npb25fdG9rZW4...",
      "expires_in": 3600
    }
  },
  "message": "Email de confirmação enviado"
}
```

## Login

### Email e Senha

```http
POST /auth/login
Content-Type: application/json

{
  "email": "usuario@example.com",
  "password": "senha123"
}
```

**Resposta (200 OK):**
```json
{
  "success": true,
  "data": {
    "user": {
      "id": "123e4567-e89b-12d3-a456-426614174000",
      "email": "usuario@example.com",
      "username": "jogador123",
      "avatar_url": "https://...",
      "rating": 1487
    },
    "session": {
      "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
      "refresh_token": "v1.MXNlc3Npb25fdG9rZW4...",
      "expires_in": 3600,
      "expires_at": "2024-01-15T11:30:00Z"
    }
  }
}
```

### OAuth2 (Em Breve)

```http
GET /auth/oauth/google
```

Redireciona para Google OAuth flow.

## Logout

```http
POST /auth/logout
Authorization: Bearer {access_token}
```

**Resposta (204 No Content)**

## Renovar Token

```http
POST /auth/refresh
Content-Type: application/json

{
  "refresh_token": "v1.MXNlc3Npb25fdG9rZW4..."
}
```

**Resposta (200 OK):**
```json
{
  "success": true,
  "data": {
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refresh_token": "v1.NEW_REFRESH_TOKEN...",
    "expires_in": 3600
  }
}
```

## Recuperação de Senha

### Solicitar Reset

```http
POST /auth/password/reset
Content-Type: application/json

{
  "email": "usuario@example.com"
}
```

**Resposta (200 OK):**
```json
{
  "success": true,
  "message": "Email de recuperação enviado"
}
```

### Confirmar Nova Senha

```http
POST /auth/password/update
Content-Type: application/json

{
  "token": "reset-token-from-email",
  "password": "nova-senha-123"
}
```

## Verificação de Email

### Confirmar Email

```http
POST /auth/verify
Content-Type: application/json

{
  "token": "verification-token"
}
```

### Reenviar Email

```http
POST /auth/verify/resend
Content-Type: application/json

{
  "email": "usuario@example.com"
}
```

## Validações

### Email
- ✅ Formato válido
- ✅ Não pode estar em uso
- ✅ Domínio deve existir

### Senha
- ✅ Mínimo 8 caracteres
- ✅ Pelo menos 1 letra
- ✅ Pelo menos 1 número
- 🔶 Recomendado: caracteres especiais

### Username
- ✅ 3-20 caracteres
- ✅ Apenas letras, números e underscores
- ✅ Único na plataforma
- ❌ Não pode conter palavras ofensivas

## Exemplo de Uso

### JavaScript

```javascript
// Login
const response = await fetch('https://api.oitoporoito.com/v1/auth/login', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    email: 'usuario@example.com',
    password: 'senha123'
  })
});

const { data } = await response.json();
const { access_token } = data.session;

// Usar token em requisições
const profile = await fetch('https://api.oitoporoito.com/v1/users/me', {
  headers: {
    'Authorization': `Bearer ${access_token}`
  }
});
```

### cURL

```bash
# Login
curl -X POST https://api.oitoporoito.com/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "usuario@example.com",
    "password": "senha123"
  }'

# Usar token
curl https://api.oitoporoito.com/v1/users/me \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
```

## Erros

### 400 Bad Request

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Dados inválidos",
    "details": {
      "email": ["Email inválido"],
      "password": ["Senha deve ter pelo menos 8 caracteres"]
    }
  }
}
```

### 401 Unauthorized

```json
{
  "success": false,
  "error": {
    "code": "INVALID_CREDENTIALS",
    "message": "Email ou senha incorretos"
  }
}
```

### 409 Conflict

```json
{
  "success": false,
  "error": {
    "code": "EMAIL_ALREADY_EXISTS",
    "message": "Este email já está cadastrado"
  }
}
```

### 429 Rate Limit

```json
{
  "success": false,
  "error": {
    "code": "TOO_MANY_ATTEMPTS",
    "message": "Muitas tentativas de login",
    "retryAfter": 300
  }
}
```

## Segurança

### Boas Práticas

✅ **Armazenar tokens de forma segura**
- Use `httpOnly` cookies
- Ou `localStorage` com cuidado

✅ **Renovar tokens antes de expirarem**
- Implemente auto-refresh

✅ **Fazer logout ao sair**
- Limpe todos os tokens

✅ **HTTPS obrigatório**
- Nunca use HTTP em produção

### Token JWT

Estrutura do JWT:

```
Header.Payload.Signature
```

Payload decodificado:
```json
{
  "sub": "123e4567-e89b-12d3-a456-426614174000",
  "email": "usuario@example.com",
  "role": "authenticated",
  "iat": 1705315200,
  "exp": 1705318800
}
```

### Expiração

- **Access Token**: 1 hora
- **Refresh Token**: 30 dias

## Próximos Passos

- [API Introduction →](introduction.md)
- [Partidas →](games.md)
