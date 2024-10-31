# Momento
# Momento

## 1- Quantos funcionarios da empresa Momento trabalham no departamento de vendas?

* R: 10 funcionarios.
```js
db["funcionario"].countDocuments({departamento: ObjectId('85992103f9b3e0b3b3c1fe71')})
```

## 2- Inclua suas próprias informações no departamento de Tecnologia da empresa.

 *R: Informações Adicionadas, insertedId: ObjectId('671ec85e994db10c6fb4a480').
```js
db["funcionario"].insertOne({
    nome:"Anna Cristina Santos",
    telefone:"11.40289.2248",
    email:"cristinaanna05@gmail.com",
    cargo:"Desenvolvedora Frontend",
    dataAdmissão:"2024-08-21",
    salario:21.000,
     departamento:ObjectId('85992103f9b3e0b3b3c1fe74')
     })

```

## 3- Agora diga, quantos funcionários temos ao total na empresa?

R: 24 funcionários.
```js
db["funcionario"].countDocuments()
```
---
## 4- E quanto ao Departamento de Tecnologia?

* R: 6 funcionários. 
```js
db["funcionario"].countDocuments({departamento:ObjectId('85992103f9b3e0b3b3c1fe74')})
```

## 5-  Qual a média salarial do departamento de tecnologia?

* R: Média Salarial:R$5.800
```js
db["funcionario"].aggregate([{$match:{departamento:ObjectId('85992103f9b3e0b3b3c1fe74')}},$group:{_id: null,mediaSalarios:{$avg:"$salario"}}},{$project:{_id:0,mediaSalarios:1}},{$limit:1}])
```

## 6- Quanto o departamento de Vendas gasta em salários?

* R: Salário: 95.100
```js
db["funcionario"].aggregate([{$match:{departamento:ObjectId('85992103f9b3e0b3b3c1fe71')}},{$group:{_id:null,Salario:{$sum:"$salario"}}},{$project:{_id:0,Salario:1}}])
```

## 7- Um novo departamento foi criado. O departamento de Inovações. Ele será locado no Brasil. Por favor, adicione-o no banco de dados da empresa.

*R: Departamento Adicionado.
```js
db["departamento"].insertOne({nome:"Inovações",escritorio:ObjectId('6722e3a400653ce18e125e97')})
db["escritorio"].insertOne({
  nome: "Downgrill",
  endereco: "Praça General Gentil,200,Brasil-SP",
  telefone: "11.40289.2248", 
  pais: "BR",
  suprimentos:[{
      produto: "Garrafa Termica",
      quantidade: 10,
      precoUnitario: 260.00
    },
    {
      produto: "Bloco de Notas",
      quantidade: 4,
      precoUnitario: 180.50 
    },
    {
      produto: "Toalha",
      quantidade: 6,
      precoUnitario: 150.00
    },
    {
      produto: "Caneta",
      quantidade: 30,
      precoUnitario: 200
    },
    {
      produto: "Cumbuca",
      quantidade: 250,
      precoUnitario: 305.00 
    }
  ]
})


```
## 8- O departamento de Inovações está sem funcionários. Inclua alguns colegas de turma nesse departamento.  
*R: Funcionários Adicionados.
```js
db["funcionario"].insertMany([{nome:"Andressa Prudente", 
telefone:"11.5374.0230",
email:"andressaprudentedev@gmail.com", 
Cargo:" Desenvolvedora Full Stack/Designer", 
dataAdmissão: "2024-08-26",
salario: "17.000", 
departamento:ObjectId('6722ea791b0595e440c36a18') 
},
{
nome:"Victor Curtis", 
telefone:"11.23456.0956",
email:"curtisvictor@gmail.com",
dataAdmissao:"2024-08-26",
cargo:"Desenvolvedor BackEnd",
salario:"17.000", 
departamento:ObjectId('6722ea791b0595e440c36a18')
},
{
nome: "Gabriel Augusto",
 telefone: "11.78889.6789",
email: "gabrielaugusto@gmail.com",
dataAdmissao: "2024-08-26",
cargo: "Design",
salario: "30.000",
departamento:ObjectId('6722ea791b0595e440c36a18')
},
{
nome: "Grazielly Cavalcante",
telefone: "1100893.6734",
email: "graziellycavalcante@gmail.com",
dataAdmissao: "2024-08-26",
cargo: " Desenvolvedora BackEnd",
salario: "17.000",
departamento:ObjectId('6722ea791b0595e440c36a18')
},
{
nome: "Hudson Rocha",
telefone: "11.89654.5567",
email: "hadrocha@gmail.com",
dataAdmissao: "2024-08-26",
cargo: "Desenvolvedor Frontend",
salario: "18.000",
departamento:ObjectId('6722ea791b0595e440c36a18')
},
{
nome: "Júlio Cesar",
telefone: "11.33456.5789",
email: "juliocesar@gmail.com",
dataAdmissao: "2024-08-26",
cargo: "Diretor de RH",
salario: "25.000",
departamento:ObjectId('6722ea791b0595e440c36a18')}])
```

## 9- Quantos funcionarios a empresa Momento tem agora?

*R: 34 Funcionários.
```js
db["funcionario"].countDocuments()
```

## 10- Quantos funcionários da empresa Momento possuem conjuges?

*R: 7 Funcionários.
```js
db["funcionario"].countDocuments({"dependentes.conjuge":{$exists:true}})

```

## 11- Qual a média salarial dos funcionários da empresa Momento, excluindo-se o CEO?

*R: R$ 10.103
```js
db["funcionario"].aggregate([{$match:{cargo:{$ne:"CEO"}}},{$group:{_id:null,mediaSalarios:{$avg:"$salario"}}},{$replaceRoot:{newRoot:{mediaSalarios:"$mediaSalarios"}}}])

```

## 12- Qual a média salarial do departamento de Tecnologia??

*R: R$:5.800
```js
db["funcionario"].aggregate([
  {
    $match: {
      departamento: ObjectId("85992103f9b3e0b3b3c1fe74")
    }
  },
  {
    $group: {
      _id: null,
      salarioMedio: { $avg: "$salario" }
    }
  }
])
```


## 13- Qual o departamento com a maior média salarial?

*R: Execultivo.
```js
db["funcionario"].aggregate([
  {
    $group: {
      _id: "$departamento",
      mediaSalarial: { $avg: "$salario" }
    }
  },
  {
    $sort: { mediaSalarial: -1 }
  },
  {
    $limit: 1
  }
])
```

## 14- Qual o departamento com o menor número de funcionários?

*R: Execultivo.
```js
db["funcionario"].aggregate([
  {
    $group: {
      _id: "$departamento",
      totalFuncionario: { $sum: 1 }
    }
  },
  {
    $sort: { totalFuncionario: 1 }
  },
  {
    $limit: 1
  }
])
```

## 15- Pensando na relação quantidade e valor unitario, qual o produto mais valioso da empresa?

*R: Sabre de Luz.
```js
 db["vendas"].aggregate([{ $sort:{ quantidade:-1}},
 {$sort:{ precoUnitario:-1}}, { $limit: 1 }])
 ```

## 16- Qual o produto mais vendido da empresa?

*R: Laço da verdade.
```js
db["vendas"].aggregate([
  {
    $group: {
      _id: "$produto",
      totalVendido: { $sum: "$quantidade" }
    }
  },
  {
    $sort: { totalVendido: -1 }
  },
  {
    $limit: 1
  }
])

```
## 17-Qual o produto menos vendido da empresa?

*R: Uniforme do Superman
```js
db["vendas"].aggregate([{ $sort: { quantidade: -1 } }, { $limit: 1 }]);
```
