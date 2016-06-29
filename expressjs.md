#Express.js

##### 28/06/2016

###Introdução a middleware

Hoje nós vamos falar um pouco sobre o que são middlewares.
Bom para começarmos vamos analizar a estrutura mínima dos middlewares.

```javascript
[...]
app.use(function(req, res, next){
    //Faca alguma coisa
    next();
});
[...]
```
Vamos lá, primeiramente vamos pensar no que está acontecendo, o que faz o *use*? Este código está colocando esta função dentro de um array de execução. Imagine isso:
```
var execucao = [middleware1, middleware2, middleware3];
```
bom, não é exatamente isso que ocorre, mas pense dessa forma, quando um middleware é colocado primeiro ele será executado primeiro e o último será executado por último, similar aos índices do array. Você deve ter reparado no *next()*, pois bem ele é quem determina quando o método acaba, não só isso você também pode mandar um erro e parar a execução, para isso passe o erro como parâmetro para o next().

Agora a pergunta é, 'onde a mágica começa?', pois bem, vamos ver um pequeno exemplo envolvendo alguns middlewares:

```javascript
[...]
app.use(function(req, res, next){
    console.log(req.qualquervalor);
    next();
});
app.use(function(req, res, next){
    req.qualquervalor = 'qualquervalor';
    next();
});
app.use(function(req, res, next){
    console.log(req.qualquervalor);
    next();
});
[...]
```
Executando este código será percebido que primeiramente o terminal mostrará *undefined* e depois mostrará *qualquervalor*, isso ocorre porque todos os middlewares compartilham os valores 'req' e 'res' não só isso, como este recurso é passado de middleware para middleware em ordem do de cima para o debaixo, então cuidado! Ordem é extremamente importante.
