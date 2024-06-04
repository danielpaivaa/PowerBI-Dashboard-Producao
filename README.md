# Criando um Dashboard de Produção em Power BI

## Introdução

Estou criando um dashboard de produção a partir de um conjunto de dados fictício. Este dashboard oferece insights sobre o desempenho de produção da empresa, incluindo total produzido, total rejeitado, taxa de qualidade, dentre outros.

## Passo a Passo para Criar o Dashboard

### Importação e Transformação dos Dados

- **Passos de Transformação:**
  - **Remoção de dados nulos:** As colunas e linhas nulas foram removidas da base de dados.
  - **Alteração dos tipos de dados:** Após verificação, observou-se que os tipos de dados não correspondiam ao desejado e, assim, foi feita a alteração.

- **Criando novas medidas com DAX:**
  - **Total Produzido:** Medida criada a partir da coluna `Qtd Produzida` utilizando a função `SUM()`. 
    > *Total Produzido = SUM('BaseProdução'[Qtd Produzida])*
  - **Total Rejeitado:** Medida criada a partir da coluna `Qtd Rejeitada` utilizando a função `SUM()`.
    > *Total Rejeitado = SUM('BaseProdução'[Qtd Rejeitada])*
  - **Taxa de Qualidade:** Medida criada a partir do cálculo entre as medidas: `Total Produzido` e `Total Rejeitado`.
    > *Taxa de Qualidade = [Total Produzido] / ([Total Produzido] + [Total Rejeitado])*
  - **Horas Produtivas:** Medida criada a partir das colunas `Total Horas` e `Qtd Produzida`, utilizando as funções `CALCULATE()` e `SUM()`.
    > *Horas Produtivas = CALCULATE(SUM('BaseProdução'[Total Horas]), 'BaseProdução'[Qtd Produzida] > 0)*
  - **Horas Improdutivas:** Medida criada a partir das colunas `Total Horas` e `Qtd Produzida`, utilizando as funções `CALCULATE()` e `SUM()`.
    > *Horas Improdutivas = CALCULATE(SUM('BaseProdução'[Total Horas]), 'BaseProdução'[Qtd Produzida] == 0)*
  - **Horas Trabalhadas:** Medida criada a partir da coluna `Total Horas` utilizando a função `SUM()`.
    > *Horas Trabalhadas = SUM('BaseProdução'[Total Horas])*
  - **Taxa de Produtividade:** Medida criada a partir do cálculo entre as medidas: `Horas Produtivas` e `Horas Trabalhadas`.
    > *Taxa de Produtividade = [Horas Produtivas] / [Horas Trabalhadas]*
  - **Taxa de Rejeição:** Medida criada a partir do cálculo entre as medidas: `Horas Improdutivas` e `Horas Trabalhadas`.
    > *Taxa de Rejeição = [Horas Improdutivas] / [Horas Trabalhadas]*

## Interpretação dos Insights

## Dashboard
![Painel de Análise de Vendas](arquivos/Aula%202.png)

### Total Produzido
- **Insight**: Com um total produzido de 3.084.251 itens, o desempenho da produção é alto, refletindo uma boa capacidade produtiva.

### Total Rejeitado
- **Insight**: Com 21.076 itens rejeitados, é essencial investigar as causas das rejeições para melhorar a qualidade.

### Horas Produtivas e Improdutivas
- **Insight**: A proporção de horas produtivas (31.331) em relação às horas improdutivas (8.515) indica uma boa utilização do tempo, mas há espaço para melhorias.

### Taxa de Produtividade
- **Insight**: A taxa de produtividade de 78,63% é sólida, mas identificar e reduzir as causas das horas improdutivas pode aumentar essa taxa.

### Total Produzido por Mês
- **Insight**: A variação no total produzido ao longo dos meses mostra picos e vales que podem estar associados a fatores sazonais ou operacionais.

### Contagem de Ocorrências por Tipo de Ocorrência
- **Insight**: As ocorrências mais comuns, "Controle de Qualidade" e "Preparação de Máquina", precisam ser monitoradas e mitigadas para reduzir o impacto na produção.

### Taxa de Qualidade
- **Insight**: Com uma taxa de qualidade de 99,32%, a produção mantém um alto padrão de qualidade, embora ainda haja margem para pequenas melhorias.

## Considerações sobre a Base de Dados

A base de dados utilizada contém as seguintes colunas:

- **Número da Ordem:** Identificação da ordem de produção.
- **Operador:** Nome do operador responsável.
- **Produto:** Nome do produto fabricado.
- **Ocorrência:** Tipo de ocorrência registrada.
- **Data de Início:** Data de início da produção.
- **Hora de Início:** Hora de início da produção.
- **Data de Término:** Data de término da produção.
- **Hora de Término:** Hora de término da produção.
- **Total de Horas:** Total de horas trabalhadas.
- **Qtd Produzida:** Quantidade total produzida.
- **Qtd Rejeitada:** Quantidade total rejeitada.