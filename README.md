# DataFarm App Job Opportunity


### Bem vindo ao DataFarm!

Este exercício visa conhecer melhor os seus conhecimento e habilidades como desenvolvedor.

O projeto disponibilizado tem o propósito de servir como base para algumas atividades, que ao final serão encaminhadas e avaliadas.


# Atividades

A Atividade proposta consiste na criação de um app em [React-Native](https://reactnative.dev/), este app será usado para registrar
as paradas de uma operação agrícola, ou seja, quando uma maquína no campo esta trabalhando, muitas vezes o operador precisa
parar a operação para fazer alguma manutenção na maquina, almoçar ou muitas vezes um problema climático como uma chuva pode 
parar uma operação. Este app então será como um "diário" de tudo que aconteceu no campo.

O App possue três telas:

* **(Tela de Login)**
  * A tela de login dele levar o logo do DataFarm (disponivel neste repositório) 






Quando entrar no endereço será aberto uma janela para adicionar o seu código 
fornecido previamente ex: `172e77d8-6da8-4074-93d1-ede238f80785`.

<img alt="insert-code" width="400" src="https://job.datafarm.app/doc/insert-code.png"/>

Este código será encaminhado em todas as chamadas e é o que possibilida ter acesso as apis desta atividade.

*Você poderá ver mais detalhes na implementação do inteceptor em* `src/app/core/application/interceptor/application.interceptor.ts`.

*Também poderá ter acesso ao exemplo da aplicação base no endereço [job.datafarm.app](https://job.datafarm.app)*.

*A documentação pode ser encontrada no endereço [job.datafarm.app/api/swagger](https://job.datafarm.app/api/swagger)*

*Endpoint base para as apis - https://job.datafarm.app/*

### Atividade 1

O mapa possui dois botões de ação e o contorno de um talhão (*inglês: Field* | **região dentro de uma fazenda**)

<img alt="field-menu" width="300" src="https://job.datafarm.app/doc/field-menu.png"/>

A atividade consiste em quando clicar no botão **verde** deverá abrir uma janela (*modal*) com as informações do 
talhão como nome do Produtor (*grower*) da Fazenda (*farm*) e do próprio talhão. Esta janela deverá ter um CRUD 
destas informações e deverá fazer uso do endpoint `/api/field/{idField}` para recuperar e persistir os campos.
Também deverá conter na janela um dashboard que pode ser consultado no endpoint `/api/field/{idField}/dashboard`.
Este dashboard contém 3 gráficos:

- `evolution`: **Gráfico de evolução de pragas** este gráfico deverá ser no formato de linhas.
- `rain`: **Gráfico de chuva** este gráfico deverá ser no formato de barras e no eixo x deverá ser relativo aos dias que choveram.
- `efficiency`: **Gráfico de eficiência produtiva** este gráfico deverá ser no formato de pizza.

Exemplo do mock da Janela:

<img alt="insert-code" width="600" src="https://job.datafarm.app/doc/modal.png"/>

*Imagens reais do sistema para inspiração*:

#### Fique livre pela escolha da biblioteca para os gráficos. 
#### Os gráficos a seguir foram feitos com a biblioteca [Chart.js](https://www.chartjs.org/) 

-------------------------------------

<img alt="yieldgap" width="600" src="https://job.datafarm.app/doc/yieldgap-1.png"/>

-------------------------------------

<img alt="yieldgap" width="600" src="https://job.datafarm.app/doc/yieldgap-2.png"/>

-------------------------------------

<img alt="yieldgap" width="600" src="https://job.datafarm.app/doc/crop-window.png"/>


### Atividade 2 

##### (**Optional - Diferencial**)

Adicionar os outros talhões da fazenda usando o endpoint `/api/farm`, 
este endpoint irá retornar os outros contornos no formato GeoJSON no campo `fields`, 
estes talhões devem ser ativados com o click sobre eles no mapa e deverá respeitar a lógica da atividade 1, 
ou seja, quando clicar no botão **verde** deverá retornar o CRUD do talhão e o 
dashboard daquele talhão selecionado. E o botão vermelho deverá remover o contorno daquele talhão do mapa.

-----------------------

# Submissão das atividades

Para submeter as atividades faça o build do projeto com o comando:

```shell
npm run build
```

Remova a pasta `node_modules`, `.angular` e comprima o projeto todo em formato `.zip`,
esta escolha para submissão das atividades garante a sua privacidade.

Ex.: 
```shell
npm run build
rm -r node_modules
rm -r .angular
zip -r datafarm-job-opportunity.zip .
``` 

Com o Arquivo `.zip` acesse [job.datafarm.app/submission](https://job.datafarm.app/submission),
preencha com o seu código fornecido e carregue o arquivo zip. 

<img alt="yieldgap" width="350" src="https://job.datafarm.app/doc/submission.png"/>

#### BOA SORTE!!!
