![Databricks](https://img.shields.io/badge/databricks-222832?style=for-the-badge&logo=databricks)
![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Apache Spark](https://img.shields.io/badge/Apache%20Spark-FDEE21?style=for-the-badge&logo=apachespark&logoColor=black)
![Apache Kafka](https://img.shields.io/badge/Apache%20Kafka-000?style=for-the-badge&logo=apachekafka)
![Apache Hadoop](https://img.shields.io/badge/Apache%20Hadoop-66CCFF?style=for-the-badge&logo=apachehadoop&logoColor=black)
![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white)
![Azure](https://img.shields.io/badge/azure-%230072C6.svg?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)
![Jupyter Notebook](https://img.shields.io/badge/jupyter-white?style=for-the-badge&logo=jupyter&logoColor=orange)
![Visual Studio Code](https://img.shields.io/badge/Visual%20Studio%20Code-0078d7.svg?style=for-the-badge&logo=visual-studio-code&logoColor=white)
![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)

# Enunciado Projeto Proposto

## Desenvolvimento e Avaliação de uma Arquitetura Distribuída para o Cadastro Ambiental Rural

### Objetivo:
O objetivo deste trabalho é explorar as capacidades de arquiteturas de bancos de dados distribuídos para lidar com conjuntos de dados "grandes", em particular, o "Cadastro Ambiental Rural". Os alunos devem propor uma nova arquitetura, implementá-la, modelar os dados de acordo com as especificações e projetar um particionamento efetivo. Em seguida, eles devem realizar uma bateria de testes comparativos nos ambientes distribuído e centralizado para avaliar o desempenho e a escalabilidade. Além disso, o trabalho deve abordar a migração da base de dados existente de um banco de dados centralizado para o novo ambiente distribuído.

### Descrição do Problema:
O "Cadastro Ambiental Rural" é um conjunto de dados que contém informações sobre propriedades rurais no Brasil. O desafio é projetar uma arquitetura que possibilite o gerenciamento eficiente desses dados, permitindo consultas e análises rápidas, mesmo diante do tamanho considerável da base de dados.

### Tarefas:
Os alunos devem seguir as seguintes etapas:

### Proposição da Nova Arquitetura:
Proponha uma arquitetura de banco de dados distribuído que seja adequada para lidar com o "Cadastro Ambiental Rural". Explique as escolhas de tecnologias, componentes e a lógica de funcionamento da arquitetura.

### Implementação da Arquitetura:
Implemente a arquitetura proposta em um ambiente de teste. Isso envolverá a configuração e integração de sistemas de gerenciamento de banco de dados distribuído, servidores, clusters e outros componentes necessários.

### Modelagem do Novo Banco de Dados:
Modele os dados do "Cadastro Ambiental Rural" de acordo com a arquitetura proposta.

### Projeto de Particionamento Adequado/efetivo:
Projete um esquema de particionamento que permita a distribuição eficiente dos dados em diferentes nós do banco de dados distribuído. Considere estratégias de particionamento horizontal.

### Bateria de Testes (queries)
Realize uma série de testes no ambiente distribuído e no ambiente centralizado. Avalie o desempenho em termos de tempo de resposta, escalabilidade e consumo de recursos. Registre e analise os resultados.

#### Consulta 1
Recupere a soma de área (em hectares) para todas as propriedades agrícolas que pertencem ao MS e MT. Ordene os resultados em ordem decrescente.

#### Consulta 2
Filtre todas as propriedades que pertecem a região sudeste. 

#### Consulta 3
Recupere todas as propriedades rurais que estão localizadas dentro de uma área geográfica específica delimitada por um polígono. Este polígono é descrito pelas seguintes coordenadas: POLYGON ((-53.5325072 -19.4632582, -51.0495971 -19.1625841, -51.3734501 -16.1924262, -53.8181518 -16.4010783, -53.5325072 -19.4632582))

#### Consulta 4
Calcule quantas propriedades foram cadastradas por ano. Apresente os resultados em ordem cronológica.

#### Consulta 5
Calcule o percentual médio de área remanescente de vegetação nativa em comparação a área total da propriedade

#### Consulta 6
Construa uma consulta que mostre a contagem de propriedades rurais por estado.

#### Consulta 7
Veja qual é a maior propriedade entre todas e calcule a distância entre ela e Brasília. Utilize a coordenada de centródide da propriedade para calcular a distância entre ela e Brasília. Coordenadas de Brasília: -15.796943053171708, -47.891638482569476

#### Consulta 8
Faça a média de área entre todas as propriedades. Calcule quantas propriedades por estado, estão acima da média. 

## PROJETO

### Objetivo

O objetivo principal deste projeto foi analisar o desempenho de consultas e processamento de dados em diferentes plataformas, integrando ferramentas como Databricks, Azure e MySQL. Buscamos compreender como particionamentos influenciam a performance, explorar dados geoespaciais utilizando consultas avançadas e integrar diferentes ambientes para obter resultados eficientes e precisos. Além disso, o projeto teve como meta aplicar técnicas de análise geográfica para identificar propriedades dentro de um polígono específico.

### DataBricks

No Databricks, realizamos o processamento de dados de tabelas particionadas armazenadas na Azure, com o objetivo de otimizar o desempenho das consultas. Implementamos funções geoespaciais utilizando a biblioteca Shapely, registrando-as como UDFs (User Defined Functions) para permitir sua utilização em consultas SQL. Para facilitar a análise, criamos views temporárias, que permitiram consultas mais simples e flexíveis.

Realizamos testes com quatro estratégias distintas de particionamento para avaliar a velocidade de processamento dos dados. No primeiro teste (projeto_big_data_queries_3), não houve particionamento manual; o Databricks dividiu o arquivo total automaticamente em quatro partes. No segundo teste (projeto_big_data_queries), particionamos os dados por estado (UF), resultando em nove partições. No terceiro teste (projeto_big_data_queries_2), foram criadas quatro partições por estado, enquanto, no quarto teste (projeto_big_data_queries_4), foi gerada apenas uma partição por estado. Esses testes foram fundamentais para comparar os tempos de processamento no Databricks com as consultas realizadas em um ambiente MySQL.

### Microsoft Azure

Na Azure, as tabelas foram armazenadas em um Data Lake, o que possibilitou o gerenciamento eficiente de grandes volumes de dados. Testamos configurações de particionamento para avaliar o impacto na performance de leitura e execução de consultas dentro do Databricks. Essa etapa foi essencial para identificar boas práticas no uso combinado dessas ferramentas.

### MySQL 

As consultas SQL seguiram as especificações do projeto, abrangendo análises geoespaciais e tabulares realizadas tanto no Databricks quanto em um ambiente MySQL configurado pelo instrutor. Essas consultas foram utilizadas para filtrar propriedades localizadas dentro de um polígono, contar registros e retornar informações detalhadas sobre essas propriedades. A integração entre os dois ambientes demonstrou a capacidade de realizar análises consistentes e eficientes em plataformas distintas, destacando a flexibilidade e a versatilidade na manipulação dos dados.

## Conclusão

Este projeto proporcionou uma experiência prática e abrangente no processamento e análise de dados geoespaciais, destacando a importância de estratégias eficientes para lidar com grandes volumes de dados em diferentes plataformas. No Databricks, aprendemos a implementar funções geoespaciais utilizando a biblioteca Shapely, registrar UDFs para consultas SQL e testar diferentes estratégias de particionamento para otimizar o desempenho de processamento. No ambiente MySQL, consolidamos o conhecimento em consultas SQL, reforçando a importância de ferramentas clássicas em análises específicas.

Além das habilidades técnicas, o projeto enfatizou a necessidade de flexibilidade e adaptação ao integrar múltiplos ambientes, demonstrando como cada ferramenta pode ser explorada para atender diferentes demandas analíticas. Com isso, foi possível comparar desempenhos, identificar pontos de melhoria e obter insights valiosos sobre a manipulação de dados em um contexto real. O aprendizado adquirido reforça a capacidade de planejar, executar e analisar projetos de dados de forma estruturada e eficaz.
