# Python Insights: Análise de Cancelamento de Clientes

## Descrição

Este projeto realiza uma análise de dados sobre o cancelamento de clientes de uma empresa, utilizando Python com as bibliotecas Pandas e Plotly. O objetivo é identificar os principais motivos pelos quais os clientes cancelam seus serviços e propor ações para reduzir a taxa de cancelamento.

## Passo a Passo

1.  **Importar a base de dados:**
    *   Utiliza a biblioteca Pandas para ler um arquivo CSV (`cancelamentos_sample.csv`) que contém os dados dos clientes.
    *   Imprime a tabela inicial para visualização.

2.  **Visualizar a base de dados:**
    *   O código imprime a tabela inicialmente, mas essa etapa está mais detalhada na descrição para o usuário, em vez de código.

3.  **Tratar a base de dados:**
    *   **Remover informações inúteis:** Remove a coluna "CustomerID" da tabela.
    *   **Lidar com valores vazios:** Remove as linhas que contêm valores nulos na tabela.
    *   **Verificar Formato dos Dados:** Verifica se o formato dos dados nas colunas é apropriado (como não foram encontradas falhas, esse passo não envolveu código)

4.  **Analisar o cancelamento dos clientes:**
    *   Calcula e exibe a contagem de clientes que cancelaram (`cancelou = True`) e que não cancelaram (`cancelou = False`).
    *   Calcula e exibe a porcentagem de clientes que cancelaram em relação ao total de clientes.

5.  **Analisar as causas do cancelamento dos clientes:**
    *   Utiliza a biblioteca Plotly para criar histogramas que mostram a relação entre as variáveis (duração do contrato, ligações para o call center, dias de atraso) e o cancelamento.
    *   Com base nos gráficos, são identificadas possíveis causas para os cancelamentos:
        *   Clientes com contrato mensal cancelam com mais frequência.
        *   Clientes que ligam mais de 4 vezes para o call center tendem a cancelar.
        *   Clientes com mais de 20 dias de atraso também tendem a cancelar.

6.  **Aplicar Filtros:**
    *   Cria uma nova tabela filtrando os dados para clientes que não cancelaram com contratos mensais, não fizeram mais de 4 ligações para o call center e não possuem atrasos superiores a 20 dias.
    *   Calcula e exibe a contagem e porcentagem de clientes que cancelaram após a aplicação dos filtros.

## Tecnologias Utilizadas

*   **Linguagem de Programação:** Python
*   **Biblioteca de Análise de Dados:** Pandas (para manipulação e análise de dados)
*   **Biblioteca de Visualização de Dados:** Plotly (para criar gráficos interativos)

## Como Executar

1.  **Requisitos:**
    *   Python 3.6 ou superior
    *   Bibliotecas Pandas, NumPy, Openpyxl, nbformat, ipykernel e Plotly instaladas.
        *   Para instalar, execute:

            ```bash
            pip install pandas numpy openpyxl nbformat ipykernel plotly
            ```
2.  **Clonar Repositório:** Clone o repositório para sua máquina.
3.  **Executar o script:** Execute o arquivo Python com o código (o nome do arquivo é variável).

    ```bash
    python nome_do_arquivo.py
    ```

## Estrutura do Projeto

*   `nome_do_arquivo.py`: Arquivo principal com o código Python para a análise.
*    `cancelamentos_sample.csv`: Arquivo CSV com os dados dos clientes (exemplo)

## Funcionamento do Código Python
*   O código começa importando as bibliotecas necessárias: Pandas para manipulação de dados e Plotly para visualização.
*   O DataFrame é carregado via Pandas e o arquivo CSV.
*   As colunas irrelevantes (CustomerID) e as linhas com valores nulos são retiradas.
*   É feita a análise das ocorrências de cancelamento, e a sua porcentagem.
*   Os histogramas são gerados para cada coluna de dados para se analisar quais colunas tem mais impacto no cancelamento.
*   Com base na análise dos histogramas, são criados os filtros no DataFrame, excluindo os clientes mais propensos a cancelarem.
*   É feita a nova análise do dataset filtrado, das ocorrências de cancelamento, e a sua porcentagem.

## Contribuindo

Se você deseja contribuir com este projeto, sinta-se à vontade para:

*   Reportar bugs ou sugerir melhorias através de issues.
*   Enviar pull requests com suas modificações.

## Autor

*   Rilson Joás

## Observações

*   Este projeto é um exemplo simplificado de análise de dados com Python.
*   As recomendações geradas a partir das análises são de alto nível e requerem um refinamento para ações mais efetivas.
*   A biblioteca Plotly é utilizada para criar gráficos interativos, que podem ser explorados mais a fundo pelo usuário.
*   O código pode ser adaptado e expandido para incluir outras variáveis e análises.
*   O arquivo `cancelamentos_sample.csv` deve existir para executar o código.

```python
# Passo a passo
# !pip install pandas numpy openpyxl nbformat ipykernel plotly

#1. Importar a base de dados

import pandas as pd

tabela= pd.read_csv('cancelamentos_sample.csv')
print(tabela)

#2. Visualizar a base de dados

#3. Tratar a base de dados

# - Se livrar de informações inúteis

tabela = tabela.drop(columns="CustomerID")
display(tabela)

# - Lidar com valores vazios

tabela = tabela.dropna()
display(tabela.info())

# - Formato está correto?
# Sim, está para todos os campos de dados. 
#4. Analisar o cancelamento dos clientes

display(tabela["cancelou"].value_counts())

display(tabela["cancelou"].value_counts(normalize=True))

#5. Analisar a causa do cancelamento dos clientes

#Importar a biblioteca Plotly

import plotly.express as px

#Criar um gráfico

for coluna in tabela:
    grafico = px.histogram(tabela, x=coluna, color="cancelou")
    grafico.show()
# clientes do contrato mensal TODOS cancelam
    # ofercer desconto nos planos anuais e trimestrais
# clientes que ligam mais do que 4 vezes para o call center, cancelam
    # criar um processo para resolver o problema do cliente em no máximo 3 ligações
# clientes que atrasaram mais de 20 dias, cancelaram
    # política de resolver atrasos em até 10 dias (equipe financeira)

tabela = tabela[tabela["duracao_contrato"]!="Monthly"]
tabela = tabela[tabela["ligacoes_callcenter"]<=4]
tabela = tabela[tabela["dias_atraso"]<=20]

display(tabela["cancelou"].value_counts())
# em percentual
display(tabela["cancelou"].value_counts(normalize=True))
```
