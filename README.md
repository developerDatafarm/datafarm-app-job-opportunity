# DataFarm App Job Opportunity


### Bem vindo ao DataFarm!

Este exercício visa conhecer melhor os seus conhecimento e habilidades como desenvolvedor.

O projeto disponibilizado tem o propósito de servir como base para algumas atividades, que ao final serão encaminhadas e avaliadas.


# Atividades

A Atividade proposta consiste na criação de um app em [React-Native](https://reactnative.dev/), este app será usado para registrar
as paradas de uma operação agrícola, ou seja, quando uma maquína no campo esta trabalhando, muitas vezes o operador precisa
parar a operação para fazer alguma manutenção na maquina, almoçar ou muitas vezes um problema climático como uma chuva pode 
parar uma operação. Este app então será como um "diário" de tudo que aconteceu no campo.

As funcionalidades desta atividade foram extraídas de uma aplicação real, esta aplicação pode ser baixada e pode ser usada 
como inspiração bem como responder algumas duvidas que possam surgir de comportamento das funcionalidades.

### DataFarm Máquinas
[Google Play](https://play.google.com/store/apps/details?id=com.br.datafarm.machines&pcampaignid=web_share) |
[App Store](https://apps.apple.com/ie/app/datafarm-m%C3%A1quinas/id6450794801?platform=iphone)


###

###

**domínio das apis (host)**: `https://job.minhafazenda.ag`

##### Importante: A aplicação deve utilizar React-Native sem o uso de ferramentas como Expo. O domínio do build também é um requisito de avaliação.


## Tela 1 - Login
  * A tela de login deve levar o logo do DataFarm ([/assets/logo-datafarm.png](https://github.com/developerDatafarm/datafarm-app-job-opportunity/blob/main/assets/logo-datafarm.png)) e os campos de usuário e senha
  * O usuário e senha para acesso foi fornecido no email que você recebeu para esta atividade
  * A autenticação deve ser feita usando o endpoint `/api/auth/v2`, este endpoint recebe um método post passando o email, senha e idPartner. O idPartner é fixo `372`.
O resultado deste endpoint será um Token que será usado em todos os outros endpoint passando sempre no `header` com a chave `authorization`. 
  
```javascript
fetch(`https://job.minhafazenda.ag/api/auth/v2`, {
  method: `POST`,
  headers: {
   'Content-Type': 'application/json',
   Accept: '*/*'
  },
  body: JSON.stringify({
   email: 'exemplo@email.com',
   senha: 'senha1234',
   idPartner: 372
  })
})
  .then((response) => response.json())
  .then((data) => {
     console.log(data);
     const token = data.data.token;
    });
```
<img alt="screen-1" width="400" src="https://datafarm-job-opportunity.s3.sa-east-1.amazonaws.com/doc/screen-1-v1.png"/>


## Tela 2 - Registro de parada

  * Na tela de registro de parada o usuário deve escolher um talhão (*inglês: field* | **região dentro de uma fazenda**) de uma fazenda (*farm*).
Escolhido o talhão, o usuário irá escolher uma das maquinhas daquele produtor (*grower*) pois a mesma maquina pode ser usada em varias fazendas daquele produtor.


Exemplo de um talhão na vida real:

<img alt="example-field" width="300" src="https://datafarm-job-opportunity.s3.sa-east-1.amazonaws.com/doc/field-example.png">

*(SC 01, SC 02... são talhões da fazenda Santa Cristina do produtor Carlos Alberto)*

  * Após dizer qual talhão e maquina, o usuário então poderá escolher qual o motivo daquela parada ex.: abastecimento
e selecionara quanto tempo ficou parado naquele local e por fim se necessário, adicionar uma nota (texto livre) desta parada.

<img alt="screen-2" width="400" src="https://datafarm-job-opportunity.s3.sa-east-1.amazonaws.com/doc/screen-2.png"/>

  * Os recursos como fazenda, talhões, maquinas e quais os motivos de paradas possiveis, podem ser obtidos pelo endpoint `/mobile/machine/resources` 

```json5
// GET https://job.minhafazenda.ag/mobile/machine/resources
// response:
{
  partner: {id: 372, name: 'Job Opportunity'}, // informações sobre o partner (representa esta atividade)
  user: {
    // informações do usuário
  },
  resources: {
    machineries: [
      {id: 5356,
       name: 'CL 045 - S690',
       serialNumber: '1CQS690ACK0125217',
       growerId: 10944}
    ],
    farms: [
      {id: 17135, name: 'Alvorada', 
       growerId: 10944, growerName: 'Carlos Alberto',
       fields: [
         {id: 108911, name: 'VS 01'}
        ]
      }
    ],
    reasons: [
      {
        id: 1,
        name: 'Abastecimento de combustível',
        icon: 'M192 160c0-17.673 14.327-32 32-32v0h320c17.673 0 32 14.327 32 32v0 320c0 17.673-14.327 32-32 32v0h-320c-17.673 0-32-14.327-32-32v0-320z M64 128c0-70.692 57.308-128 128-128v0h384c70.692 0 128 57.308 128 128v0 512c70.692 0 128 57.308 128 128v0 32c0 17.673 14.327 32 32 32s32-14.327 32-32v0-288h-32c-17.673 0-32-14.327-32-32v0-200c0-17.673 14.327-32 32-32v0h95.68c-0.704-30.464-3.392-57.216-12.864-78.208-5.232-12.379-13.961-22.429-24.945-29.158l-0.271-0.154c-11.776-7.040-29.696-12.48-57.6-12.48-17.673 0-32-14.327-32-32s14.327-32 32-32v0c36.096 0 66.176 7.040 90.368 21.504 24.512 14.592 40.576 35.264 50.816 58.048 18.88 41.92 18.816 93.76 18.816 133.184v203.2c0 0.019 0 0.041 0 0.064 0 17.673-14.327 32-32 32-0 0-0-0-0-0l-32-0v288c0 53.019-42.981 96-96 96s-96-42.981-96-96v0-32c0-35.346-28.654-64-64-64v0 256h32c17.673 0 32 14.327 32 32s-14.327 32-32 32v0h-704c-17.673 0-32-14.327-32-32s14.327-32 32-32v0h32v-832zM640 128c0-35.346-28.654-64-64-64v0h-384c-35.346 0-64 28.654-64 64v0 832h512v-832z'
      }
    ]
  }
}
```

 * Para salvar esta parada deve ser utilizado o endpoint `/mobile/machine/stop-register/registry`, este endpoint recebe um método post com os seguintes campos:

```json5
// POST https://job.minhafazenda.ag/mobile/machine/stop-register/registry
// request:
{
  uuid: 'f400bf91-916d-403b-8fe9-29496bf05a07', // id da parada
  note: null,
  idFarm: 17135,
  idField: 108911,
  idReason: 1,
  idMachinery: 5356,
  minutes: 10, // tempo total da parada em minutos
  longitude: -55.12, // longitude do local da parada
  latitude: -13.55   // latitude do local da parada
}
```


## Tela 3 - Listagem *local* das paradas 

 * O app deve conter uma copia local de todas as paradas já registradas naquele dispositivo, e a terceira tela deve listar estas paradas.

<img alt="screen-3" width="400" src="https://datafarm-job-opportunity.s3.sa-east-1.amazonaws.com/doc/screen-3-v2.png"/>

 * Os botões de relógio e lista na parte inferior do app deve ser usado para navegar entre as telas de listagem e registro de nova parada.


## (**Optional - Diferencial**)

  Em condições reais nas operações em campo quase sempre não possuem o acesso a internet, esta tarefa consistem em transformar este app para rodar de forma totalmente offine.
  O fluxo então seria da seguinte forma:
  * O usuario acessa o app na sede da fazenda (com acesso a internet) em seguida vai a campo com o celular registrando todas as paradas (offine), 
no final do dia ele retorna a sede da fazenda e realiza o sincronismo com o backend usando as apis*

###### *a api `/mobile/machine/resources` pode receber as paradas em lote

-----------------------

# Submissão das atividades

Para submeter as atividades faça o build do projeto para a versão android usando o formato de `apk`, 
envie a apk como anexo para o email que recebeu o convite para esta etapa.

Após enviar a apk para o email, compartilhe o seu código com **[Patrick Rogger Garcia](https://github.com/PatrickRogger)** através do [GitHub](https://github.com/PatrickRogger)

#### BOA SORTE!!!
