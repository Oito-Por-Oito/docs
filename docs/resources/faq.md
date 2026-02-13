# FAQ - Perguntas Frequentes

Respostas para as perguntas mais comuns sobre o OitoPorOito.

## Geral

### O que é o OitoPorOito?

OitoPorOito é uma plataforma open-source completa de xadrez online. Oferecemos partidas, puzzles, aprendizado, recursos sociais e muito mais - tudo gratuito.

### O OitoPorOito é realmente grátis?

Sim! O OitoPorOito é 100% gratuito e open-source. Não há planos pagos, anúncios ou paywalls.

### Como o projeto se sustenta?

O projeto é mantido por contribuidores voluntários e doações da comunidade. Veja [FUNDING.yml](https://github.com/Oito-Por-Oito/.github/blob/main/FUNDING.yml) para apoiar.

### Posso usar offline?

Parcialmente. Após carregar uma vez, o Stockfish funciona offline. Mas partidas online e sincronização requerem internet.

## Conta e Perfil

### Como criar uma conta?

Veja nosso [guia de criação de conta](../user-guide/creating-account.md).

### Posso mudar meu username?

Sim, uma vez a cada 30 dias em Configurações > Perfil.

### Como deleto minha conta?

Configurações > Conta > Excluir Conta. **Atenção**: ação irreversível após 30 dias.

### Esqueci minha senha

Use "Esqueci minha senha" na tela de login. Você receberá um email de recuperação.

### Posso ter múltiplas contas?

Não. Múltiplas contas violam os [Termos de Uso](https://github.com/Oito-Por-Oito/.github/blob/main/legal/LICENSE.md) e podem resultar em banimento.

## Jogabilidade

### Como funciona o matchmaking?

O sistema pareia jogadores com rating similar (±200 pontos) que buscam o mesmo tempo de jogo.

### Por que não encontro oponentes?

- Horário com poucos jogadores online
- Faixa de rating muito restrita
- Modo de jogo pouco popular

**Solução**: Expanda filtros ou jogue em horários de pico.

### O que é rating provisório?

Suas primeiras 20 partidas têm rating marcado com `?`. O sistema está calibrando seu nível.

### Como aumentar meu rating?

- Resolva puzzles diariamente (melhora táticas)
- Analise suas partidas (aprenda com erros)
- Estude aberturas  (melhores primeiros movimentos)
- Jogue regularmente (consistência)

### Posso jogar contra o computador sem afetar rating?

Sim! Partidas vs computador não afetam seu rating online.

## Partidas

### Como funciona o relógio?

- **X+0**: X minutos totais, sem incremento
- **X+Y**: X minutos iniciais, ganha Y segundos por lance

Exemplo: 10+5 = 10 minutos + 5 segundos de bônus por movimento

### O que acontece se eu desconectar?

- Sistema aguarda 30 segundos
- Adiciona tempo extra (até 30s)
- Se não voltar, perde por abandono

### Posso desfazer movimento?

Não em partidas ranqueadas. Apenas vs computador no modo prática.

### Como ofereço empate?

Clique no botão "Empate" durante sua vez. Oponente pode aceitar ou recusar.

### O que é stalemate?

Empate onde o rei não está em xeque, mas não há movimentos legais disponíveis.

## Puzzles

### Como funcionam os puzzles?

São posições reais de partidas onde você deve encontrar o melhor lance (geralmente tático).

### Por que meu rating de puzzles é diferente do de partidas?

São sistemas separados. Puzzle rating mede habilidade tática; partida rating mede jogo completo.

### Posso pular puzzles difíceis?

Não. Puzzles são apresentados baseados no seu rating atual. Resolver consistentemente aumenta a dificuldade.

### Quantos puzzles posso fazer por dia?

Ilimitado! Quanto mais fizer, melhor.

## Técnico

### Quais navegadores são suportados?

- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

### Funciona em mobile?

Sim! A plataforma é totalmente responsiva e otimizada para mobile/tablet.

### Por que o Stockfish é lento?

Stockfish roda no seu dispositivo. Desempenho depende de:
- CPU do dispositivo
- Número de threads configurado
- Profundidade de análise

### Como melhorar performance?

- Use navegador moderno
- Feche abas desnecessárias
- Reduza profundidade do Stockfish
- Desative animações (Configurações)

## Segurança e Fair Play

### O que é considerado trapaça?

- 🚫 Uso de engines durante partidas
- 🚫 Conta compartilhada
- 🚫 Sandbagging (perder de propósito)
- 🚫 Uso de assistentes (opening books, tablebases)

### Como o sistema detecta trapaça?

- Análise estatística de movimentos
- Correlação com engines
- Padrões de tempo suspeitos
- Reports da comunidade

### O que acontece se eu for pego?

1ª vez: Aviso + suspensão temporária (3-7 dias)
2ª vez: Suspensão longa (30 dias)
3ª vez: Banimento permanente

### Como reporto jogador suspeito?

Durante ou após partida: Menu (⋮) > Reportar > Selecione motivo

## Desenvolvimento e Contribuição

### Como contribuo com código?

Veja nosso [guia de contribuição](../contributing/how-to-contribute.md).

### Preciso saber programar?

Não! Você pode contribuir com:
- Documentação
- Traduções
- Testes
- Design
- Reportar bugs

### Onde reporto bugs?

[GitHub Issues](https://github.com/Oito-Por-Oito/frontend/issues) com template de bug report.

### Como sugiro features?

[GitHub Issues](https://github.com/Oito-Por-Oito/frontend/issues) com template de feature request.

## Legal

### Qual a licença do projeto?

[MIT License](https://github.com/Oito-Por-Oito/.github/blob/main/legal/LICENSE.md) - open-source e permissiva.

### Posso usar o código no meu projeto?

Sim! Respeitando os termos da licença MIT.

### Meus dados são privados?

Sim. Leia nossa política de privacidade. Não vendemos dados.

### Como faço GDPR request?

Email: privacy@oitoporoito.com

## Recursos

### Onde aprendo xadrez?

- Seção [Aprender](../user-guide/learning.md) na plataforma
- [Chess.com Learn](https://www.chess.com/learn)
- [Lichess Practice](https://lichess.org/practice)

### Onde encontro a comunidade?

- [Discord](https://discord.gg/oitoporoito)
- [GitHub Discussions](https://github.com/Oito-Por-Oito/discussions)
- [Fórum](../user-guide/social-features.md) na plataforma

### Como fico atualizado?

- ⭐ Star no [GitHub](https://github.com/Oito-Por-Oito)
- 📰 [Changelog](changelog.md)
- 🐦 Twitter/X: @OitoPorOito (se existir)

## Problemas Comuns

### "Email não confirmado"

Verifique spam/lixo eletrônico. Reenvie email em Login > Reenviar confirmação.

### "Movimento inválido"

- Verifique se é sua vez
- Peça pode estar pinada ao rei
- Movimento pode violar regras (ex: roque através de xeque)

### "Não consigo fazer login"

- Verifique email/username e senha
- Tente recuperar senha
- Limpe cache do navegador
- Contate suporte: suporte@oitoporoito.com

### Página não carrega

- Verifique conexão internet
- Limpe cache: Ctrl+Shift+R (Windows) / Cmd+Shift+R (Mac)
- Tente navegador diferente
- Verifique [status da plataforma](https://status.oitoporoito.com)

## Suporte

Não encontrou sua resposta?

- 📖 [Documentação Completa](../index.md)
- 💬 [Discord Community](https://discord.gg/oitoporoito)
- 📧 Email: suporte@oitoporoito.com
- 🐛 [Report Issue](https://github.com/Oito-Por-Oito/frontend/issues)

---

**Última atualização**: Janeiro 2024
