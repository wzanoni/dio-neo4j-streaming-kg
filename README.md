# dio-neo4j-streaming-kg
# Grafo de Conhecimento para Serviço de Streaming — Neo4j

Projeto prático do desafio da DIO modelando um grafo de conhecimento para recomendação e descoberta de conteúdo em um serviço de streaming utilizando **Neo4j** e **Arrows.app**.

## Contexto e Justificativa do Grafo

Serviços de streaming dependem de relações muitos-para-muitos entre usuários, títulos (`Movie` e `Series`), gêneros, atores e diretores. Em bancos relacionais, recomendações colaborativas, afinidades de elenco/direção e caminhos de conexão exigem múltiplos *joins* e consultas recursivas custosas. Com um grafo de propriedades no Neo4j, a travessia direta por relacionamentos torna consultas de vizinhança e recomendações mais naturais, legíveis e escaláveis.

## Modelo do Grafo

O modelo atende aos requisitos do desafio com seis entidades e quatro tipos de relacionamento:

- **Nós:** `User`, `Movie`, `Series`, `Genre`, `Actor`, `Director`.
- **Relacionamentos:**
  - `(:User)-[:WATCHED {rating, watchedAt}]->(:Movie | :Series)`[cite: 1]
  - `(:Actor)-[:ACTED_IN {role}]->(:Movie | :Series)`[cite: 1]
  - `(:Director)-[:DIRECTED]->(:Movie | :Series)`[cite: 1]
  - `(:Movie | :Series)-[:IN_GENRE]->(:Genre)`[cite: 1]

### Diagrama no Arrows.app
![Diagrama do Grafo no Arrows.app](model/arrows-schema.png)

### Esquema Físico no Neo4j (`CALL db.schema.visualization()`)
![Esquema Físico no Neo4j](model/neo4j-schema-viz.png)

## Estrutura do Repositório

```text
├── README.md
├── model/
│   ├── arrows-schema.png
│   ├── arrows-schema.json
│   └── neo4j-schema-viz.png
├── scripts/
│   ├── 01_constraints_and_seed.cypher
│   └── 02_business_queries.cypher
└── evidences/
