# MEAN- primeira aplicacao do zero

---

## <a name="indice">Índice</a>

- [Introdução-Instalação](#parte1)   
- [MongoDB](#parte2)   
- [Node](#parte3)   
- [Express](#parte4)   
- [Angular](#parte5)   
- [](#parte6)   
- [](#parte7)   
- [](#parte8)   
- [](#parte9)   
- [](#parte10)   
- [](#parte11)   
- [](#parte12)   



---

## <a name="parte1">Introdução-Instalação</a>

- https://www.mongodb.com/

- https://nodejs.org/en/


[Voltar ao Índice](#indice)

---

## <a name="parte2">MongoDB</a>

- Aula 01
```
mongod - Inicializar o servidor do Mongo

mongo - Iniciar o console do Mongo

show dbs  - Listar todas as databases
use db_finance  - Usar database db_finance
db  - Verificar o database atual
show dbs  

db.createCollection('billingCycles')  - Criar Collection billingCycles
show dbs  
show collections  - Listar as Collections

db.createCollection('billingcycles')  
show collections  
 
db.billingCycles.drop()  -  Remover a Collection billingCycles
show collections  - show collections

db.billingcycles.drop()  -  Remover a Collection billingcycles
show collections  

show dbs  

```

- Aula 02

```
show dbs
use db_finance - Usar database db_finance
show collections

db.billingcycles.insert({name:"Janeiro/17", month: 1, year: 2017}) - Inserção na Collection billingcycles
show collections
show dbs

db.billingcycles.save({name:"Fevereiro/17", month: 2, year: 2017}) - Salvar na Collection billingcycles

db.billingcycles.insert({ - Inserção na Collection billingcycles
  name:"Março/17",
  month: 3,
  year: 2017,
  credits: [
    {name: "Salário", value: 5000}
  ],
  debts: [
    {name: "Luz", value: 100, status: "PAGO"},
    {name: "Telefone", value: 100, status: "PENDENTE"}
  ]
})
```

- Aula 03

```
use db_finance

db.billingcycles.find() - Listar todos os registros da Collection

db.billingcycles.find().pretty() - Listar os registros da Collection com uma melhor leitura
db.billingcycles.findOne() - Listar apenas um registro da Collection
db.billingcycles.findOne({month: 2}) - Listar apenas um registro da Collection que contém mês 2
db.billingcycles.find({$or: [{month: 1}, {month: 2}]}).pretty() - Listar apenas um registro da Collection que contém mês 1 ou
mês 2 com uma melhor leitura
db.billingcycles.find({credits:{$exists:true}}).pretty() - Listar os registros da Collection com o atributo credits com
uma melhor leitura
db.billingcycles.find({year:2017}) -  Listar os registros da Collection que contém ano 2017
db.billingcycles.find({year:2017}).skip(1) - Listar os registros da Collection menos o primeiro registro
db.billingcycles.find({year:2017}).limit(1) - Listar apenas um registros da Collection menos o primeiro
registro

```

- Aula 04

```
- Criar fluxo do pipeline para somatória de credits e debts
db.billingcycles.aggregate([{
  $project:{credit:{$sum:"$credits.value"},debt:{$sum:"$debts.value"}},
}, {
  $group:{_id:null,credit:{$sum:"$credit"},debt:{$sum:"$debt"}}
}])

- Listar apenas um registro da Collection que contém mês 3
db.billingcycles.findOne({month: 3})
```

- Aula 05

```
- Atualizar o registro da collection
db.billingcycles.update({
  $and:[{
    month: 1
  }, {
    year:2017
  }]
}, {
  $set: {
    credits:[{
      name:"Salário",value:5000
    }]
  }
})

- Listar apenas um registro da Collection
db.billingcycles.findOne()

- Listar os registros da Collection com atributo credits e retornar o atributo name com uma melhor leitura
db.billingcycles.find({credits:{$exists:true}}, {_id:0, name:1}).pretty()
```

- Aula 06
```
db.billingcycles.count() - Contar quantos registros tem a Collection

- Remover os registros da Collection que contém mês 2
db.billingcycles.remove({month:2})
db.billingcycles.count()

- Remover apenas um registros da Collection que contém ano 2017
db.billingcycles.remove({year:2017}, 1)
db.billingcycles.count()

- Remover a database db_finance
db.dropDatabase()
show dbs

```

[Voltar ao Índice](#indice)

---

## <a name="parte3">Node</a>

- Aula 01 (ex01.js)

```js
const ola = () => console.log('Olá Node');
setInterval(ola, 1000);

node ex01.js
```

- Aula 02

```js
//FundamentosMEAN/node/ex02_utils.js
function upper(text) {
    return text.toUpperCase();
}
module.exports = {upper}

```

```js
//FundamentosMEAN/node/ex02_teste.js
const utils = require('./ex02_utils.js')
console.log(utils.upper('teste de upcasa'))
```

- Aula 03

```js
// FundamentosMEAN\node\ex03_singleton.js
let numero = 1;

function exibirProximo(){
    console.log(numero++);
}

module.exports = {exibirProximo}
```

```js
// FundamentosMEAN\node\ex03_teste.js
const s1 = require('./ex03_singleton');
const s2 = require('./ex03_singleton');

s1.exibirProximo();
s2.exibirProximo();
s1.exibirProximo();
s2.exibirProximo();
```

- Aula 04
```js
// FundamentosMEAN\node\ex04_global.js
const PI = 3.14;
console.log(global.PI);

global.obj = {
    name: 'Estou no global!'
}
```

```js
// FundamentosMEANnode\ex04_teste.js
require('./ex04_global')
console.log(global.obj.name)
console.log(obj.name)
```

- Aula 05
```js
// FundamentosMEAN/node/ex05_module.js
console.log(global === this);
console.log(module === this);
console.log(module.exports === this);

this.digaOi = function () {
    console.log('Oi!!!')
};
```

```js
// FundamentosMEAN/node/ex05_teste.js
const modulo = require('./ex05_module')
modulo.digaOi()
```

- Aula 06
```js
const _ = require('lodash')

const alunos = [{
    nome: 'Joao',
    nota: 7.6
}, {
    nome: 'Maria',
    nota: 8.6
}, {
    nome: 'Pedro',
    nota: 8.1
}];

const media = _.sumBy(alunos, 'nota') / alunos.length;

console.log(media);
```
- npm init -y [Criar arquivo package.json]
- npm i lodash --save [Instalando a dependência lodash]

- Aula 07

```js
// FundamentosMEAN/node/ex07_param.js
module.exports = function(param) {
    console.log(`O param informado foi ${param}`)
}
```

```js
//FundamentosMEAN/node/ex07_teste.js

const moduloComoParam = require('./ex07_param');
moduloComoParam('param1');

```

- Aula 08

```js

// FundamentosMEAN/node/ex08_process.js
function temParam(param) {
    return process.argv.indexOf(param) !== -1
}
if(temParam('--producao')){
    console.log('Atenção total!')
} else {
    console.log('Tranquilo!!!')
}

//node ex08_process
//node ex08_process --prducao
  
```

- Aula 09
```js
// FundamentosMEAN/node/ex09_process.js
process.stdout.write('Está gostando do curso? ')
process.stdin.on('data', function(data) {
    process.stdout.write(`Sua resposta foi ${data.toString()}Obrigado!\n`)
    process.exit()
})
```

- Aula 10

```js
// FundamentosMEAN/node/ex10_fs.js
const fs = require('fs')
const files = fs.readdirSync(__dirname)
files.forEach(f => console.log(f))
```
- Aula 11

```js
// FundamentosMEAN/node/ex11_http.js
const http = require('http')
const server = http.createServer(function(req, res) {
    res.writeHead(200, {"Content-Type": "text/html"})
    res.end('<h1>Acho que é melhor usar o Express, não?</h1>')
})
const porta = 3456
server.listen(porta, function() {
    console.log(`Escutando a ${porta}`)
})
```


[Voltar ao Índice](#indice)

---

## <a name="parte4">Express</a>

- Aula 01 - Configuração e Mapeando uma Rota
```js
const express = require('express');
const server = express();

server.get('/', function (req, res) {
    res.send('<h1>Index!</h1>');

});

server.all('/teste', function (req, res) {
    res.send('<h1>TESTE</h1>');
});

server.get(/api/, function (req, res) {
    res.send('<h1>API</h1>');
});

server.listen(3000, () => console.log('Executando'));
```

- Aula 02 - Cadeia de Middlewares
```js
const express = require('express');
const server = express();

server.get('/', function (req, res, next) {
    console.log('inicio...');
    next();
    console.log('fim...');

});

server.get('/', function (req, res) {
    console.log('Resposta....');
    res.send('<h1>NEXT!!</h1>');

});

server.listen(3000, () => console.log('Executando Servidor....'));
```

- Aula 03 - Método USE
```js
const express = require('express');
const server = express();


server.use('/api',function (req, res, next) {
//server.use(function(req, res, next) {
    console.log('Inicio...')
    next()
    console.log('Fim...')
})

server.use('/api',function (req, res) {
//server.use(function(req, res) {
    console.log('Resposta...')
    res.send('<h1>API!</h1>')
})

server.listen(3000, () => console.log('Executando Servidor....'));
```

- Aula 04
```js

```

- Aula 05
```js

```

- Aula 06
```js

```


[Voltar ao Índice](#indice)

---

## <a name="parte5"></a>


[Voltar ao Índice](#indice)

---

## <a name="parte6"></a>


[Voltar ao Índice](#indice)

---

## <a name="parte7"></a>


[Voltar ao Índice](#indice)

---

## <a name="parte8"></a>


[Voltar ao Índice](#indice)

---

## <a name="parte9"></a>


[Voltar ao Índice](#indice)

---

## <a name="parte10"></a>


[Voltar ao Índice](#indice)

---

## <a name="parte11"></a>


[Voltar ao Índice](#indice)

---

## <a name="parte12"></a>


[Voltar ao Índice](#indice)

---