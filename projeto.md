# MVP em Engenharia de Dados

## Parte da avaliação da pós graduação em Ciência de Dados e Análises pela PUC-Rio

Estudante Ique Moraes<br/>
01 de Outubro de 2023

## 1.0 Objetivo

O objetivo desse projeto é providenciar dados e evidências a respeito dos acidentes em estradas federais dentro da região sudeste do Brasil, que ocorreram nos anos de 2020 e 2021.

Busca-se por luz sobre outras faces dos eventos por meio da construção de um a tabela de fácil e rápida consulta. Na atual versão, serão relacionados os acidentes nas estradas com os registros metereológicos da região sudeste.

## 2.0 Origem dos dados

Nsse projeto todos os bancos de dados usados se encontravam abertos para uso público.
Partindo dos dados de acidentes, postos como principais, foram agregados dados de outras fontes que pudessem enriquecer em informações. Todos os datasets foram coletados virtualmente sem produção de nenhum dado novo em instâncias. Os novos dados foram produzidos em processamento e transformações.

### 2.1 Os dados

1.Registros de acidentes nas rodovias federais.

São os dados da Polícia Rodoviária Federal tratados e disponibilizados por usuária na plataforma Kaggle. Atualizado em 18 de Setembro de 2023.
| Link | Licença |
| ---- | ------- |
| [Disponível aqui](https://www.kaggle.com/datasets/tgomesjuliana/police-traffic-incidents) |[Sobre uso dos dados do governo (Não relacionado ao Kaggle)](https://www.gov.br/prf/pt-br/acesso-a-informacao/dados-abertos)|

As tabelas estão separadas por ano e trazem dentro de cada ano as informações sobre

- data,
- horário,
- fase do dia,
- dia da semana,
- unidade federativa,
- identificação da rodovia,
- quilômetro na rodovia em que ocorreu o acidente,
- município,
- causa do acidente,
- tipo do acidente,
- classificação do acidente,
- sentido na rodovia,
- condição meterológica,
- tipo da pista,
- traçado da via,
- uso do solo,
- números de pessoas envolvidas, mortos, feridos ao total, feridos levemente, feridos gravemente, ilesos e veículos,
- latitude,
- longitude,
- superintendência regional da polícia federal,
- delegacia responsável
- e unidade operacional

<br/>
2-Registros do tempo pelas estações de meterologia disponíveis no Brasil.

Os dados originais são do Instituo Nacional de Meteorologia (INMET) e estão disponíveis após tratamentos por usuário(PROPPG/PPG em informática PUC) na plataforma Kaggle. Atulizado em Janeiro de 2023.
| Link | Licença |
| ---- | ------- |
| [Disponível aqui](https://www.kaggle.com/datasets/PROPPG-PPG/hourly-weather-surface-brazil-southeast-region/data) | [Tipo de licença](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html) |

As tabelas estão separadas por região, comportam dados de 2000 a 2021 e apresentam

- data da medição,
- horário,
- precipitação total dá última hora pré medição,
- pressão atmosférica na estação, maior e menos registros de pressão na última hora,
- radiação solar,
- temperaturas do ar, máxima e mínima da última hora pre medição em graus celsius,
- temperaturas do orvalho, máximo, mínima da última hora e a temperatura do ponto de orvalho durante a medição em graus celsius,
- umidade relativa do ar, máxima e mínima da última hora e a umidade relativa do ar durante a medição em grau celsius,
- direção do vento em graus e rajadas de vento em metros por segundo,
- velocidade do vento em metros por segundos durante a medição,
- unidade federativa,
- nome da estação,
- código da estação,
- região,
- latitude,
- longitude
- e elevação da estação em referência ao nível do mar.

<br/>
3.Dados de volume de tráfego nas praças de pedágio das rodovias em concessão privada.

Os dados originais são da Agência Nacional de transporte terreste (ANTT) e estão disponíveis no próprio site da agência como dado aberto. Atualizado em 28 de Setembro de 2023.
| Link | Licença |
| ---- | ------- |
|[Disponível aqui](https://dados.antt.gov.br/dataset/volume-trafego-praca-pedagio) | [Tipo de licença](https://opendefinition.org/licenses/cc-by/) |

No site estão dispopnibilizadas as tabelas com dados de 2010 a 2023. Foram usados somente os datasets de 2020 e 2021. Nas tabelas constam

- o nome da concessionaria,
- o mês e ano de referência do volume total,
- sentido na pista,
- nome da praça,
- categoria dos veículos calculados,
- tipo do veículo
- e o volume total dos referidos atributos.

<br/>
4.Dados das praças de pedágios

Os dados originais são da Agência Nacional de transporte terreste (ANTT) e estão disponíveis no próprio site da agência como dado aberto.
| Link | Licença |
| ---- | ------- |
|[Disponível aqui](https://dados.antt.gov.br/dataset/praca-de-pedagio)|[Tipo de licença](https://opendefinition.org/licenses/cc-by/) |

Estão disponibilizados os dados referente as praças de pedágio atuantes com última atualização em 28 de Setembro de 2023. Na tabela constam:

- Concessionária,
- nome da praça,
- ano que representa as informações do Plano Nacional de Viação e Sistema Nacional de Viação,
- rodovia em que está localizada,
- unidade federativa,
- quilômetro na rodovia,
- município,
- tipo de pista,
- sentido na pista,
- situação de atividade,
- data de inativação,
- latitude
- e longitude.

## 3.0 Coleta

A partir do download foram analisados superficialmente os dados de cada tabela. Foram conferidos as informações de cabeçalho com as apresentações das respectivas plataformas, valores nulos ou equivocados de fácil identificação, tipos de valores e separadores de colunas.

## 4.0 Modelagem

Com os conteúdos oferecidos em aula e com as discussões nos momentos ao vivo, o primeiro movimento foi pela construção de uma única tabela flat que trouxessem os dados mais próximos do local e do dia do acidente.
Porém, com a ferramenta utilizada não foi possível a implementação pelo modelo incialmente planejado.

Todos os registros de acidentes possuem data, hora, latitude e longitude.
Porém, os registros de medição do tempo não possuem dados de todos os dias por todas as estações disponíveis desde a implementação e tão pouco de muitas horas por dia.

Muitos dos registros do tempo ficam distantes do dia e horário do acidente.
Considerando que podem ocorrer mais de um registro de tempo por dia, foi planejado produzir valores médios ao redor dos dias registrados para usá-los em consulta como valor estimado.

As tabelas de volumes de carros nas estradas apresentam os valores totais do mês, trazendo dimensão de movimento na área próximo ao acidente mas com distante precisão.

Já as tabelas das praças de pedágio foram incorporadas por trazerem localização exata no mapa e suprir a fragilidade de alguns valores da tabela de volume de carros.
O projeto seguiu pela construção de um Datawarehouse em que os dados ficassem disponíveis
Partindo para um modelo de dados em múltiplas tabelas, assim ficaram os resultados.

Esquema da tabela de acidentes - nome: accidentsSEdata
![Esquema da tabela de acidentes parte 1.](/imgs/schemas/schema_accidentsfinaltable_part1.png)
![Esquema da tabela de acidentes parte 2.](/imgs/schemas/schema_accidentsfinaltable_part2.png)

Esquema da tabela de medição das condições climáticas - nome: treatedWeather
![Esquema da tabela de condições climáticas por dia.](/imgs/schemas/schema_weatherfinaldata.png)

Esquema da tabela de volume de carros por mês - nome:
![Esquema da tabela de volumes de carros por mês.](/imgs/schemas/schema_trafficvolumefinaldata.png)

Esquema da tabela das praças de pedágio - nome:
![Esquema da tabela das praças de pedágio.](/imgs/schemas/schema_tollsstationsfinaldata.png)

Ainda que separadas em 4 tabelas, os dados foram tratados e transformados para atender as necessidades de pesquisa a respeito dos acidentes por dia, hora e local. Porém, não apresentam relações diretas (uso de chaves estrangeiras).

## 5.0 Carga

A plataforma escolhida para servir de nuvem e desenvolver os dados foi a Azure. Dentro da Azure foram usadas as ferramentas Contas de armazenamento, Banco de dados SQL, SQL server, Data Factory e as implícitas de assinatura e grupo de recursos. Todas as ferramentas foram instanciadas e disponibilizadas para o uso.

### 5.1 Carregamento

Depois de baixados os dados originais, todos foram carregados na nuvem da Azure por meio de uma Conta de Armazenamento com uso da interface gráfica.

![Interface gráfica do carregamento dos dados.](/imgs/load/load_blobstorage.png)

Dentro do armazenamento foi construído um container para agrupar todos os dados originais necessários.

![Interface gráfica do container com os dados.](/imgs/load/load_container.png)

### 5.2 Extração

A extração dos dados foi realizada dentro da ferramenta Data Factory por meio da interface gráfica.

![Interface gráfica do data factory.](/imgs/extract/extract_trafficvolume.png)

Ao lado esquerdo, as tabelas originais e as tabelas finais conectadas na ferramenta Data Facotry.

Nesse processo foram configuradas as leituras das tabelas, os divisores,cabeçalhos, schemas importados e saídas iniciais.
Para que as transformações ocorressem como o esperado, com poucas exceções como nas colunas de data, os atributos foram inicialmente extraídos como string. Evitou-se assim que valores como latitude e longitude fossem arredondados ou processados mais de uma vez em mudança de tipagem.
Com os valores em string a leitura das múltiplas tabelas foram facilitadas, pois ainda que duas tabelas de anos diferntes tivessem as mesmas colunas, apresentavam tipos diferentes dentro do mesmo campo.
![Exemplo das tipagens iniciais nas importações.](/imgs/extract/extract_accidentsexample.png)

### 5.3 Transformação

Todo processo foi pensado para transformar com o menor número possível de dados. Ainda que não tenham sido realizados testes de desempenho, a opção foi eliminar colunas e linhas antes das trasnformações.

Em muitas das transformações foram usadas expressões próprias da Azure facilitando um pouco a inclusão de processos lógicos.

#### 5.3.1 Acidentes no sudeste do Brasil dos anos de 2020 e 2021

Os datasets originais estavam separados por anos e carragevam informações que foram consideradas dispensáveis neste projeto.
Transformações:

1. Seleção das colunas necessárias e renomeamento para facilitar identificação.(Excluídos os atributos que dizem respeito a Polícia como a regional responsável, a delegacia que registrou, a unidade de operação e a finalidade do solo ao redor da rodovia.)
2. Unificação das linhas, as instâncias de 2020 com as instâncias de 2021.
3. Filtragem das instâncias que ocorreram apenas dentro da região.
4. Padronização de valores nulos. Em distintas colunas possuíam valor "NA" e "Não Informado" trazendo inicialmente um equívoco de que não haviam valores nulos. Assim, as referidas string foram substituídas por strings vazias.

![Interface gráfica do dataflow de acidentes.](/imgs/dataflow/dataflow_accidents.png)

#### 5.3.2 Histórico de medições climáticas

O dataset de registro do tempo trazem dados dos anos 2000 a 2021 por toda região sudeste.
Transformações:

1. Seleção das colunas e renomeamento. Foram excluídas as colunas de medição de temperatura de ponto de orvalho, altura do nível do mar em que se encontram as estações e radiação solar.
2. Filtragem das instâncias. Foram selecionadas somente as linhas que correspondessem aos anos de 2020 e 2021.
3. Transformação dos valores nulos. Conforme apresentado no site em que o dataset foi obtido, valores iguais a -9999 ou -9999.0 era valores vazios ou nulos que surgiram durante processamento do administrador. Sendo assim, todas as colunas tratadas como string foram verificadas para substituir por string vazia.
4. Transformação dos tipos. Aos valores que caberiam análises matemáticas foram convertidos em tipo float. Onde os valores eram vazios automaticamente foram preenchidos como NULL.
5. Renomeação das colunas nesta etapa atendendo necessidades de pesquisa a respeito do problema.
6. Produção de dados. Considerando a possibilidade de existência de mais de um registro por dia e a impossibilidade de aproximação das horas do acidente com as horas do registro climático, foram gerados os dados por dia. Assim, os acidentes podem estar associados aos registros climáticos do dia ou do dia mais próximo.
   Observação: foram considerados registros dentro de um dia os atributos relacionados ao atributo da data do registro. Ainda que muitas instâncias tenham sido registradas à 00:00 de um dia e que possui colunas que fazem menção a uma janela de uma hora anterior, todos esses valores foram considerados ao dia do campo data.

![Interface gráfica do dataflow de registro climático.](/imgs/dataflow/dataflow_weather.png)

#### 5.3.3 Registro de volume nas estradas e lista das praças de pedágio

Os dados de volume nas estradas também estavam separados por anos.
As transformações realizadas foram:

1. União das instâncias dos dois datasets.
2. Filtragem das instâncias que estão dentro do território sudeste.
3. Renomeação das colunas para lowercase seguindo padrão das demais colunas das outras tabelas.
4. Transformação da coluna praca. O nome da praça na maioria das instâncias contém a rodovia, o quilômetro e o nome da praça. Assim, com uso das funções nativas e Regex a coluna foi fragmentada em 4 outras colunas para facilitar comparação e pesquisa com as demais tabelas.

O dataset com a lista das praças sofreu as seguintes transformações:

1. Remoção da coluna 'data_da_inativacao' pois como dados históricos do referido mês essa informação não será utilizada.
2. Filtragem das praças que se encontram dentro do território sudeste.
3. Trasnformação. Inserção de nova coluna 'nome_praca' para ficar mais próxima a coluna praca da tabela de volume de carros e também podronização das colunas concessionária, em lowercase, e rodovia removendo "BR-"dos valores.

![Interface gráfica do dataflow do volume de carros e lista dos pedágios.](/imgs/dataflow/dataflow_trafficvolume.png)

## 6.0 Análise

### 6.1 Qualidade de dados

Envolvendo os 6 datasets, de 4 objetos diferentes, várias incompatibilidades foram surgindo. Embora alguns pontos já tenham sido apresentados ao longo do documento, traço mais alguns apontamentos.
Todos os dados foram escritos em língua Portuguesa e esse foi um ponto para permanecer a identificação das colunas, assim como das instâncias, no mesmo idioma. Porém, caracteres acentuados e outras configurações nos títulos dos atributos causavam erro de renderização e atrapalhavam a identificação. Logo, quase todos os títulos foram reescritos em caixa baixa no formato snake case e quando em possível redundância, concatenado substantivo que o ajudasse a ser facilmente identificado.
Nos casos das colunas da tabela sobre o tempo, muitos valores inteiros e fracionados possuem diferentes medidas. A umidade relativa do ar é dada em porcentagem, as temperaturas em graus celsius e outras medidas. A escolha foi permanecer com a identificação original escrevendo ao final do título as medidas representadas.

A decisão de entrar com a maioria dos valores em tipo string se deu após algumas consultas e tentativas de transformações, bem como agregações. Até mesmo conseguir identificar os valores equivocados na tabela. Desenvolvendo a transformação durante as expressões e ao final do processo gerou um melhor resultado.

Muitos dos valores nulos ou faltantes da tabela de acidentes em um primeiro momento podem atrapalhar as análises, mas podem ser resolvidos com a introdução de ferramentas como machine learning.
A maioria dos dados faltantes se encontram nas colunas "br"(o número da rodovia), "km", "sentido" e "tracado_via". Br e Km por associação com as colunas de "municipio", "uf", "latitude" e "longitude" podem ser rapidamente preenchidas.
A coluna "tracado_via" com auxílio de outras ferramentas de inteligência artifical, imagens de mapa, "latitude" e "longitude" também pode ser preenchida.
Já os valores do "sentido" quando envolvem pista dupla ficam mais difíceis de imprimir a realidade. Mas podendo ser preenchida por decisões humanas em estatísticas.

