# Banco de Dados não Relacional escola
Repositório para a avaliação da materia de Banco de Dados não Relacional

# 1. Subindo o MongoDB com Docker
docker run --name escola_volistica -p 27017:27017 -d mongo:latest

# 2. Acessando o Banco (mongosh)
docker exec -it escola_volistica mongosh

 3. Criando o Banco
use escola

# 4. Criando a Coleção
db.createCollection("alunos")

# 5. Inserindo Alunos
db.alunos.insertMany([
  {
    "nome": "Giba",
    "idade": 19, 
    "curso": "Suzano Ataque Explosivo",
    "notas": [7, 8, 9],
    "endereco": { "cidade": "Londrina", "estado": "PR" }
  },
  {
    "nome": "Fofão",
    "idade": 21,
    "curso": "São Caetano Levantamento Mágico",
    "notas": [9, 9, 10],
    "endereco": { "cidade": "São Paulo", "estado": "SP" }
  },
  {
    "nome": "Serginho",
    "idade": 25, 
    "curso": "Sesc Defesa Sólida",
    "notas": [6, 7, 8],
    "endereco": { "cidade": "Diamante do Norte", "estado": "PR" }
  },
  {
    "nome": "Ana Moser",
    "idade": 17, 
    "curso": "Transbrasil Cortada Letal",
    "notas": [8, 9, 9],
    "endereco": { "cidade": "Blumenau", "estado": "SC" }
  },
  {
    "nome": "Fabiana",
    "idade": 18, 
    "curso": "Sesc Defesa Sólida", 
    "notas": [7, 7, 8],
    "endereco": { "cidade": "Belo Horizonte", "estado": "MG" }
  }
])


# 6. (1) Buscar os alunos
db.alunos.find()

# 7. (2) Buscar alunos do curso "ADS"
db.alunos.find({ curso: "ADS" })

# 8. (3) Buscar alunos com idade maior que 21
db.alunos.find({ idade: { $gt: 21 } })

# 9. (4) Atualizar a idade de um aluno
db.alunos.updateOne(
  { nome: "Serginho" },
  { $set: { idade: 23 } }
)

# 10. (5) Adicionar uma nova nota a um aluno
db.alunos.updateOne(
  { nome: "Giba" },
  { $push: { notas: 10 } }
)

# 11. (6) Remover um aluno
db.alunos.deleteOne({ nome: "Fofão" })

# 12. (7) Média de notas por aluno
db.alunos.aggregate([
  {
    $project: {
      _id: 0,
      nome: 1,
      media: { $avg: "$notas" }
    }
  }
])

# 13. (8) Quantidade de alunos por curso
db.alunos.aggregate([
  {
    $group: {
      _id: "$curso",
      quantidade: { $sum: 1 }
    }
  }
])
