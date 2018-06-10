# MEAN- primeira aplicacao do zero

---

## <a name="indice">Índice</a>

- [Introdução-Instalação](#parte1)   
- [MongoDB](#parte2)   
- [](#parte3)   
- [](#parte4)   
- [](#parte5)   
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

## <a name="parte3"></a>


[Voltar ao Índice](#indice)

---

## <a name="parte4"></a>


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