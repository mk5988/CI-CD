# Aula guiada de código e CI CD

Construa e opere um pipeline para o quiz Cloud e DevOps. Em cada etapa, registre a previsão ou a interpretação do resultado. O roteiro inclui 24 perguntas e evidências ligadas às suas execuções.

Duração sugerida de duas aulas de 120 minutos. Na primeira, use 10 minutos para apresentação da dinâmica e 110 minutos nas etapas 1 a 6. Na segunda, execute as etapas 7 a 12 em 120 minutos.

Identificação da equipe e integrantes

Repositório

Endereço publicado

## Uso do material

Extraia ARQUIVOS_ALUNO_CICD.zip. Execute os passos em ordem. Alterne quem navega, quem lê o código e quem registra as respostas. Os trechos do guia apoiam a leitura, e os arquivos indicados contêm o código completo para copiar. Registre hipóteses antes da ação quando a pergunta pedir previsão. Use o arquivo RESPOSTAS.md para entrega digital.

A aplicação usa HTML, CSS e JavaScript e testes nativos do Node.js. Os testes verificam a pontuação. A interface será conferida manualmente no endereço publicado. As contas e o navegador devem estar acessíveis antes da prática.

## Etapa 01 Preparação do projeto e das contas

Tempo sugerido de 15 minutos. Conceito de DevOps — Responsabilidade das ferramentas e controle das mudanças.

A equipe vai manter um quiz de três perguntas. Cada acerto vale um ponto. Uma atualização deve passar pelos testes antes de chegar ao endereço publicado.

1. Acesse github.com e entre na sua conta. Escolha um responsável pelo repositório da dupla. Os demais alternarão a navegação com ele ao longo da aula.
2. Extraia ARQUIVOS_ALUNO_CICD.zip. Localize projeto_inicial, etapa_05, workflows e RESPOSTAS.md. Deixe essa pasta aberta.
3. No GitHub, clique em + no topo e em New repository. Use o nome quiz-devops-aula, visibilidade Public e a opção Add a README file. Clique em Create repository.
4. Confira a aba Code e o seletor de branch. Padronize o exercício em main. Se a conta criou outro nome, peça ajuda para renomeá-lo antes de prosseguir.
5. Abra RESPOSTAS.md e preencha a identificação e o link do repositório.

**Conferência** O repositório público está aberto em Code, com README.md e branch main. O material está extraído no computador.

**Q01** Se queremos automatizar os testes e disponibilizar o site por um endereço, qual responsabilidade cabe ao GitHub Actions e qual cabe ao GitHub Pages?

Resposta

**Q02** Que problema operacional pode ocorrer se cada integrante publicar uma cópia diferente do código sem registrar a versão utilizada?

Resposta

**Evidência a registrar** Anote no arquivo de respostas o link do repositório e o nome da branch.


## Etapa 02 Código inicial e primeiro commit

Tempo sugerido de 20 minutos. Conceito de DevOps — Versionamento e estrutura do repositório.

Os arquivos do quiz precisam manter os caminhos esperados pelos testes e pela publicação.

1. Na aba Code, selecione Add file e Upload files.
2. Dentro da pasta projeto_inicial do material extraído, selecione a pasta site e o arquivo package.json. Arraste ambos para o upload, preservando a pasta site.
3. Confira os caminhos apresentados. O HTML deve aparecer em site/index.html e package.json deve ficar na raiz, ao lado de README.md.
4. Na confirmação, escreva Cria primeira versao do quiz. Faça commit diretamente na main e confirme em Commit changes.
5. Abra site/index.html, site/app.js e site/pontuacao.js. Localize o carregamento do módulo e a importação da função de pontuação.

```
<script type="module" src="./app.js"></script>

import { calcularPontuacao } from './pontuacao.js';
```

As duas linhas pertencem a arquivos diferentes. A primeira fica em site/index.html e a segunda em site/app.js. O kit contém os arquivos completos.

**Conferência** Na raiz aparecem README.md, package.json e a pasta site. Dentro de site há index.html, style.css, app.js e pontuacao.js.

**Q03** Que informação o commit registra para que outra pessoa consiga localizar esta entrega depois?

Resposta

**Q04** O que pode acontecer com nosso pipeline se site/index.html ficar dentro de projeto_inicial/site/index.html no repositório?

Resposta

**Evidência a registrar** Copie a mensagem e o identificador curto do commit. Para consultar, use o histórico de commits da aba Code ou History em um arquivo.


## Etapa 03 Mudança identificável e histórico

Tempo sugerido de 15 minutos. Conceito de DevOps — Rastreabilidade entre alterações e versões.

Você vai criar uma segunda versão para reconhecer a relação entre uma alteração e seu commit.

1. Em Code, abra site/index.html e clique no lápis para editar.
2. Localize o h1 e altere somente seu texto para Quiz Cloud e DevOps da equipe. Preserve as demais tags e atributos.
3. Clique em Commit changes, use a mensagem Personaliza titulo do quiz e confirme na main.
4. Abra History no arquivo ou o histórico de commits em Code. Compare este commit com Cria primeira versao do quiz.
5. Abra a alteração do novo commit e identifique a linha removida e a linha acrescentada.

```
<h1>Quiz Cloud e DevOps da equipe</h1>
```



**Conferência** O histórico contém as duas mensagens e identificadores diferentes. O novo commit mostra a alteração do título.

**Q05** Se uma execução futura apresentar um erro, por que devemos anotar o identificador do commit associado a ela?

Resposta

**Q06** A mudança do título já iniciou algum teste automático neste momento? O que ainda precisamos configurar?

Resposta

**Evidência a registrar** Registre o identificador do novo commit e descreva em uma frase a diferença entre as duas versões.


## Etapa 04 Regra de negócio que será protegida

Tempo sugerido de 15 minutos. Conceito de DevOps — Critério verificável de qualidade.

A função de pontuação transforma respostas em pontos. Os testes vão verificar essa regra de forma independente da navegação pela página.

1. Abra site/pontuacao.js no GitHub e leia a função abaixo. Os índices das alternativas começam em zero.
2. Acompanhe o exemplo respostas [0, 2, 3] e gabarito [0, 1, 2]. Compare uma posição por vez e registre o total esperado.
3. Abra site/app.js e localize a chamada calcularPontuacao. Observe de onde vêm os argumentos e como o resultado chega ao elemento resultado.
4. Registre a regra e os resultados esperados antes de criar os testes.

```
export function calcularPontuacao(respostas, gabarito) {
  let pontos = 0;
  for (let i = 0; i < gabarito.length; i++) {
    if (
      respostas[i] !== null &&
      respostas[i] !== undefined &&
      respostas[i] === gabarito[i]
    ) {
      pontos += 1;
    }
  }
  return pontos;
}
```



**Conferência** A equipe identifica a função usada pela interface e explica por que o exemplo produz um ponto.

**Q07** Por que executar testes sobre a mesma função utilizada pela interface ajuda a verificar a versão que vamos publicar?

Resposta

**Q08** Defina o resultado esperado para três acertos e para nenhuma resposta marcada. Qual regra sustenta sua previsão?

Resposta

**Evidência a registrar** Escreva no arquivo de respostas os dois resultados previstos e o caminho da função.


## Etapa 05 Testes automatizados e comando do projeto

Tempo sugerido de 20 minutos. Conceito de DevOps — Execução repetível das verificações.

Um comando registrado no projeto permitirá executar as mesmas verificações a cada alteração.

1. Na raiz do repositório, selecione Code, Add file e Create new file. Digite tests/pontuacao.test.js.
2. Abra etapa_05/tests/pontuacao.test.js no material extraído. Copie todo o conteúdo para o editor do GitHub.
3. Faça commit na main com a mensagem Adiciona testes da pontuacao.
4. Volte à raiz, abra package.json e clique no lápis. Substitua o conteúdo pelo arquivo etapa_05/package.json. Faça commit com a mensagem Configura comando de testes.
5. Confira os cinco testes e leia o exemplo abaixo. O primeiro argumento de assert.equal é o valor observado e o segundo é a expectativa.

```
test('tres respostas corretas somam tres pontos', () => {
  assert.equal(calcularPontuacao([0, 1, 2], [0, 1, 2]), 3);
});

// No package.json, scripts deve conter
// "test": "node --test"
```

Os comentários explicam o trecho. Use o package.json completo do arquivo de apoio, que é JSON válido.

**Conferência** tests/pontuacao.test.js está ao lado da pasta site. package.json contém type module e scripts.test com node --test.

**Q09** Qual é a sequência entre npm test, package.json e os arquivos de teste?

Resposta

**Q10** Se o runner executar zero testes e terminar sem erro, isso é evidência suficiente para liberar a versão? O que você conferiria?

Resposta

**Evidência a registrar** Registre os caminhos do arquivo de teste e do package.json e o comando definido para os testes.


## Etapa 06 Primeiro workflow de integração contínua

Tempo sugerido de 25 minutos. Conceito de DevOps — Pipeline definido como código.

O workflow descreve os eventos, o ambiente e os comandos que o GitHub executará.

1. Abra workflows/01_ci_testes.yml no material extraído. Leia os blocos on, jobs e steps. Preserve recuos feitos com espaços.
2. No GitHub, volte à raiz. Selecione Code, Add file e Create new file. Digite exatamente .github/workflows/ci-cd.yml.
3. Copie o conteúdo completo de 01_ci_testes.yml, incluindo a configuração do Node.js. Cole apenas o YAML no editor.
4. Antes de salvar, responda Q11. Depois faça commit na main com a mensagem Configura CI do quiz.
5. Confira na aba Code que o caminho termina em .github/workflows/ci-cd.yml.

```
on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  testes:
    name: Testar pontuacao
    runs-on: ubuntu-latest
```

Recorte para leitura. O workflow completo está em workflows/01_ci_testes.yml e precisa ser copiado integralmente.

**Conferência** Um único arquivo de workflow está ativo no caminho .github/workflows/ci-cd.yml. O commit na main pode iniciar a execução automaticamente.

**Q11** Preveja se o commit que cria esse YAML na main inicia o pipeline. Qual evento e qual filtro do arquivo justificam sua resposta?

Resposta

**Q12** Qual é a vantagem de registrar o workflow no mesmo histórico do código da aplicação?

Resposta

**Evidência a registrar** Registre o caminho do YAML e o identificador do commit que o criou.


## Etapa 07 Execução no Actions e leitura dos logs

Tempo sugerido de 15 minutos. Conceito de DevOps — Ambiente de execução e evidência observável.

Agora é preciso verificar qual revisão rodou, em qual ambiente e com qual resultado.

1. Abra Actions no repositório. Selecione CI do Quiz na lateral e a execução associada ao commit mais recente.
2. Confira branch main, evento push e identificador do commit. Compare com o histórico do código.
3. Clique em Testar pontuacao. Expanda Buscar codigo do repositorio, Preparar Node.js e Executar testes.
4. No log dos testes, localize os nomes dos cinco casos, o total, os aprovados e as falhas.
5. Volte à página do workflow CI do Quiz. Clique em Run workflow, selecione main e confirme. Identifique o disparo manual na nova execução.

```
- name: Preparar Node.js
  uses: actions/setup-node@v7
  with:
    node-version: '24'
    package-manager-cache: false

- name: Executar testes
  run: npm test
```



**Conferência** Os cinco testes passam e a execução manual também é localizada. A versão do Node.js utilizada está visível no passo de preparação.

**Q13** Por que configuramos a versão do Node.js no runner? No trecho, o que significam v7 e 24?

Resposta

**Q14** Que dados do log você registraria para comprovar que esta revisão foi verificada? Indique também a diferença entre uses e run.

Resposta

**Evidência a registrar** Cole os links da execução automática e da manual e o resumo real dos testes. Identifique o evento observado em cada uma.


## Etapa 08 Falha controlada e correção

Tempo sugerido de 25 minutos. Conceito de DevOps — Feedback rápido e diagnóstico.

Uma alteração intencional vai violar a regra de pontuação e produzir um resultado de teste reprovado.

1. Antes de editar, responda Q15. Depois abra Code, site/pontuacao.js e o lápis de edição.
2. Troque somente pontos += 1 por pontos += 2. Faça commit com a mensagem Demonstra falha na pontuacao.
3. Em Actions, abra a execução desse commit e o passo Executar testes. Registre o primeiro caso reprovado, esperado e recebido.
4. Restaure pontos += 1 e faça um novo commit com a mensagem Corrige pontuacao.
5. Abra a execução do commit de correção e confirme o resumo de cinco testes aprovados.

```
// Alteração intencional
pontos += 2;

// Correção
pontos += 1;
```



**Conferência** O histórico de execuções contém sucesso inicial, falha após a alteração e sucesso após a correção. A implementação entregue termina com um ponto por acerto.

**Q15** Antes de executar, quais dos cinco casos você prevê que falharão ao dobrar o ponto por acerto? Justifique.

Resposta

**Q16** Por que reexecutar a execução defeituosa não substitui fazer o commit da correção? Use os identificadores das execuções na explicação.

Resposta

**Evidência a registrar** Registre links das execuções com erro e corrigida. Copie esperado e recebido de pelo menos um teste reprovado.


## Etapa 09 Publicação condicionada e configuração do Pages

Tempo sugerido de 25 minutos. Conceito de DevOps — Dependência entre jobs e implantação contínua.

A mesma automação passará a publicar os arquivos após a aprovação dos testes.

1. No repositório, abra Settings, Pages e Build and deployment. Em Source, selecione GitHub Actions.
2. Abra workflows/02_ci_cd_pages.yml no material. Compare com a versão de testes e localize needs: testes no job publicar.
3. Em Code, abra .github/workflows/ci-cd.yml e clique no lápis. Substitua todo o conteúdo pelo modelo 02_ci_cd_pages.yml.
4. Confira a preservação dos recuos, path ./site, permissões e expressão da URL. Faça commit na main com a mensagem Adiciona publicacao automatica.
5. Observe em Actions a execução CI/CD do Quiz, com testes e publicação.

```
publicar:
  name: Publicar site
  needs: testes
  runs-on: ubuntu-latest
  permissions:
    contents: read
    pages: write
    id-token: write
```

Este trecho é parte do segundo job. O modelo completo inclui environment, checkout, configuração, upload e deploy.

**Conferência** O repositório tem um único ci-cd.yml ativo. O job publicar depende do ID testes e o Pages está configurado para receber o deploy do Actions.

**Q17** O que needs: testes exige antes de permitir o job publicar neste workflow? Por que o nome usado é testes?

Resposta

**Q18** Como a publicação automática deste exercício caracteriza implantação contínua? Como seria uma liberação com decisão humana após os testes?

Resposta

**Evidência a registrar** Registre o commit que alterou o workflow e copie a linha que conecta os jobs.


## Etapa 10 Artefato publicado e mudança visível

Tempo sugerido de 20 minutos. Conceito de DevOps — Empacotamento e verificação da implantação.

Vamos acompanhar os arquivos selecionados para publicação e conferir a aplicação no endereço real.

1. Na execução CI/CD do Quiz, confira o sucesso de Testar pontuacao e abra Publicar site.
2. Expanda Empacotar arquivos do site e Publicar no GitHub Pages. Localize o endereço no ambiente de publicação ou em Settings e Pages.
3. Abra o endereço. Responda todas as perguntas corretamente e depois tudo errado. Confira o botão Reiniciar.
4. Volte a Code, abra site/index.html e altere o texto do h1 para Quiz Cloud e DevOps versao 2. Faça commit com a mensagem Atualiza titulo publicado.
5. Acompanhe a execução desse novo commit. Depois do deploy, atualize a página e confira o título.

```
- name: Empacotar arquivos do site
  uses: actions/upload-pages-artifact@v4
  with:
    path: './site'
```



**Conferência** O site está acessível. Três acertos rendem três pontos, nenhum acerto rende zero e a versão do título é atualizada após o novo deploy.

**Q19** O que o path ./site seleciona para o artefato de publicação? Por que precisamos conferir esse caminho?

Resposta

**Q20** Que evidências ligam a alteração do título à versão que está no endereço publicado?

Resposta

**Evidência a registrar** Registre o endereço do site, o commit do novo título e o link da execução que publicou essa mudança.


## Etapa 11 Bloqueio de uma versão com defeito

Tempo sugerido de 20 minutos. Conceito de DevOps — Controle da publicação por verificações.

Agora já existe um site publicado. Vamos verificar como uma alteração com erro afeta o próximo deploy.

1. Abra site/pontuacao.js, mude pontos += 1 para pontos += 2 e registre o commit Impede publicacao com erro.
2. Abra a execução correspondente. Identifique a falha de Testar pontuacao e o estado skipped do job Publicar site.
3. Abra o endereço publicado e responda corretamente apenas uma pergunta. Compare o resultado da página com o valor observado no teste da revisão com defeito.
4. Restaure pontos += 1 e registre o commit Recupera fluxo de publicacao.
5. Confira testes e publicação aprovados na nova execução.

**Conferência** Na execução com defeito, publicar fica skipped. A versão anterior continua pontuando um acerto como um ponto. Após correção, o deploy volta a ocorrer.

**Q21** A execução com falha retirou o site do ar? Explique o que você observou no endereço publicado e no job publicar.

Resposta

**Q22** Como a mesma evidência demonstra integração contínua e controle da implantação? Identifique cada parte do processo.

Resposta

**Evidência a registrar** Registre o link da execução com testes reprovados e publicar skipped e o link da recuperação com ambos aprovados.


## Etapa 12 Novo teste e explicação individual do pipeline

Tempo sugerido de 15 minutos. Conceito de DevOps — Manutenção das verificações e aplicação do aprendizado.

Você vai acrescentar um caso de teste e explicar como a configuração controla a publicação.

1. Antes de editar, determine o resultado de respostas [0, null, 2] contra gabarito [0, 1, 2].
2. Abra tests/pontuacao.test.js, clique no lápis e acrescente o sexto caso abaixo ao final, preservando os anteriores. Faça commit Amplia verificacao de respostas em branco.
3. Acompanhe a nova execução e confirme seis testes aprovados e publicação concluída.
4. Cada integrante responde Q23 e Q24 individualmente no campo indicado em RESPOSTAS.md, antes de discutir com a equipe.
5. Entregue o arquivo de respostas preenchido e os links exigidos.

```
test('respostas parcialmente em branco somam dois pontos', () => {
  assert.equal(calcularPontuacao([0, null, 2], [0, 1, 2]), 2);
});
```



**Conferência** A execução final tem seis testes aprovados. As respostas individuais usam a configuração e os resultados da própria prática.

**Q23** Se alguém remover needs: testes do job publicar, a falha de testes ainda garante o bloqueio? Qual configuração você restauraria e como comprovaria a correção?

Resposta

**Q24** Escolha um comportamento de uma aplicação que seu grupo poderia construir. Proponha um teste com entrada e resultado esperado e explique em que momento do pipeline ele deve executar.

Resposta

**Evidência a registrar** Registre o link da execução final com seis testes e complete as duas respostas individuais com identificação de cada integrante.
