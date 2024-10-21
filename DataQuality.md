# Agendamento de DataQuality

## Aqui irei apresentar um passo a passo de como criar um agendamento de Verificação de Qualidade de Dados

### 1. No console do Google Cloud Dataplex, acesse a página Qualidade dos dados.
<img width="928" alt="passo1" src="https://github.com/user-attachments/assets/2e3d9d87-fab6-4d5d-b576-11f87e4f4365">

### 2. Clique em Criar verificação de qualidade de dados.
<img width="959" alt="passo2" src="https://github.com/user-attachments/assets/fdff1225-2297-4dd2-b82a-69ea69356e51">

3. Na janela Definir verificação, preencha os seguintes campos:

- a. Digite um Nome de exibição.

- b. O ID de verificação será gerado automaticamente se você não fornecer um ID próprio. Consulte a convenção de nomenclatura de recursos.

- c. No campo Tabela, clique em Procurar, escolha sua tabela e clique em Selecionar. O Dataplex só oferece suporte a padrões tabelas do BigQuery.

     Para tabelas em conjuntos de dados multirregionais, escolha uma região onde criar na verificação de dados.

     Para navegar pelas tabelas organizadas no lake do Dataplex, Clique em Procurar nos lakes do Dataplex.

- d. No campo Escopo, escolha Incremental ou Dados inteiros.
     Se você escolher Incremental: no campo Coluna de carimbo de data/hora, selecione uma coluna do tipo DATE ou TIMESTAMP na tabela do BigQuery que aumenta monotonicamente       e pode ser usada para identificar novos registros. Pode ser uma coluna que particiona a tabela.
 <img width="364" alt="passo3" src="https://github.com/user-attachments/assets/29fd4795-06b5-4dd9-bd50-86ef3860d952">

- e. Para criar uma amostra dos seus dados, na lista Tamanho da amostragem, selecione um a porcentagem de amostragem. Escolha um valor de porcentagem entre 0,0% e 100,0% com       até três dígitos decimais. Para dispositivos maiores conjuntos de dados, escolha uma porcentagem de amostragem mais baixa. Por exemplo, para um Tabela de             
      aproximadamente 1 PB. Se você inserir um valor entre 0,1% e 1,0%, O Dataplex faz amostras entre 1 e 10 TB de dados. Para verificações de dados incrementais, o Dataplex       aplica a amostragem incremento mais recente.

Os resultados da verificação mais recente podem ser acessados na guia Qualidade de dados no Páginas do BigQuery e do Data Catalog para a origem tabela.

4. Na janela Programar, escolha uma das seguintes opções:

- Repetir: execute o job de verificação de qualidade de dados em uma programação: diária, semanal, mensal ou personalizada. Especificar com que frequência a verificação é executada e em que horário. Se você escolher personalizado, use o cron. para especificar a programação.

- Sob demanda: execute o job de verificação de qualidade de dados sob demanda.

Clique em Continuar.

![passo4](https://github.com/user-attachments/assets/072741fa-a723-48da-90ce-6ac8e699157e)

5. Na janela Regras de qualidade de dados, defina as regras para configurar para esta verificação da qualidade de dados. Clique em Adicionar regras e escolha uma das opções a seguir.

### Recomendações com base no perfil 
Crie regras na com base em uma verificação de criação de perfil de dados atual.

- ***Escolher colunas***: selecione as colunas para receber regras recomendadas.

- ***Verificar projeto***: recomendações com base em dados atuais a verificação de criação de perfil. Por padrão, o Dataplex seleciona a criação de perfil do mesmo projeto em que você está criando os dados verificação de qualidade. Se você criou a verificação em um projeto diferente, especifique o projeto para extrair as verificações de perfil.

- ***Escolha os resultados do perfil***: com base nas colunas e no projeto que você selecionar, vários resultados de perfil serão exibidos.

Selecione um ou mais resultados de perfil e clique em OK. Isso preenche uma lista de regras para seleção.

Para selecionar as regras que você quer editar, marque as caixas e clique em Selecionar. Depois de selecionadas, as regras são adicionadas à sua regra atual lista. Em seguida, você pode editar as regras.

<img width="563" alt="Recomenção com base no perfil" src="https://github.com/user-attachments/assets/d33df0a2-c6f6-4c9a-9b09-b18a6edeeefa">

### Tipos de regra integrados 
Crie regras com base em regras predefinidas. Veja a lista de regras predefinidas.

- ***Escolher colunas***: selecione as colunas para as quais as regras serão aplicadas.

- ***Escolha os tipos de regras***: com base nas colunas selecionadas, vários tipos de regras aparecem para seleção.

Selecione um ou mais tipos de regra e clique em OK. Isso preenche uma lista de regras para seleção.

Marque as caixas para escolher as regras que você quer editar e clique em Selecionar. Depois de selecionadas, as regras são adicionadas à sua lista atual. Depois, edite as regras.

| Tipo de Regra | Descrição | Tipos de coluna compatíveis |
|---------------|-----------|-----------------------------|             
|NonNullExpectation(Verificação de valores nulos)|Valide se os valores da coluna não são nulos|Todos os tipos de colunas aceitos|
|SetExpectation(Defina a verificação)|Verifica se os valores em uma coluna são um dos valores especificados em um conjunto|Todos os tipos de coluna com suporte, exceto Record e Struct|
|RegexExpectation(Verificação de expressão regular)|Verifique os valores em relação a uma expressão regular especificada|String|
|Uniqueness(Verificação de exclusividade)| Verifique se todos os valores em uma coluna são únicos|Todos os tipos de coluna com suporte, exceto Record e Struct|
|RangeExpectation(Verificação de intervalo)|Verifique se o valor está entre o mínimo e o máximo|Todas as colunas do tipo numérico, de data e de carimbo de data/hora|
|StatisticRangeExpectation(Verificação de estatística)|Verifique se a medida estatística fornecida corresponde à expectativa do intervalo|Todos os tipos de colunas numéricas aceitos|

### Regra de verificação de linha do SQL
Criar uma regra SQL personalizada para aplicar a cada linha (SQL personalizado) regra de verificação de linha). 

  a. Em Dimensão, escolha uma dimensão.

  b. Em Limite de aprovação, escolha uma porcentagem de registros que precisam passar na verificação.

  c. Em Nome da coluna, escolha uma coluna.

  d. No campo Fornecer uma expressão SQL, insira uma expressão SQL. que resulte em um booleano true (aprovado) ou false (reprovado). Para mais informações, consulte Tipos de regras SQL personalizadas com suporte e os exemplos na seção Definir regras de qualidade de dados deste documento.

  e. Clique em Adicionar.

### Regra de verificação agregada do SQL 
Criar um SQL personalizado regra de condição de tabela.

  a. Em Dimensão, escolha uma dimensão.

  b. Em Nome da coluna, escolha uma coluna.

  c. No campo Fornecer uma expressão SQL, insira uma expressão SQL. que resulte em um booleano true (aprovado) ou false (reprovado). Para mais informações, consulte Tipos de regras SQL personalizadas com suporte e os exemplos em Definir regras de qualidade de dados deste documento.

  d. Clique em Adicionar.

### Regra de declaração SQL 
Criar uma regra de declaração SQL personalizada para verificar para um estado inválido dos dados.

  a. Em Dimensão, escolha uma dimensão.

  b. Opcional: em Nome da coluna, escolha uma coluna.

  c. No campo Fornecer uma instrução SQL, insira uma instrução SQL. que retorna linhas que correspondem ao estado inválido. Se alguma linha for retornada, essa regra falhará. Omita o ponto e vírgula final da instrução SQL. Para mais informações, consulte Tipos de regras SQL personalizadas com suporte e os exemplos em Definir regras de qualidade de dados deste documento.

6. Opcional: exportar os resultados da verificação para um padrão do BigQuery tabela. Clique em Procurar para selecionar um BigQuery para armazenar os resultados da verificação da qualidade de dados.
<img width="449" alt="passo6" src="https://github.com/user-attachments/assets/ee27c8d1-cbe3-4665-bf69-23bbc6e6c8c5">

7. Clique em criar.

## Como ver o histórrco de resultados das verificações

1. No console do Google Cloud, acesse a página Qualidade de dados.

2. Clique no nome de uma verificação.

3. Clique na guia Histórico de jobs.
<img width="723" alt="historico" src="https://github.com/user-attachments/assets/9cd708c9-4c36-47c7-88d7-3334a705056a">

A guia Histórico de jobs fornece informações sobre jobs anteriores. Ele lista todos os jobs, o número de registros verificados em cada job, o status do job, o horário em que o job foi executado, se cada regra foi aprovada ou falhou e muito mais.

4. Clique no ID do Job
<img width="794" alt="idhistorico" src="https://github.com/user-attachments/assets/d73bdc01-3117-4a9c-a957-9e9803a82ec9">

- Aqui você terá acesso aos detalhes do Job

<img width="743" alt="detalheshisotirco" src="https://github.com/user-attachments/assets/28991107-95ad-4def-a8a4-f038b6b69691">
