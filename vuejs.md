#Vue.js


##### 26/06/2016

### Acesso ao servidor por Ajax

O plugin oficial [Vue-Resource](https://github.com/vuejs/vue-resource) fornece serviços para fazer requsições HTTP e receber as respostas usando um XMLHttpRequest ou JSONP.

##### 27/06/2016

### Rotear web app no vue.js

Hoje irei relatar algumas impressões que eu tive a respeito de roteamento com [vuejs](vuejs.org). [Esta página](http://vuejs.org/guide/application.html#Routing) lhe ensinará algumas coisas importantes sobre esse passo, e uma das recomendações é usar a lib padrão para roteamento, a [vue-router](http://router.vuejs.org/en/index.html), ele irá pedir para que você escolha a opção mais razoável para seus projetos.

Pois bem, siga este [site](http://router.vuejs.org/en/index.html) que você irá conseguir configurar suas rotas corretamente, algo bastante interessante nessas rotas é que você terá que tratar algumas coisas, por exemplo, por padrão seu site ficará com estes símbolos '#!', mas logicamente que você pode contornar isso, bastando por na configuração este option [history](http://router.vuejs.org/en/options.html) como *true*, mas isso acarreta em um problema. Vamos analisar:

Quando o usuário clicar em algum link interno ele irá renderizar normalmente, mas ao tentar atualizar a página ou copiar o tal link, seu servidor tentará executar os códigos e como aquela rota pode não existir no seu server ele dará erro 404, sim isso mesmo, ele irá procurar a rota no server e não no vue.js, como resolver isso? O próprio site ensina para quem usa [proxies](http://readystate4.com/2012/05/17/nginx-and-apache-rewrite-to-support-html5-pushstate/) tem um [tutorial ensinando](http://readystate4.com/2012/05/17/nginx-and-apache-rewrite-to-support-html5-pushstate/) tanto no Apache quanto no Nginx, o que a solução sugere é apenas fazer com que seu server ignore todos os erros 404 e execute o index.html ou index.php dependendo do que você usar, minha solução para o node.js é apenas que você apague todos os códigos de tratamento de erros, pelo menos do tipo 404 e faça o render para o 'index.ejs'. Boa sorte!

