#Javascript

##Sumário
[Dica com objetos](https://github.com/Leandro-Araujo/devdiario/blob/master/javascript.md#dica-com-objetos)

##### 25/06/2016

### Dica com objetos

Olá pessoal, tudo bom? Esse será nosso primeiro momento desse devdiario, e para iniciarmos vamos falar sobre objetos analisando algumas situações, então abra o bloco de notas e vamos começar a programação.

Primeiramente instale o [jquery](https://jquery.com/)( servirá apenas para a manipulação do DOM ), agora com ele instalado, vamos começar explicando o que será feito. Iremos criar uma ferramenta similar a uma calculadora bem simples, mas não terá todos aqueles botões, apenas um input para colocarmos o valor e dois botões que irá somar e subtrair, o valor inicial será 0.

```html
index.html
<html>
  <head>
    <title>
      Calcuradora simples
    </title>
  </head>
  <body>
    <div>
      <input type="text" id="value" value="0"/>
      <input type="submit" id="somar" value="somar"/>
      <input type="submit" id="subtrair" value="subtrair" />
    </div>
      <div id="newValue"> </div>
    <script src='https://code.jquery.com/jquery-3.0.0.min.js'></script>
    <script src='./index.js'></script>
  </body>
</html>
```

```javascript
index.js
//Codigo para criar um objeto que faz os calculos e guarda os valores
var Calc = function(){
  this.valorAtual = 0;
  this.somar = function(valor){
    return this.valorAtual = this.valorAtual + valor;
  };
  this.subtrair = function(valor){
    return this.valorAtual = this.valorAtual - valor;
  }
}

$(function(){
  //Funções que respondem ao eventos do DOM e usa o objeto para para fazer os cálculos
  $('#somar').click(function(){
    calculadora = new Calc();
    $('#newValue').html( calculadora.somar( parseInt($('#value').val()) ) );
  });
  $('#subtrair').click(function(){
    calculadora = new Calc();
    $('#newValue').html( calculadora.subtrair( parseInt($('#value').val()) ) );
  });
});
```

Ao fazer isso você irá perceber um certo problema, aparentemente o objeto que criamos não guarda de fato o valor atual, o problema está no fato que o operador 'new' constrói um novo objeto apartir da função então nós temos duas referências para dois objtos diferentes, então como resolver isso?

```javascript
index.js
[...]
$(function(){
  //Funções que respondem ao eventos do DOM e usa o objeto para para fazer os cálculos
  calculadora = new Calc();
  $('#somar').click(function(){
    $('#newValue').html( calculadora.somar( parseInt($('#value').val()) ) );
  });
  $('#subtrair').click(function(){
    $('#newValue').html( calculadora.subtrair( parseInt($('#value').val()) ) );
  });
});
[...]
```

Este código resolve este tipo de problema, mas aí também gera outros problemas, primeiramente porque são as funções de manipulação de dom são assícronas e porque temos que acessar mais uma variável global que fica como intermediária, vamos a mais uma solução que pode ser a definitiva neste caso:

```javascript
index.js
var calc = {
  valorAtual : 0,
  somar : function(valor){
    return this.valorAtual = this.valorAtual + valor;
  },
  subtrair : function(valor){
    return this.valorAtual = this.valorAtual - valor;
  }
}
$(function(){
  $('#somar').click(function(){
    $('#newValue').html( calc.somar( parseInt($('#value').val()) ) );
  });
  $('#subtrair').click(function(){
    $('#newValue').html( calc.subtrair( parseInt($('#value').val()) ) );
  });
});
```
Isto ocorre porque só existe uma instância do objeto, é bastante útil para esse tipo de comportamento, podendo ser usado em sistemas de 'carrinhos' por exemplo.

##### 06/07/2016

###Erros

Existem várias formas de se trabalhar com erros, mas vamor falar dos blocos *try* e *catch*. Vamos começar com um pequeno código que vai acusar um erro.

```javascript
const a = 1;
a = 2;
```

Bom, se você não sabe o que é *const*, ela é uma palavra reservada para constantes, e como sabemos constantes quando são declaradas e tem seu valor setado, este valor não pode ser alterado. Gerando assim um erro.

A grande pergunta é para que serve o *try - catche*? Bom, com ele você não precisa trava os códigos quando o node.js identificar um erro, você pode também tratar todos os erros que acontecem como fossem um só, dando um tratamento geral e interessante para os seus códigos.

Aqui está o código base para o tratamento de erro:

```javascript
try {
    // Aqui você vai colocar a execução normal dos seus codigos
}catch(err){
    // Aqui voce vai colocar seus códigos caso haja algum erro
}
```

Vamos ver agora como implementar nosso erro com constantes:

```javascript
try {
    const a = 1;
    a = 2;
} catch(err){
    console.log('Oops seu código tem varios erros, como constantes e lets declarados de forma errada');
    // Você poderia enviar algum evento para alguma peça chave no seu desenvolvimento, por exemplo
}
```
