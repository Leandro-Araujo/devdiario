#Node.js

##Sumário

[Controlar funções assicronas](https://github.com/Leandro-Araujo/devdiario/blob/master/nodejs.md#controlar-fun%C3%A7%C3%B5es-assicronas)

- [process.nextTick()](https://github.com/Leandro-Araujo/devdiario/blob/master/nodejs.md#processnexttick)

- [Promise](https://github.com/Leandro-Araujo/devdiario/blob/master/nodejs.md#promise)

- [Async](https://github.com/Leandro-Araujo/devdiario/blob/master/nodejs.md#async)

##### 25/06/2016

### Controlar funções assicronas

Muitas vezes vejo como um problema para quem está iniciando com node.js o controle de funções assícronas, bom principalmente quando há variáveis para configurar a função assícronas e muitas vezes funções que necessitam do retorno de operações I/O, bom, e como resolver isso?

A forma mais corretar de trabalhar com essas funções são os callbacks, mas algumas vezes as pessoas necessitam trabalhar de outra maneira, por isso apresento aqui este pequeno artigo.

#### process.nextTick()

[process.nextTick()](https://nodejs.org/dist/latest-v6.x/docs/api/process.html#process_process_nexttick_callback_arg) é nativa do node.js, com ela você pode fazer com que qualquer código seja chamado após o loop pertinente a ele, seus códigos serão executados após todos os outros sícronos, com isso você pode até mesmo simular processamento assícrono, dando a seus callbacks e códigos flexibilidade maior, evitando transtornos.

#### Promise

[Promise](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise) é um objeto padrão do ES2015(dependendo da versão do node.js que você estiver utilizando esta propriedade pode não estar disponível) serve para controlar as funções assícronas(elas continuarão sendo assícronas, mas obedecerão alguma ordem) serve para você obter respostas de alguma função assícronas e executar outro objeto logo após a última acabar.

#### Async

[Async](https://github.com/caolan/async) é um módulo que trás um conjunto de ferramentas para você trabalhar com códigos assícronos, parecido em parte com Promise, pois permite que você 'diga' qual código deve ser executado primeiro e também permite que você capture valores das funções assícronas, além disso contém uma série de ferramentas. Ele não é nativo, então baixe no [npm](https://www.npmjs.com/)


#### 28/06/2016

### npm

Segue os códigos npm que eu mais costumo usar:

```
npm init
```
npm init é utilizado para que você possa criar sua aplicação, iniciando com a configuração do package.json, recomendo bastante sua utilização, ele vai pedir para que você insira informações que ele pedir, tudo por terminal. Sem o package.json configurado você provavelmente terá problemas com algum módulo que você tentar importar.

```
npm install
```
Este código é muito útil quando você estiver testando um app de terceiros, por exemplo, ou baixar seus próprios apps de um repositório(recomendo vocês utilizarem o *gitignore*), isso porque ele instala todos os módulos que estejam descritos no package.json(é vantajoso você apagar todos os módulos de sua pasta *node_modules* principalmente porque sua aplicação ocupará menos espaço no seu repositório).

```
npm install module-name --save
```
Este código é bastante útil porque além de você colocar seus módulos disponíveis no *node_modules* você o coloca em seu package.json, atenção *module-name* é apenas um exemplo poderia ser *mongoose* e etc.
