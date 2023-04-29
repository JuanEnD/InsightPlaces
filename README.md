# InsightPlaces | 2º Challenge Data Science Alura

A imobiliária InsightPlaces, situada na cidade do Rio de Janeiro, está enfrentando dificuldades para alugar e vender imóveis. Em uma pesquisa de como empresas semelhantes operam no mercado, a InsightPlaces percebeu que esse problema pode estar relacionado aos valores dos imóveis e às recomendações realizadas em seu site.

| :placard: Vitrine.Dev |                                                                      |
| --------------------- | -------------------------------------------------------------------- |
| ✨ Nome               | **InsightPlaces**                                              |
| 🏷 Tecnologias        | Python, PySpark                                                      |
| 🚀 URL                | https://github.com/JuanEnD/InsightPlaces                             |
| 🔥 Desafio            | [Link do Challenge](https://www.alura.com.br/challenges/data-science-2) |

<!-- Inserir imagem com a #vitrinedev ao final do link -->

![Empresa InsightsPlaces do projeto](https://i.imgur.com/Tnj84r9.jpg#vitrinedev)

## Detalhes do projeto

Esse projeto tem algumas etapas, como: ler e fazer o tratamento do histórico dos preços de imóveis no Rio de Janeiro, construir um modelo de regressão para precificar imóveis e criar um recomendado de imóveis. Usando os métodos do PySpark, que é uma interface para Apache Spark em Python.

O projeto usou uma base de dados de imóveis na cidade do Rio de Janeiro, onde a InsightPlaces disponibilizou os dados contidos no banco de dados quanto às informações de preços de imóveis da cidade do Rio de Janeiro.

[Base de dados - InsightPlaces](https://caelum-online-public.s3.amazonaws.com/challenge-spark/semana-1.zip)

### Dicionário de Dados - Anuncio

| Colunas         | Descrição                                                        |
| --------------- | ------------------------------------------------------------------ |
| id              | Código de identificação do anúncio no sistema da InsightPlaces |
| tipo_unidade    | Tipo de imóvel (apartamento, casa e outros)                       |
| tipo_uso        | Tipo de uso do imóvel (residencial ou comercial)                  |
| area_total      | Área total do imóvel (construção e terreno)                    |
| area_util       | Área construída do imóvel                                       |
| quartos         | Quantidade de quartos do imóvel                                   |
| suites          | Quantidade de suítes do imóvel                                   |
| banheiros       | Quantidade de banheiros do imóvel                                 |
| vaga            | Quantidade de vagas de garagem do imóvel                          |
| caracteristicas | Listagem de características do imóvel                            |
| andar           | Número do andar do imóvel                                        |
| endereco        | Informações sobre o endereço do imóvel                         |
| valores         | Informações sobre valores de venda e locação dos imóveis      |

## Sobre o desafio

### Etapas do projeto

- **✔️ Semana 1:** Transformação dos dados com PySpark: Explorar e tratar uma base de dados que veio dos sistemas internos da empresa InsightPlaces.
- **✔️ Semana 2:** Tratamento dos dados e criação de um modelo de regressão com PySpark: Criar um modelo de regressão para prever os valores dos imóveis.
- **✔️ Semana 3 e 4:** Criando um modelo de recomendação com PySpark: Onde vou criar um recomendador de imóveis.

<!-- -   **Semana 4:** Ajustes gerais e correções de bugs. -->

---

### -  **1º semana:** 

Na primeira semana eu baixei a biblioteca do PySpark para iniciar a leitura da base de dados para utilizar no projeto, depois de ler os dados fui explorar para tratar os dados, separar cada um dos camps da Base de Dados e deixar apenas as informações do campo "anuncio" já que nessa base tinha 3 campos principais que eram: Anuncio, Imagem e Usuario.

Então, como precisaria para analisar apenas as informações do campo Anuncio eu apaguei as outras e foquei em analisar as colunas desse campo. Após fazer essa separação comecei a analisar e fazer todos os tratamentos de cada uma das colunas, um deles foi transformar os dados das colunas "quartos", "suites", "banheiros", "vaga", "area_total" e "area_util" de listas para inteiros. Em seguida, precisei extrair da coluna "endereco" apenas as informações de "zona" e "bairro" para transformar apenas elas duas como colunas no DataFrame, logo depois fui separar os campos da coluna "valores" para cada uma ser um campo ser coluna assim como tinha feito na coluna "endereco" já que nessa coluna "valores" tinha as informações de condominio, iptu, tipo, e valor.

Por último após tratar todos esses dados finalizei o Notebook salvando esse DataFrame que tinha criado com todas as informações de Anuncio no formato Parquet, que é um formato de arquivo de código aberto e orientado por colunas, ele é bastante eficiente quando se trata de armazenar e analisar grandes volumes de dados. Também salvei o DataFrame em CSV, depois fiz um teste de desempenho entre a leitura dos dois arquivos.

---

### -  **2º semana:** 

No inicio do Notebook dessa semana utilizei a base de dados que teve algumas transformações e salvei no final da primeira semana, depois fiz uma etapa muito importante na construção de modelos de Machine Learning que é a seleção de features, escolhendo quais colunas são importante e descartar as irrelevantes para a análise reduzindo a complexidade dos dados inseridos que por conseequência o modelo irá demorar menos tempo para ser ajustado. Nesse processo descartei as colunas ("area_total", "tipo_anuncio", "tipo_unidade", "tipo_uso" e "tipo") e antes existia duas colunas com muitos dados iguais que eram a ('area_util', 'area_total'), então verifiquei qual das duas tinha mais dados nulos e descobri que era a ("area_total").

Em seguida, converti os tipos de algumas colunas que estavam erradas, como por exemplo de numéricas das colunas "andar", "banheiros", "suites" e "quartos" para o tipo inteiro. Além disso também converti as colunas "area_util", "condominio", "iptu" e "valor" para o tipo double. Após isso fui fazer um tratamento da coluna características, porque ela possuia listas de strings como conteúdo de suas linhas, mas algumas dessas listas estão sem elementos. Então transformei essas listas sem elementos em valores nulos utilizando os recursos da biblioteca **functions** do PySpark, depois fiz um tratamento com os dados faltantes (nulos e NaN's) porque possui muito deles em todo o DataFrame e os modelos de Machine Learning não costumam trabalhar corretamente com dados nulos.

Então após todos esses tratamentos nas colunas comecei a preparação dos dados para os algoritmos do **Spark MLlib**, utilizei a técnica de vetorização dos dados e usei a classe **VectorAssembler** da biblioteca **pyspark.ml.feature**. Em seguida comecei a construção dos modelos de regressão para auxiliar na previsão dos valores de imóveis após os dados já estarem vetorizados, o primeiro modelo utilizado foi o **Random Forest** que é um modelo de Machine Learning que utiliza a técnica de ensemble learnin (aprendizado de ensemble), ele é composto por uma coleção de árvores de decisão onde cada uma dessas árvores é treinada com uma amostra aleatória do conjunto de dados. Assim o modelo no final faz a média dos resultados de cada uma das árvores para obter a predição mais correta.

**[Todos os Detalhes](https://github.com/JuanEnD/InsightPlaces/tree/main/Semana_2)**

---

### -  **3º e 4º semana:**

Iniciei o notebook utilizando a base de dados que tinha feito o tratamento na última semana para utilizar no modelo de Machine Learning de Regressão. Após isso, apliquei as transformações para utilizar os dados no modelo de clustering utilizando o **VectorAssembler** e fiz uma padronização nos dados para consegui utilizar o PCA neles, por meio da classe **StandardScaler** **do PySpark** para realizar esse processo e criar **o** modelo de recomendação, mas antes disso preciso reduzir a dimensão dos dados e para fazer isso preciso utilizar a técnica chamada PCA assim teria um novo conjunto de dados onde as colunas serão uma combinação linear das colunas originais. Após a transformação com o PCA posso utilizar o método **explainedVariance**que retorna a variância explicada por cada componente principal, com esse método conseguiria encontrar o número ideal de componentes princiapis que os dados devem possuir.

Em seguida, construi um Pipeline para facilitar a aplicação das transformações nos dados e o que antes eram vários processos separados agora era apenas um que fazia tudo desde o VectorAssembler até o PCA. Então depois de terminar esses tratamentos comecei a criar os Clusters com Kmeans que é um algoritmo de aprendizado não supervisionado que tem como objetivo encontrar grupos de dados que possuem características semelhantes e colocar todo em um mesmo Cluster. Também avaliei os dados de cada um dos Clusters para descobrir as informações de todos os imóveis, como quantidade de banheiros, quartos e tamanho do imóvel. Após isso fiz uma representação por meio de um gráfico de todos os dados dos imóveis que estão no Cluster, onde poderia ver qual o Cluster especifico e quais bairros são de cada um dos dados.

Então ao fazer todos esses tratamentos e criar os Clusters pude filtrar imóveis de um mesmo Cluster com um ID, além disso calculei a distância euclidíana para encontrar as 10 melhores recomendações. No final criei uma função recomendadora para que os Dev da **InsightPlaces** conseguissem utilizar o recomendador no site, por isso nessa função coloquei todas as outras etapas que tinha feito antes dos imóveis, recomendados e procurado.
