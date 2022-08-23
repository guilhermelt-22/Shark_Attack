# Shark Attack 

   Status do Projeto: Completo

# Objetivo 

  O objetivo do projeto é realizar a limpeza de dados do dataset 'Global Shark Attack'
  e a partir dessa limpeza direcionada, responder a pergunta: 
  *Qual espécie de tubarão é mais mortal?*

# Métodos

  - Limpeza de Dados 
  - Estatística Básica

# Tecnologias

  - Python
      - Pandas
      - Regex

# Descrição do Projeto

  O dataset 'Global Shark Attack' está disponivel em:https://www.kaggle.com/datasets/teajay/global-shark-attacks
  originalmente o dataset possui 25723 linha × 24 colunas. A limpeza foi realizada somente nas colunas:
  'Species ' e 'Fatal (Y/N)' responder a pergunta: *Qual espécie de tubarão é mais mortal?* 	

# Passos
  
  - O primeiro passo foi ler o arquivo em csv dos ataques, foi necessário utilizar o argumento encoding="cp1252" na função     pd.read_csv(), pois o arquivo não conseguia ser lido. 
  - Remoção das colunas 'Unnamed: 22' e 'Unnamed: 23', pois não possuiam informação relevante para análise.
  - Utilizando o método .info() para obter mais informação sobre o dataset, a partir da análise percebi que todas as linhas     sem informação sobre o PDF não contribuiram para a resposta  da pergunta, então decidi remover usando .dropna(subset=['pdf'])
  - Ajustei as colunas para uma formatção mais simples (usando '_' e lowercase)
  - Criação de um novo dataframe como somente as linhas com valores não nulos na coluna 'species'
  - Transformação de todos os valores na coluna 'species' em lowercase
  - Criação de uma lista com todos os tipos de tubarões usando re.findall() e uso de sets para retirar repetições
  - Criaçãod de um dicionário com todos os elementos da lista anterior como chave, como foram usadas diferentes maneiras de representar os tubarões foi necessária uma pesquisa no google para relacionar de maneira correta as chaves com nomes comuns de tubarões que seriam usadas como valores no dicionário
  - Uso de um for para realizar as substituições nos no dataframe, usando .loc[df_conhecidos['species'].str.contains(key),'species'] = value
  - Para validar os resultados das substituições procurei por opções que não foram alteradas usando .loc[~(df_conhecidos['species'].str.contains('\w+_shark')),'species'].unique()
  - Como haviam tipos de tubarões que passaram pelo filtro estabelecido no re.findall(), preenchi os que faltavam manualmente no dicionário, os tipos que não possuiam espécies definidas ou não eram tubarões foram definidos como 'desconhecida'
  - Remoção dos valores 'desconhecida' do dataframe 
  - Limpeza da coluna 'fatal_(y/n)', felizmente só haviam três tipos de informação que desviavam do estabelecido, as quais foram identificados usando .values_count(). ' N' foi associado aos valores 'N', 'M' e '2017' foram associados aos valores 'UNKNOW'
  - Após as colunas necessárias serem limpas, foi criado um novo dataframe com somente as colunas limpas, usando pd.pivot_table(), com os seguintes argumentos: index='species',columns='fatal_(y/n)', values='case_number', aggfunc='count', fill_value=0, margins=True
  - Organizei os valores pelo número de ocorrencias de ataques de maneira decrescente 
  - Nova coluna chamada mortalidade, que seria determinada por n de ocorrencias fatais/n de ocorrencias 
  - Projeto concluido 

# Conclusão
  
  Como os tubarões que possuem uma taxa de mortalidade muito alta possuem poucos ataques,
  decidi que só seriam válidos tubarões como mais de 100 ocorrências. Portanto o tubarão mais mortal é o *Tubarão Tigre*  
  
# Contato
  - Linkedin: https://www.linkedin.com/in/guilhermeteofilo/
  - Github: https://github.com/guilhermelt-22
 
