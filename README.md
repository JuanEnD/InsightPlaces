# InsightPlaces | 2º Challenge Data Science Alura

A imobiliária InsightPlaces, situada na cidade do Rio de Janeiro, está enfrentando dificuldades para alugar e vender imóveis. Em uma pesquisa de como empresas semelhantes operam no mercado, a InsightPlaces percebeu que esse problema pode estar relacionado aos valores dos imóveis e às recomendações realizadas em seu site.

| :placard: Vitrine.Dev |   |
| -------------  | --- |
| :sparkles: Nome       | **InsightPlaces**
| :label: Tecnologias | Python, PySpark
| :rocket: URL         | https://github.com/JuanEnD/InsightPlaces 
| :fire: Desafio     | [Link do Challenge](https://www.alura.com.br/challenges/data-science-2)  


<!-- Inserir imagem com a #vitrinedev ao final do link -->
![Empresa InsightsPlaces do projeto](https://i.imgur.com/Tnj84r9.jpg#vitrinedev) 

## Detalhes do projeto
Esse projeto tem algumas etapas, como: ler e fazer o tratamento do histórico dos preços de imóveis no Rio de Janeiro, construir um modelo de regressão para precificar imóveis e criar um recomendado de imóveis. Usando os métodos do PySpark, que é uma interface para Apache Spark em Python.

O projeto usou uma base de dados de imóveis na cidade do Rio de Janeiro, onde a InsightPlaces disponibilizou os dados contidos no banco de dados quanto às informações de preços de imóveis da cidade do Rio de Janeiro.

[Base de dados - InsightPlaces](https://caelum-online-public.s3.amazonaws.com/challenge-spark/semana-1.zip)

### Dicionário de Dados - Anuncio

| Colunas         | Descrição                                                      |
|-----------------|----------------------------------------------------------------|
| id              | Código de identificação do anúncio no sistema da InsightPlaces |
| tipo_unidade    | Tipo de imóvel (apartamento, casa e outros)                    |
| tipo_uso        | Tipo de uso do imóvel (residencial ou comercial)               |
| area_total      | Área total do imóvel (construção e terreno)                    |
| area_util       | Área construída do imóvel                                      |
| quartos         | Quantidade de quartos do imóvel                                |
| suites          | Quantidade de suítes do imóvel                                 |
| banheiros       | Quantidade de banheiros do imóvel                              |
| vaga            | Quantidade de vagas de garagem do imóvel                       |
| caracteristicas | Listagem de características do imóvel                          |
| andar           | Número do andar do imóvel                                      |
| endereco        | Informações sobre o endereço do imóvel                         |
| valores         | Informações sobre valores de venda e locação dos imóveis       |

## Sobre o desafio

###  Etapas do projeto
-   **Semana 1:** Transformação dos dados com PySpark: Explorar e tratar uma base de dados que veio dos sistemas internos da empresa InsightPlaces.
-   **Semana 2:** Tratamento dos dados e criação de um modelo de regressão com PySpark: Criar um modelo de regressão para prever os valores dos imóveis.
-   **Semana 3 e 4:** Criando um modelo de recomendação com PySpark: Onde vou criar um recomendador de imóveis.
<!-- -   **Semana 4:** Ajustes gerais e correções de bugs. -->

### -  **1 semana:**
Na primeira semana eu baixei a biblioteca do PySpark para iniciar a leitura da base de dados para utilizar no projeto, depois de ler os dados fui explorar para tratar os dados, separar cada um dos camps da Base de Dados e deixar apenas as informações do campo "anuncio" já que nessa base tinha 3 campos principais que eram: Anuncio, Imagem e Usuario. 

Então, como precisaria para analisar apenas as informações do campo Anuncio eu apaguei as outras e foquei em analisar as colunas desse campo. Após fazer essa separação comecei a analisar e fazer todos os tratamentos de cada uma das colunas, um deles foi transformar os dados das colunas "quartos", "suites", "banheiros", "vaga", "area_total" e "area_util" de listas para inteiros. Em seguida, precisei extrair da coluna "endereco" apenas as informações de "zona" e "bairro" para transformar apenas elas duas como colunas no DataFrame, logo depois fui separar os campos da coluna "valores" para cada uma ser um campo ser coluna assim como tinha feito na coluna "endereco" já que nessa coluna "valores" tinha as informações de condominio, iptu, tipo, e valor.

Por último após tratar todos esses dados finalizei o Notebook salvando esse DataFrame que tinha criado com todas as informações de Anuncio no formato Parquet, que é um formato de arquivo de código aberto e orientado por colunas, ele é bastante eficiente quando se trata de armazenar e analisar grandes volumes de dados. Também salvei o DataFrame em CSV, depois fiz um teste de desempenho entre a leitura dos dois arquivos.

### -  **2 semana:**

