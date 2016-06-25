

#Javascript

##### 25/06/2016

### Dica com objetos

Olá pessoal, tudo bom? Esse será nosso primeiro momento desse devdiario, e para iniciarmos vamos falar sobre objetos analisando algumas situações, então abra o bloco de notas e vamos começar a programação.

Primeiramente instale o [jquery](https://jquery.com/)( servirá apenas para a manipulação do DOM ), agora com ele instalado, vamos começar explicando o que será feito. Iremos criar uma ferramenta similar a uma calculadora bem simples, mas não terá todos aqueles botões, apenas um input para colocarmos o valor e dois botões que irá somar e subtrair, o valor inicial será 0.

```html
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

