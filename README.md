# tcc_bi_master

As etapas de coleta de dados (que compreende o download de arquivos CSV e web scraping dos sites da B3 e CVM), de tratamento dos dados coletados e da criação do banco de dados em SQLite foram realizadas através de um jupyter notebook em python 3. Foram utilizadas as seguintes bibliotecas: numpy, time, datetime, pandas, string, wget, zipfile, random, sqlite3 e selenium.

A CVM disponibiliza diversos formulários de demonstrações financeiras desde o ano de 2011 no site http://dados.cvm.gov.br. A etapa de coleta de dados no site da CVM consiste em fazer o download dos arquivos e concatená-los para posterior ingestão no banco de dados.

A B3 também disponibiliza informações no site www.b3.com.br. As séries históricas são disponibilizadas em arquivos CSV em séries anuais, mensais ou diárias. Estes arquivos estão formatados por largura de coluna de forma que há necessidade de ajustar estes arquivos conforme layout disponível no site da B3. Após este pré-processamento os arquivos são concatenados para posterior importação no banco de dados. Por outro lado, dados básicos das empresas listadas na B3 não estão disponíveis através de arquivos CSV. Assim, é necessário empregar a técnica de web scraping para extrair informações básicas das empresas (código CVM, CNPJ, razão social, site, código de negociação etc). O site da B3 emprega muito a linguagem javascript e iframes dentro de iframes de forma que a extração destas informações não é uma tarefa trivial. Felizmente, o pyhton possui a biblioteca selenium que permite renderizar em um browser, simulando a navegação realizada por ser humano, ao mesmo tempo que coleta as informações. Todas estas informações foram salvas num arquivo CSV.

Após a coleta e tratamentos dos dados, os arquivos CSVs criados foram importados em um banco de dados SQLite.

Com o banco de dados criado, a última etapa é criar uma conexão entre o banco de dados e o Power Bi. O Power BI não suporta nativamente o banco de dados SQLite. Para que seja possível a conexão, é preciso baixar um drive ODBC para SQLite no site http://www.ch-werner.de/sqliteodbc/. 

Para criar a conexão ao banco de dados, é preciso criar uma conexão ODBC no PowerBI, escolher SQLite no menu, informar o local do banco de dados e escolher as tabelas que serão importadas. Após a importação, são necessários alguns passos: ajustar o tipo de dados para as colunas de datas e código CVM e definir os relacionamentos.
