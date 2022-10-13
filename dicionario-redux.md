#Dicionário redux

##Action

Action é uma função que retorna um objeto (ou apenas o objeto). Este objeto contém obrigatoriamente um type, e opcionalmente contém um payload. O objeto representa uma ação que será feita em um reducer.

Exemplo:

```
{
  type: ‘incrementar’
}
```

##Dispatch/Dispatcher

Dispatch é a ação de disparar uma action. A action sozinha é apenas um objeto com a “assinatura” que o redux aceita, já o dispatch é uma função que oficializa que aquela action está sendo disparada para o redux.

Exemplo:

```
dispatch(incrementar(2))
```
A função incrementar() retorna a action com type e payload

##Immer

Immer é uma biblioteca que consegue lidar com imutabilidade mais facilmente, para que você não precise se preocupar em estar mutando um estado ou não.

##Imutabilidade

Imutabilidade é o ato de você nunca mudar um dado. É uma técnica que permite que tenhamos um projeto muito mais performático, pois como o dado nunca é mudado, ou seja, no redux nunca retornamos um estado mudado, e sim um novo estado.

##InitialState

InitialState é o estado inicial de um reducer, ele é obrigatório pois é usado como o primeiro ponto de um estado antes das alterações que as actions disparadas farão.

##Payload

Payload é o nome da propriedade dentro do objeto action. Dentro desta propriedade colocamos um ou mais argumentos que gostaríamos de utilizar dentro do reducer.

Exemplo:

```
{
  type: ‘incrementar’,
  payload: {
    id: ‘123’ // id que quero incrementar
    quantidade: 2 // quantidade que quero incrementar
  }
}
```

##Provider

Provider é um componente da biblioteca ‘react-redux’ que nos permite prover o Store para todos os componentes abaixo dele.

##Reducer

Reducers são pequenos estados dentro do Store. Reducers são funções que aceitam um estado inicial e as actions como argumentos, e sempre retornam um novo estado.

Exemplo:

```
function contadorReducer(state = 0, action) {
  if(action.type === ‘incrementar’) {
    return state += action.payload;
  }
  return state;
}
```

##Redux Toolkit

Redux Toolkit é uma biblioteca que facilita a criação de inúmeras coisas no Redux. Com ele, conseguimos criar Reducers abstratos utilizando Slices, que automaticamente cria actions para nós e consegue resolver os estados com imutabilidade de forma automática.

##React Redux

Redux em si não é uma biblioteca React, e sim uma biblioteca Javascript. React Redux nos permite utilizar o Redux dentro do React, nos provendo funções/componentes utilitárias(os) como o Provider, useDispatch e useSelector, por exemplo.

##Slice

Slice é o termo usado pelo Redux Toolkit para se referir ao pedaço que criamos que corresponderá ao Reducer, as Actions e as Action types correspondentes àquele reducer. É criado com a função createSlice do Redux toolkit.

Exemplo:

```
import { createSlice } from '@reduxjs/toolkit';

const contadorSlice = createSlice({
  name: ‘contador’ // nome do reducer
  initialState: 0 // estado inicial do reducer
  reducers: {
    incrementar: (state) => { // esta função é uma action, ele automaticamente gera um type ‘contador/incrementar’
      state++ // esta linha parece simples, mas ela utilizará o Immer por debaixo dos panos para incrementar o contador com imutabilidade!
    }
  }
})

const { incrementar } = contadorSlice.actions; // contadorSlice.actions contém todas as actions criadas.
const contadorReducer = contadorSlice.reducer; // aqui está o reducer, que deve ser indexado ao Store
```
Aqui pode parecer confuso que escrevemos “contadorSlice.reducers” e recebemos “contadorSlice.actions”, mas há uma explicação para isso. No Redux vanilla, o Reducer é uma função apenas que normalmente tinha um switch case que lidava com cada action, retornando um estado novo dependendo de cada action que gostaríamos de realizar, mas desta forma fica bem complexo, pois devemos criar uma action para cada ação que gostaríamos e um case novo dentro do switch case lidando com aquela action (aqui está um exemplo disto na documentação do redux). O redux toolkit te pede para criar “vários reducers”, que são a representação daquele switch case, e retorna para nós, ao mesmo tempo, a action que criaríamos e como lidaríamos com ele dentro do switch case, prático né?

##State

State é um termo relativo no Redux, mas a forma mais comum de ser utilizado é se referindo ao estado atual de um reducer. Dentro de useSelector, State representa o estado de todo o Store.

##Store

Store é o estado total do Redux, com todos os reducers e algumas funções utilitárias como getState() e dispatch(), entre outras.

##Type

Type é um identificador de uma action, que será utilizada pelo reducer para identificar aquela ação e saber o que fazer com ela. Se o type é “incrementar” dentro do reducer deve haver um tratamento para caso a action seja do type incrementar. Caso esteja utilizando Redux Toolkit, o type é criado automaticamente.

##useDispatch

useDispatch é um hook da biblioteca react-redux, que nos permite disparar uma action.

Exemplo:

```
const dispatch = useDispatch();

dispatch(incrementar(2));
```
##useSelector

useSelector é um hook que nos permite acessar o state de toda a aplicação. Nele, você pode receber todo o estado de uma só vez ou pegar exatamente o que você precisa. O recomendado é que seja utilizado para filtrar exatamente o necessário para o seu componente atual, pois o seu componente fica “conectado” ao estado entregue pelo useSelector, logo ele atualizará sempre que aquele estado mudar.

Exemplo:

const contador = useSelector(state => state.contador); // Aqui temos que escrever state.contador pois state é o store inteiro, e contador é o state do reducer de nome contador.

Uma dúvida que talvez possa aparecer é o por quê não utilizamos o nome state ao invés de store no parâmetro do useSelector. Normalmente Store é utilizado para se referir à variável store diretamente, nela não só temos o state de todo o Redux do projeto como também a algumas funções que existem dentro dela, então colocamos state pois é literalmente o state do store.

##View

View é o nome que damos à parte de visualização, ou seja, todos os componentes que criamos.