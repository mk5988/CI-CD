# Consulta dos elementos do workflow

## workflow

Receita completa registrada em um arquivo YAML.

## on e push

Eventos que iniciam a execução. Push corresponde ao envio de alterações.

## branches e main

Filtro que seleciona a branch principal neste exercício.

## workflow_dispatch

Permite iniciar a execução manualmente na interface do Actions.

## jobs e testes

Conjunto de trabalhos e identificador do trabalho de testes.

## name

Nome legível mostrado na interface do GitHub Actions.

## runs-on e runner

Define o ambiente que executa o job. Ubuntu é o sistema usado aqui.

## steps

Lista de passos de um job, executados em sequência.

## uses e checkout

Chama uma action. Checkout busca o código do commit no runner.

## with e setup-node

Configura os parâmetros da action que prepara o Node.js.

## run e npm test

Executa o comando de testes definido no package.json.

## needs

Declara dependência de outros jobs. Aqui exige o sucesso de testes.

## permissions

Define acessos concedidos à automação, como leitura e publicação.

## environment

Identifica o ambiente de implantação e permite associar sua URL.

## artifact e path

Pacote de arquivos e pasta de origem selecionada para publicação.

## id e outputs

Identifica um passo e permite consultar seus valores de saída.

## concurrency

Controla execuções simultâneas do mesmo grupo.

## skipped

Indica um job ou passo que foi pulado na execução.
