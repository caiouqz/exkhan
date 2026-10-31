# EXKHAN

**by [caioopj](https://github.com/caiouqz)**

Uma ferramenta experimental para auxiliar em atividades da Khan Academy. O Exkhan reúne um painel de cálculos, modo automático, Answer Revealer com IA e um recurso experimental de substituição de questões.

> O projeto não é afiliado à Khan Academy ou ao OpenRouter. Não há garantia de acerto ou de compatibilidade com todas as atividades. A automação pode afetar o progresso e os resultados registrados na conta.

## Instalar pelo bookmarklet

Um **bookmarklet** é um favorito que executa um pequeno código quando você clica nele.

1. No GitHub, crie um repositório **público** chamado `Exkhan` na conta `caiouqz`.
2. Envie este README e o arquivo `Exkhan.js` para a raiz do repositório, na branch `main`.
3. No Brave ou Chrome, adicione um favorito e edite-o: use **Exkhan** como nome e cole o código inteiro abaixo no campo **URL**, incluindo `javascript:`.
4. Abra a Khan Academy e clique no favorito. O painel deve aparecer após a tela de abertura.

```javascript
javascript:fetch('https://cdn.jsdelivr.net/gh/caiouqz/Exkhan@main/Exkhan.js').then(r=>{if(!r.ok)throw new Error('Não foi possível carregar o Exkhan: '+r.status);return r.text()}).then(code=>(0,eval)(code)).catch(e=>alert(e.message));
```

O endereço acima só funcionará depois que o arquivo for publicado exatamente nesse caminho. Se mudar o nome do repositório, da branch ou do arquivo, atualize também o favorito. A CDN pode demorar a refletir atualizações. Algumas páginas podem bloquear a execução de bookmarklets por suas políticas de segurança.

O favorito precisa ser acionado novamente após um recarregamento completo da página; ele não é uma extensão e não garante inicialização antes do carregamento das questões.

## Como usar

- **Calcular**: tenta resolver o formato de questão reconhecido.
- **Iniciar automático**: tenta seguir pelas questões suportadas; pode parar se não reconhecer o formato ou receber erro.
- **Answer Revealer**: solicita à IA uma sugestão para a questão aberta. Confira o resultado antes de usá-lo.
- **Spoof experimental**: tenta substituir questões. Pode falhar ou produzir uma questão visualmente alterada que não seja aceita pela plataforma.
- Arraste o cabeçalho para mover o painel. Use **Fechar** para fechar o painel.

O suporte depende do tipo de exercício e pode deixar de funcionar após mudanças no site.

## Configurar o OpenRouter

A IA é opcional para os cálculos locais, mas é necessária para o Answer Revealer e para o spoof experimental nesta versão.

1. Crie uma conta ou entre no [OpenRouter](https://openrouter.ai/).
2. Abra [API Keys](https://openrouter.ai/settings/keys) e crie uma chave.
3. No painel do Exkhan, abra **Chaves OpenRouter**, dê um nome à chave, cole-a e clique em **Salvar e selecionar**. Você pode guardar outras chaves e escolher a ativa na lista.
4. Se quiser usar o spoof, clique em **Ativar spoof experimental**. O Answer Revealer e as próximas solicitações do spoof usam a chave selecionada.
5. Para remover uma chave, selecione-a na gaveta e clique em **Remover selecionada**. Se ela foi exposta, revogue-a também no OpenRouter e crie outra.

Criar várias chaves não aumenta os limites de uso da conta.

O script usa o modelo `openrouter/free`, que direciona cada solicitação para um modelo gratuito disponível. Isso não garante disponibilidade nem respostas corretas. Modelos e políticas podem mudar.

### Limites, custos e erros

Na documentação do OpenRouter, os modelos gratuitos têm limites de uso; eles podem variar com a conta e mudar com o tempo. Consulte os [limites atualizados](https://openrouter.ai/docs/api/reference/limits) e sua [atividade](https://openrouter.ai/activity). O modelo gratuito pode ficar temporariamente indisponível; outros modelos, se configurados futuramente, podem ter custos.

- **HTTP 429**: limite de requisições ou capacidade temporariamente indisponível. Aguarde e confira a atividade e os limites da conta.
- **HTTP 401**: confira se a chave está correta e ativa.
- **HTTP 402**: confira créditos e limites na conta.
- **Campo de resposta não encontrado**: o formato da questão pode não ser suportado; tente o Answer Revealer ou responda manualmente.

## Privacidade e segurança

Quando a IA é usada, o conteúdo da questão e descrições disponíveis são enviados ao OpenRouter e ao provedor do modelo. Não envie conteúdo sensível. A chave fica no armazenamento do navegador acessível à página; outros scripts executados nesse contexto podem acessá-la. Evite usar uma chave com créditos elevados, configure limites no OpenRouter e nunca publique ou compartilhe a chave.

Um bookmarklet carregado da internet executa código com acesso à página aberta. Revise o código e use apenas versões em que você confia. O link acima carrega a branch `main`, que pode mudar com o tempo.
