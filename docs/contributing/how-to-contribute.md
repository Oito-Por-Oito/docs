# Como Contribuir

Obrigado por considerar contribuir com o OitoPorOito! Este guia irá ajudá-lo a começar.

## Código de Conduta

Ao participar deste projeto, você concorda em seguir nosso [Código de Conduta](code-of-conduct.md).

## Formas de Contribuir

Existem várias maneiras de contribuir:

### 💻 Código
- Implementar novas funcionalidades
- Corrigir bugs
- Melhorar performance
- Refatorar código
- Escrever testes

### 📖 Documentação
- Melhorar docs existentes
- Adicionar exemplos
- Corrigir typos
- Traduzir conteúdo

### 🎨 Design
- Melhorar UI/UX
- Criar assets (ícones, ilustrações)
- Propor novos temas
- Acessibilidade

### 🐛 Reportar Bugs
- Abrir issues detalhadas
- Ajudar a reproduzir bugs
- Testar correções

### 💡 Sugestões
- Propor novas funcionalidades
- Melhorias de usabilidade
- Feedback geral

### 👥 Comunidade
- Responder perguntas
- Ajudar outros usuários
- Compartilhar conhecimento

## Primeiros Passos

### 1. Fork o Repositório

```bash
# Via GitHub UI, clique em "Fork"
# Ou via CLI:
gh repo fork Oito-Por-Oito/frontend
```

### 2. Clone seu Fork

```bash
git clone https://github.com/seu-usuario/frontend.git
cd frontend
```

### 3. Configure os Remotes

```bash
# Adicione o upstream
git remote add upstream https://github.com/Oito-Por-Oito/frontend.git

# Verifique
git remote -v
```

### 4. Instale Dependências

```bash
npm install
```

### 5. Crie uma Branch

```bash
# Para features
git checkout -b feature/nome-da-feature

# Para bugfixes
git checkout -b fix/descricao-do-bug

# Para docs
git checkout -b docs/descricao-melhoria
```

## Workflow

### 1. Mantenha sua Fork Atualizada

```bash
# Busque mudanças do upstream
git fetch upstream

# Merge na sua branchlocal
git merge upstream/main
```

### 2. Faça suas Mudanças

Siga nosso [Guia de Estilo](style-guide.md):

- ✅ Código limpo e legível
- ✅ Comentários quando necessário
- ✅ Testes para novas funcionalidades
- ✅ Documentação atualizada

### 3. Commit suas Mudanças

Use [Conventional Commits](https://www.conventionalcommits.org/):

```bash
# Feature
git commit -m "feat: adiciona modo de jogo personalizado"

# Bugfix
git commit -m "fix: corrige movimento de peão en passant"

# Docs
git commit -m "docs: atualiza guia de instalação"

# Style
git commit -m "style: formata componente ChessBoard"

# Refactor
git commit -m "refactor: simplifica lógica de validação"

# Test
git commit -m "test: adiciona testes para useAuth hook"
```

**Tipos de commit:**
- `feat`: Nova funcionalidade
- `fix`: Correção de bug
- `docs`: Documentação
- `style`: Formatação (não afeta código)
- `refactor`: Refatoração
- `test`: Testes
- `chore`: Tarefas gerais (dependências, config)
- `perf`: Performance

### 4. Push para seu Fork

```bash
git push origin feature/nome-da-feature
```

### 5. Abra um Pull Request

1. Vá para seu fork no GitHub
2. Clique em "Compare & pull request"
3. Preencha o template de PR
4. Aguarde review

## Pull Request Guidelines

### Template

```markdown
## Descrição
[Descreva o que foi feito]

## Tipo de Mudança
- [ ] 🐛 Bugfix
- [ ] ✨ Nova feature
- [ ] 📖 Documentação
- [ ] 🎨 Estilo/UI
- [ ] ♻️ Refactor

## Como Testar
1. Clone o branch
2. Execute `npm install`
3. Execute `npm run dev`
4. Teste X, Y, Z

## Screenshots (se aplicável)
[Cole screenshots]

## Checklist
- [ ] Código segue guia de estilo
- [ ] Self-review realizado
- [ ] Comentários adicionados
- [ ] Documentação atualizada
- [ ] Testes passam
- [ ] Sem warnings no console
```

### Boas Práticas

✅ **Um PR = Uma funcionalidade/correção**
- Mantenha PRs focados
- Mais fácil de revisar
- Mais rápido para mergear

✅ **Descrição Clara**
- Explique o problema
- Descreva a solução
- Adicione screenshots/gifs

✅ **Commits Atômicos**
- Um commit = Uma mudança lógica
- Facilita o histórico

✅ **Testes**
- Adicione testes para novos recursos
- Garanta que testes existentes passam

✅ **Documentação**
- Atualize docs relevantes
- Adicione JSDoc em funções

## Processo de Review

### O que esperar

1. **Review automatizado**: CI/CD roda testes
2. **Review por pares**: Mantainer revisa código
3. **Feedback**: Podem ser solicitadas mudanças
4. **Aprovação**: Após ajustes, PR é aprovado
5. **Merge**: Mantainer faz merge

### Tempo de Resposta

- **Issues**: 1-3 dias
- **PRs simples**: 2-5 dias
- **PRs complexos**: 1-2 semanas

### Revisões Solicitadas

Se mudanças forem solicitadas:

```bash
# Faça as mudanças
git add .
git commit -m "fix: ajustes conforme review"
git push origin feature/nome-da-feature
```

PR é automaticamente atualizado.

## Encontrando Issues para Contribuir

### Labels Úteis

- 🟢 `good first issue`: Bom para iniciantes
- 🟡 `help wanted`: Ajuda é bem-vinda
- 🔴 `bug`: Bugs a corrigir
- 🔵 `enhancement`: Melhorias
- 🟣 `documentation`: Docs

### Filtros

```
# Issues boas para iniciantes
label:"good first issue" is:open

# Bugs
label:bug is:open

# Ajuda necessária
label:"help wanted" is:open
```

## Reportar Bugs

Use nosso [template de bug](https://github.com/Oito-Por-Oito/.github/blob/main/ISSUE_TEMPLATE/bug_report.yml):

### Informações Necessárias

- **Descrição**: O que aconteceu?
- **Passos para Reproduzir**: Como reproduzir o bug?
- **Comportamento Esperado**: O que deveria acontecer?
- **Screenshots**: Se aplicável
- **Ambiente**:
  - OS: Windows/Mac/Linux
  - Browser: Chrome/Firefox/Safari
  - Versão: 1.0.0

### Exemplo

```markdown
**Descrição**
Não consigo fazer promoção de peão para cavalo

**Passos**
1. Iniciar partida
2. Mover peão até a última fila
3. Tentar selecionar cavalo
4. Somente Rainha é promovida

**Esperado**
Deveria mostrar opções: Rainha, Torre, Bispo, Cavalo

**Ambiente**
- OS: Windows 11
- Browser: Chrome 120
- Versão: v0.5.2
```

## Sugerir Features

Use nosso [template de feature](https://github.com/Oito-Por-Oito/.github/blob/main/ISSUE_TEMPLATE/feature_request.yml):

### Estrutura

```markdown
**Problema a Resolver**
[Qual problema esta feature resolve?]

**Solução Proposta**
[Como você imagina que funcione?]

**Alternativas Consideradas**
[Outras formas de resolver?]

**Informações Adicionais**
[Contexto extra, mockups, etc.]
```

## Desenvolvimento

### Estrutura de Branch

```
main (produção)
  ├── develop (desenvolvimento)
  │   ├── feature/nova-funcionalidade
  │   ├── fix/correcao-bug
  │   └── docs/documentacao
  └── hotfix/urgente
```

### Commits Significativos

❌ **Ruim:**
```bash
git commit -m "mudanças"
git commit -m "fix"
git commit -m "atualização"
```

✅ **Bom:**
```bash
git commit -m "feat(chess): adiciona validação de roque"
git commit -m "fix(puzzle): corrige cálculo de rating"
git commit -m "docs(api): atualiza endpoint de autenticação"
```

### Testes

```bash
# Rodar todos os testes
npm test

# Modo watch
npm test:watch

# Coverage
npm test:coverage
```

Garanta que:
- ✅ Todos os testes passam
- ✅ Coverage não diminui
- ✅ Novos recursos têm testes

### Linting

```bash
# Verificar
npm run lint

# Corrigir automaticamente
npm run lint:fix
```

## Comunicação

### Discord

Junte-se ao nosso [Discord](https://discord.gg/oitoporoito):
- #contribuidores
- #dev-chat
- #help

### GitHub Discussions

Para discussões mais longas:
[github.com/Oito-Por-Oito/discussions](https://github.com/Oito-Por-Oito/discussions)

### Email

Para assuntos privados:
dev@oitoporoito.com

## Reconhecimento

Todos os contribuidores são:

- ✨ Listados em [CONTRIBUTORS.md](https://github.com/Oito-Por-Oito/.github/blob/main/profile/CONTRIBUTORS.md)
- 🎖️ Recebem badge de contribuidor
- 🙏 Mencionados nos releases

## Licença

Ao contribuir, você concorda que suas contribuições serão licenciadas sob a mesma [licença do projeto](https://github.com/Oito-Por-Oito/.github/blob/main/legal/LICENSE.md).

## Próximos Passos

- 📖 [Guia de Estilo](style-guide.md)
- 🔍 [Processo de Review](review-process.md)
- ⚖️ [Código de Conduta](code-of-conduct.md)

---

**Obrigado por contribuir! 🎉**
