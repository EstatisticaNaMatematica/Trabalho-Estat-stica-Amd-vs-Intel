# Relatório de Análise Estatística 

**Tema**: *\PROCESSADORES, AMD VS INTEL*  
**Autores**: *\Olavo Francisquini, Vinicius Pedro Manzoni Barros*  
**Data**: *\28/06/2025*

## 1\. Introdução

Este relatório apresenta uma análise estatística do conjunto de dados AMD vs INTEL. O objetivo principal é analisarmos os processadores referente ao banco de dados levantado, para que possamos comparar os desempenhos dos processadores, a média entre os valores encontrados, e qual máquina terá o melhor desempenho com o melhor custo benefício. Utilizaremos estatítica descritiva, probabilidade e inferência estatítica. 
-----

## 2\. Descrição do Conjunto de Dados

* Fonte dos dados:[Link para Dataset](https://www.kaggle.com/datasets/alanjo/amd-processor-specifications)
* Número de observações (linhas): 61
* Número de variáveis (colunas): 8

### 2.1. O que representam os dados?

Este conjunto de dados contém informações sobre processadores, dentre essas informações elas descrevem, Cache, Núcleo (CORE), Trheads, Velocidade de Frequência (SPEED GHZ), Preço (PRICE), e foi obtido a partir de um repositório público disponível no Kaggle.

| Coluna | Descrição | Tipo de Dado | Exemplo |
|---|---|---|---|
| Cores| Quantidade de Núcleos do Processador (CPI)| Numérico | 32,24,16 |
| Trheads | Quantidade de Trheads do Processador (CPU)| Numérico | 64,48,32 |
| Speed| Quantidade de Velocidade em GHZ do Processador (CPU) | Numérico | 3.0,3.2,3.5 |
| ... | ... | ... | ... |

### 2.2. Como os dados foram obtidos?

O banco de dados foi obtido na plataforma Kaggle e contém especificações técnicas de processadores das marcas AMD e Intel. Ele reúne informações como quantidade de núcleos (cores), número de threads, tamanho da memória cache (em MB), velocidade de clock (em GHz), preço estimado e o nome do modelo do processador.
No caso da AMD, estão presentes processadores das famílias Ryzen, Threadripper e FX. Já a Intel está representada por suas linhas mais conhecidas, como Core i5, i7, i9 e Xeon.
Esse conjunto de dados é útil para comparações de desempenho e custo-benefício entre as duas marcas, sendo uma ferramenta relevante para entusiastas, pesquisadores e profissionais da área de tecnologia. As informações provavelmente foram compiladas a partir de fontes públicas como sites oficiais dos fabricantes e varejistas de hardware. Onde tivemos um pré-processamento para a construção de uma nova coluna sendo ela intitulada MARCA.


-----

## 3\. Questões Motivadoras

Nesta análise, buscamos responder às seguintes questões/problemas:

  * **Questão 1:** Onde pode facilitar, a compra para algumas pessoas referente a essas duas marcas.
  * **Questão 2:** Curiosidade sobre algumas informações, por exemplo desempenho, custo benefício, e que nem citado antes, auxilio para comprar quaisquer desses CPU's analisados.
  

-----

## 4\. Códigos Utilizados

Todos os códigos para esta análise foram desenvolvidos em **R**.

Todos os códigos em R usados na análise estão incluídos abaixo.
Para formatar blocos de código em Markdown no GitHub, use três crases (\`\`\`) seguidas da linguagem (`r` para R):

```r
# Carregar pacotes
library(tidyverse)

# Leitura dos dados
dados <- read.csv("dados.csv")

# Visualizar os primeiros registros
head(dados)
```

```r
# Carregando pacotes necessários
library(ggplot2)
library(dplyr)
library(knitr) # Para tabelas bonitas
library(Tidyverse) # Pacote para manipulação de dados
library(stats) # Para funções estatísticas

# Exemplo de carregamento de dados
dados <- read.csv("dados_exemplo.csv")

# Exemplo de visualização das primeiras linhas do dataframe
head(dados)

# Exemplo de cálculo de estatísticas descritivas
summary(dados$ColunaNumerica)

# Exemplo de um gráfico de dispersão
ggplot(dados, aes(x = ColunaX, y = ColunaY)) +
  geom_point() +
  labs(title = "Gráfico de Dispersão de X vs Y",
       x = "Eixo X",
       y = "Eixo Y") +
  theme_minimal()

# Exemplo de teste t
t_test_resultado <- t.test(dados$GrupoA, dados$GrupoB)
print(t_test_resultado)

```

-----

## 5\. Figuras Geradas e Explicações

Insira aqui gráficos com breve explicação. Para adicionar imagens no Markdown do GitHub:

```markdown
![Texto alternativo](caminho/para/imagem.png)
```

### 5.1. Histograma da Variável [Nome da Variável]

  * **Explicação:** Este histograma mostra a distribuição da variável `Idade`. Observa-se que [descreva as principais características da distribuição, ex: a maioria dos indivíduos está na faixa de 30-40 anos, a distribuição é levemente assimétrica à direita, etc.]. Isso é importante para entender [justifique a relevância da visualização, ex: a composição etária da nossa amostra, a presença de outliers, etc.].

### 5.2. Gráfico de Dispersão entre [Variável X] e [Variável Y]

  * **Explicação:** O gráfico de dispersão acima ilustra a relação entre as variáveis `Variável X` e `Variável Y`. É possível observar [descreva a tendência, ex: uma correlação positiva, negativa, ausência de correlação, agrupamentos, etc.]. Esta visualização auxilia na [justifique a relevância, ex: identificação de padrões, detecção de relações lineares ou não lineares, etc.].

### 5.3. Gráfico de Barras da Variável Categórica [Nome da Variável]

  * **Explicação:** Este gráfico de barras apresenta a frequência de cada categoria da variável `Região`. [Descreva o que o gráfico mostra, ex: a maioria dos dados pertence à "Região Sul", enquanto a "Região Norte" possui a menor representatividade]. Essa visualização é crucial para [justifique a relevância, ex: entender a distribuição das categorias, identificar desequilíbrios na amostra, etc.].

-----

## 6\. Justificativa de Utilização de Cada Medida

### 6.1. Medidas de Tendência Central (Média, Mediana, Moda)

  * **Média:** Utilizada para [justifique a escolha, ex: fornecer uma visão geral do valor "típico" em distribuições aproximadamente simétricas, pois é sensível a valores extremos].
  * **Mediana:** Empregada para [justifique a escolha, ex: representar o valor central em distribuições assimétricas ou com outliers, pois não é afetada por valores extremos].
  * **Moda:** Aplicada para [justifique a escolha, ex: identificar o valor mais frequente em variáveis categóricas ou discretas, sendo útil para entender a categoria mais comum].

### 6.2. Medidas de Dispersão (Desvio Padrão, Amplitude, Intervalo Interquartil - IQR)

  * **Desvio Padrão:** Escolhido para [justifique a escolha, ex: quantificar a dispersão dos dados em relação à média, sendo útil em distribuições normais ou aproximadamente normais].
  * **Amplitude:** Utilizada para [justifique a escolha, ex: fornecer uma medida rápida da variação total dos dados, indicando a diferença entre o valor máximo e mínimo].
  * **Intervalo Interquartil (IQR):** Aplicado para [justifique a escolha, ex: medir a dispersão dos 50% centrais dos dados, sendo robusto a outliers e útil em distribuições assimétricas].

### 6.3. Medidas de Posição (Quartis, Percentis)

  * **Quartis/Percentis:** Empregados para [justifique a escolha, ex: dividir os dados em partes iguais, permitindo analisar a distribuição e identificar a posição relativa de valores, útil para identificar outliers e entender a cauda da distribuição].

### 6.4. Medidas de Associação (Coeficiente de Correlação de Pearson/Spearman)

  * **Coeficiente de Correlação de Pearson:** Utilizado para [justifique a escolha, ex: medir a força e direção de uma relação linear entre duas variáveis numéricas, assumindo normalidade].
  * **Coeficiente de Correlação de Spearman:** Empregado para [justifique a escolha, ex: medir a força e direção de uma relação monotônica entre duas variáveis, sem assumir normalidade, sendo robusto a outliers e útil para dados ordinais].

-----

## 7\. Testes Estatísticos Utilizados

### 7.1. Teste [Nome do Teste, ex: Teste t de Student para duas amostras independentes]

  * **Objetivo:** [Descreva o objetivo do teste, ex: Comparar as médias de duas amostras independentes para determinar se há uma diferença estatisticamente significativa entre elas.]
  * **Hipóteses:**
      * **H0 (Hipótese Nula):** [Descreva a hipótese nula, ex: Não há diferença significativa entre as médias dos grupos.]
      * **H1 (Hipótese Alternativa):** [Descreva a hipótese alternativa, ex: Há uma diferença significativa entre as médias dos grupos.]
  * **Resultado:**
    ```
    # Código R do teste
    t.test(dados$VariávelNumérica ~ dados$VariávelCategórica, data = dados)
    ```
      * **P-valor:** [Valor do p-valor]
      * **Interpretação:** [Com base no p-valor e nível de significância, ex: Com um p-valor de [X] e um nível de significância de 0.05, rejeitamos/não rejeitamos a hipótese nula. Isso indica que há/não há evidências suficientes para afirmar uma diferença significativa entre as médias dos grupos.]

### 7.2. Teste [Nome do Teste, ex: Análise de Variância (ANOVA)]

  * **Objetivo:** [Descreva o objetivo do teste, ex: Comparar as médias de três ou mais grupos para determinar se há uma diferença estatisticamente significativa entre elas.]
  * **Hipóteses:**
      * **H0:** [Descreva a hipótese nula, ex: As médias de todos os grupos são iguais.]
      * **H1:** [Descreva a hipótese alternativa, ex: Pelo menos uma média de grupo é diferente das outras.]
  * **Resultado:**
    ```r
    # Código R do teste
    modelo_aov <- aov(VariávelResposta ~ Fator, data = dados)
    summary(modelo_aov)
    ```
      * **P-valor:** [Valor do p-valor]
      * **Interpretação:** [Com base no p-valor, ex: Dado o p-valor de [X], menor que 0.05, rejeitamos a hipótese nula, indicando que existe uma diferença significativa entre as médias de pelo menos um grupo.]

-----

## 8\. Análise e Discussão dos Resultados Obtidos

Nesta seção, discuta os achados mais importantes da sua análise em relação às questões motivadoras. Não apenas reporte os números, mas interprete-os e conecte-os ao contexto do problema.

  * **Para a Questão 1 ([Reformule a questão]):**

      * [Apresente os principais achados relacionados a essa questão. Ex: Os resultados do teste t indicaram uma diferença estatisticamente significativa na média de [Variável Resposta] entre os grupos A e B (p \< 0.05). O Grupo A apresentou uma média [maior/menor] de [Valor] em comparação com o Grupo B, que teve uma média de [Valor].]
      * [Discuta as implicações desses achados. Ex: Isso sugere que [implicação prática, ex: a intervenção X realmente teve um impacto positivo/negativo].]

  * **Para a Questão 2 ([Reformule a questão]):**

      * [Apresente os resultados dos modelos ou análises. Ex: O modelo de regressão linear múltipla revelou que [Variável Preditiva X] é um preditor significativo de [Variável Resposta] (coeficiente = [Valor], p \< 0.01), enquanto [Variável Preditiva Y] não se mostrou significativa.]
      * [Discuta o significado prático e teórico desses achados. Ex: Este achado confirma que [ideia central] e pode ser usado para [aplicação prática].]

  * **Para a Questão 3 ([Reformule a questão]):**

      * [Descreva os padrões ou agrupamentos encontrados. Ex: A análise exploratória de dados, como o gráfico de dispersão, sugeriu a existência de dois grupos distintos de dados, com diferentes comportamentos em relação às variáveis X e Y. Isso foi corroborado por [mencione outro teste ou análise se aplicável].]
      * [Analise as possíveis razões para esses padrões. Ex: Acreditamos que esses grupos possam representar [explicação, ex: diferentes segmentos de clientes, condições experimentais distintas, etc.].]

-----

## 9\. Conclusão

Este relatório explorou o conjunto de dados [Nome do Conjunto de Dados] com o objetivo de [reafirme o objetivo geral]. As principais descobertas incluem:

  * [Resumo do principal achado 1, ex: Houve uma diferença significativa em [Variável] entre os grupos A e B.]
  * [Resumo do principal achado 2, ex: [Variável X] foi um preditor significativo de [Variável Y].]
  * [Resumo do principal achado 3, ex: Foram identificados dois padrões distintos nos dados, sugerindo a presença de subgrupos.]

Esses resultados têm implicações para [mencione as implicações práticas ou teóricas, ex: a tomada de decisão em marketing, o desenvolvimento de novas políticas, a compreensão de um fenômeno, etc.].

### Limitações e Trabalhos Futuros

É importante notar que [mencione quaisquer limitações da análise, ex: o tamanho da amostra, a ausência de algumas variáveis importantes, vieses nos dados, etc.].

Para trabalhos futuros, sugerimos:

  * [Sugestão de pesquisa futura 1, ex: Coletar mais dados para aumentar a robustez das análises.]
  * [Sugestão de pesquisa futura 2, ex: Explorar modelos mais complexos, como machine learning, para previsões mais precisas.]
  * [Sugestão de pesquisa futura 3, ex: Realizar análises de sensibilidade para avaliar a robustez dos resultados a diferentes suposições.]

-----

## Referências / Links Úteis

  * [Conjunto de Dados Original](https://www.google.com/search?q=https://example.com/link_para_dados)
  * [Documentação do Pacote ggplot2](https://ggplot2.tidyverse.org/)
  * [Guia de Markdown para GitHub](https://docs.github.com/pt/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

-----

### Dicas de Formatação Markdown para GitHub:

  * **Títulos:** Use `#` para o título principal, `##` para subtítulos, `###` para sub-subtítulos, e assim por diante.
  * **Texto em negrito:** Use `**texto**` ou `__texto__`.
  * **Texto em itálico:** Use `*texto*` ou `_texto_`.
  * **Listas não ordenadas:** Use `*` ou `-` seguido de um espaço.
    ```markdown
    * Item 1
    * Item 2
        * Subitem 2.1
    ```
  * **Listas ordenadas:** Use números seguidos de um ponto e um espaço.
    ```markdown
    1. Primeiro item
    2. Segundo item
    ```
  * **Blocos de código:** Use três crases (\`\`\`\`\`) antes e depois do seu bloco de código e especifique a linguagem para destaque de sintaxe.
    ````markdown
    ```R
    # Seu código R aqui
    print("Olá Mundo!")
    ```
    ````
  * **Código inline:** Use uma crase (`` ` ``) ao redor do texto. Exemplo: `print("Olá")`.
  * **Links:** Use `[Texto do link](URL do link)`. Exemplo: `[Google](https://www.google.com)`.
  * **Imagens:** Use `![Texto alternativo da imagem](URL da imagem)`. Para imagens locais no seu repositório GitHub, use caminhos relativos: `![Gráfico](img/grafico1.png)`.
  * **Tabelas:** Use `|` para separar colunas e `-` para a linha de cabeçalho.
    ```markdown
    | Cabeçalho 1 | Cabeçalho 2 |
    |---|---|
    | Linha 1 Coluna 1 | Linha 1 Coluna 2 |
    | Linha 2 Coluna 1 | Linha 2 Coluna 2 |
    ```
  * **Linhas horizontais:** Use três ou mais hifens (`---`), asteriscos (`***`) ou underscores (`___`) em uma linha separada.
