# Relatório de Análise Estatística 

**Tema**: *PROCESSADORES, AMD VS INTEL*  
**Autores**: *Olavo Francisquini, Vinicius Pedro Manzoni Barros*  
**Data**: *28/06/2025*

## 1\. Introdução

Este relatório apresenta uma análise estatística do conjunto de dados AMD vs INTEL. O objetivo principal é analisarmos os processadores referente ao banco de dados levantado, para que possamos comparar os desempenhos dos processadores, a média entre os valores encontrados, e qual máquina terá o melhor desempenho com o melhor custo benefício. Utilizaremos estatítica descritiva, probabilidade e inferência estatítica. 

-----

## 2\. Descrição do Conjunto de Dados

* Fonte dos dados: [Link para Dataset](https://www.kaggle.com/datasets/alanjo/amd-processor-specifications)
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

### 5.1. Histograma
#### 5.1.1 Histograma da Variável [Frequência AMD]
![IMAGEM HISTOGRAMA](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Histograma/histograma%20-%20frequencia%20amd.png)


 Este histograma ilustra a distribuição das frequências (em GHz) dos processadores AMD. É possível perceber que a maioria desses processadores opera entre aproximadamente 3,0 GHz e 4,0 GHz, com uma concentração mais evidente na faixa de 3,2 a 3,8 GHz.

A forma da distribuição sugere uma leve assimetria para a esquerda, já que os valores se agrupam principalmente em torno da média, mas há alguns poucos processadores com frequências menores, como 2,8 GHz, que puxam a cauda da curva nessa direção.

Além da distribuição empírica, duas curvas foram adicionadas ao gráfico para comparação com modelos teóricos. A linha vermelha representa uma distribuição normal, que parece se encaixar relativamente bem ao comportamento observado nos dados. Já a linha azul mostra uma distribuição exponencial, que claramente não representa bem esses valores, pois não acompanha a concentração central evidenciada no histograma.

Essa visualização ajuda a compreender melhor o perfil de desempenho dos processadores AMD no que diz respeito à frequência de operação. Além disso, permite avaliar se modelos estatísticos como a normal ou a exponencial são adequados para representar esse conjunto de dados, o que pode ser útil em análises comparativas, simulações ou previsões.

#### 5.1.2 Histograma da Variável [Núcleo AMD]

![IMAGEM HISTOGRAMA](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Histograma/histograma%20-%20nucleos%20amd.png)

Este histograma representa a distribuição da quantidade de núcleos dos processadores AMD. Nota-se que a maior parte dos modelos analisados possui entre 6 e 12 núcleos, o que caracteriza uma forte concentração nessa faixa. Poucos modelos apresentam quantidades mais elevadas, como 16, 24 ou 32 núcleos.

A distribuição é assimétrica à direita (positiva), indicando que há uma cauda estendida em direção a valores maiores, embora a maioria dos dados esteja concentrada em valores menores. Ou seja, a presença de processadores com muitos núcleos é menos comum, mas ainda significativa.

As curvas sobrepostas no gráfico ajudam a comparar os dados com distribuições teóricas. A curva vermelha, que representa a distribuição normal, tenta acompanhar o padrão geral, mas não representa bem a assimetria dos dados. Já a curva azul, correspondente à distribuição exponencial, oferece um ajuste mais coerente ao comportamento assimétrico da amostra, embora ainda não perfeito.

Esse tipo de visualização é essencial para compreender o perfil dos processadores AMD disponíveis no mercado, especialmente no que diz respeito ao número de núcleos, que influencia diretamente no desempenho em tarefas paralelas. Além disso, permite avaliar se há modelos estatísticos adequados para representar a distribuição dessa variável, o que pode ser útil em estudos comparativos ou previsões de desempenho.

#### 5.1.3 Histograma da Variável [Preço AMD]
![IMAGEM HISTOGRAMA](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Histograma/histograma%20-%20pre%C3%A7o%20amd.png)

Este histograma apresenta a distribuição dos preços dos processadores AMD. É possível observar que a maior parte dos modelos está concentrada na faixa de preços mais baixos, especialmente abaixo de 500 dólares. À medida que o preço aumenta, a frequência relativa dos processadores diminui consideravelmente, o que indica que os modelos mais caros são menos comuns.

A distribuição é claramente assimétrica à direita (positiva), com uma cauda longa que se estende até valores acima de 1500 dólares. Isso sugere que há alguns modelos de alto desempenho com preços elevados, mas eles representam uma minoria dentro do conjunto analisado.

As curvas adicionadas ao gráfico ajudam a avaliar o ajuste das distribuições teóricas aos dados observados. A linha vermelha, correspondente à distribuição normal, não representa bem essa assimetria, pois assume uma simetria em torno da média que não está presente. Por outro lado, a linha azul, que representa a distribuição exponencial, mostra um comportamento mais coerente com a estrutura dos dados, especialmente no início da curva, onde a frequência é mais alta.

Essa visualização é útil para compreender como os preços dos processadores AMD estão distribuídos no mercado e quais faixas de preço concentram a maior parte dos modelos. Além disso, permite avaliar qual modelo estatístico pode ser mais apropriado para representar esses dados em análises futuras.

#### 5.1.4 Histograma da Variável [Frequência Intel]
![IMAGEM HISTOGRAMA](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Histograma/histograma%20-%20frequencia%20intel.png)

O histograma acima apresenta a distribuição da variável frequência (em GHz) dos processadores Intel. Percebe-se que a maioria dos modelos está concentrada na faixa entre 3,0 GHz e 4,0 GHz, com destaque para a região entre 3,2 e 3,8 GHz, onde ocorre o maior pico de frequência relativa.

A forma da distribuição sugere uma ligeira assimetria negativa (à esquerda), com os valores mais frequentes localizados próximos à média e uma leve cauda voltada para as frequências mais baixas, por volta de 2,8 GHz. Isso indica que os modelos com frequências muito baixas são menos comuns entre os processadores Intel analisados.

As curvas sobrepostas permitem avaliar o quão bem distribuições teóricas se ajustam aos dados observados. A linha vermelha, que representa a distribuição normal, apresenta um bom ajuste, acompanhando o padrão centralizado dos dados. Por outro lado, a linha azul, correspondente à distribuição exponencial, demonstra uma baixa adequação, pois se mantém praticamente plana e não acompanha a forma do histograma.

Essa visualização ajuda a entender o comportamento das frequências de operação dos processadores Intel, o que pode ser relevante para análises comparativas com outras marcas (como AMD) e também para avaliar a aplicabilidade de modelos estatísticos na representação desses dados.

#### 5.1.5 Histograma da Variável [Núcleo Intel]
![IMAGEM HISTOGRAMA](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Histograma/histograma%20-%20nucleos%20intel.png)

Este histograma mostra a distribuição da quantidade de núcleos presentes nos processadores Intel analisados. Observa-se que a maioria dos modelos possui entre 4 e 6 núcleos, o que representa a faixa com maior frequência relativa. À medida que a quantidade de núcleos aumenta, a frequência dos modelos vai diminuindo, indicando que processadores com 10 núcleos ou mais são menos comuns.

A distribuição é claramente assimétrica à direita, com uma cauda que se estende para valores mais altos (até 18 núcleos), evidenciando a presença de alguns modelos de alto desempenho, porém em menor quantidade.

As curvas sobrepostas ajudam a visualizar como os dados se comparam com distribuições teóricas. A linha vermelha, que representa a distribuição normal, tenta seguir o padrão dos dados, mas não representa bem a assimetria observada. Já a linha azul, correspondente à distribuição exponencial, se ajusta melhor ao comportamento dos dados, especialmente na parte inicial, refletindo a queda acentuada da frequência à medida que o número de núcleos aumenta.

Essa análise permite compreender a oferta de processadores Intel em termos de capacidade de processamento paralelo, além de mostrar quais distribuições estatísticas podem melhor descrever essa variável em estudos mais aprofundados.

#### 5.1.6 Histograma da Variável [Preço Intel]
![IMAGEM HISTOGRAMA](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Histograma/histograma%20-%20pre%C3%A7o%20intel.png)
Este histograma apresenta a distribuição dos preços dos processadores Intel analisados. É possível perceber que a maior parte dos modelos se concentra na faixa de preço mais baixa, entre 0 e 1000 dólares. A frequência vai diminuindo gradualmente à medida que os preços aumentam, o que indica que processadores mais caros são bem menos comuns.

A distribuição é nitidamente assimétrica à direita, com uma cauda longa se estendendo até preços próximos de 4000 dólares, evidenciando a presença de alguns modelos premium ou de alto desempenho.

Em relação às curvas ajustadas, a linha vermelha, correspondente à distribuição normal, não representa bem o comportamento dos dados, especialmente nas extremidades. Já a linha azul, que representa a distribuição exponencial, acompanha de forma mais fiel a queda rápida na frequência dos preços mais altos, adaptando-se melhor à natureza assimétrica da distribuição.

Essa visualização ajuda a entender a disparidade de preços entre os modelos disponíveis da Intel e pode ser útil em análises de custo-benefício, posicionamento de mercado e estudos sobre acessibilidade tecnológica.

### 5.2. Gráfico de Dispersão 
#### 5.2.1 Gráfico de Dispersão entre [Frequência AMD] e [Frequência Intel]
![IMAGEM GRÁFICO DE DISPRSÃO](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Grafico%20de%20Dispersao/grafico%20de%20dispersao%20-%20frequencia%20amd.png)
![IMAGEM GRÁFICO DE DISPERSÃO](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Grafico%20de%20Dispersao/grafico%20de%20dispersao%20-%20frequencia%20intel.png)

Os gráficos Q-Q apresentados comparam a distribuição das frequências dos processadores AMD e Intel com a distribuição teórica normal. Essa análise é fundamental, já que a frequência de operação (em GHz) está diretamente relacionada ao desempenho computacional dos processadores, ou seja, quanto maior e mais estável for essa frequência, maior tende a ser a capacidade de processamento.

No caso dos processadores AMD, observa-se que os pontos do gráfico seguem de forma relativamente próxima à linha reta, sugerindo que as frequências amostradas se aproximam de uma distribuição normal. No entanto, nota-se um leve afastamento da linha nos extremos, especialmente na cauda direita, o que pode indicar a presença de valores mais altos do que o esperado, sugerindo uma assimetria positiva ou outliers. Isso pode refletir modelos AMD com frequências mais elevadas, voltados a alto desempenho.

Para os processadores Intel, o comportamento é semelhante: os dados seguem a linha de referência da normalidade com certa precisão, principalmente na região central. Pequenas variações nas extremidades são esperadas em dados empíricos, mas o alinhamento geral sugere que a frequência dos modelos Intel também se distribui de forma aproximadamente normal.

A proximidade dos dados com a distribuição normal reforça a consistência das frequências oferecidas por ambas as marcas. Essa regularidade é desejável em contextos de análise de desempenho, pois permite aplicar métodos estatísticos com mais robustez, como testes de hipóteses, comparações de eficiência e simulações de desempenho.

Assim, os gráficos não apenas avaliam a normalidade dos dados, mas também dão indícios sobre a confiabilidade e o comportamento estatístico das frequências, atributos diretamente ligados à qualidade e ao desempenho dos processadores.

#### 5.2.2 Gráfico de Dispersão entre [Núcleo AMD] e [Núcleo Intel]
![IMAGEM GRÁFICO DE DISPERSÃO](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Grafico%20de%20Dispersao/grafico%20de%20dispersao%20-%20nucleo%20amd.png)
![IMAGEM GRÁFICO DE DISPERSÃO](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Grafico%20de%20Dispersao/grafico%20de%20dispersao%20-%20nucleos%20intel.png)

  Os gráficos Q-Q acima representam a comparação entre a distribuição dos números de núcleos dos processadores AMD e Intel com uma distribuição teórica normal. Essa análise é relevante, pois o número de núcleos influencia diretamente na capacidade de processamento paralelo, sendo um dos principais fatores que determinam o desempenho multitarefa de um processador.

No gráfico referente aos processadores AMD, observa-se uma forte assimetria positiva. Embora uma parte dos pontos centrais se alinhe relativamente bem à linha de referência, há um desvio acentuado na extremidade superior direita. Isso indica que há processadores AMD com quantidades significativamente maiores de núcleos do que seria esperado em uma distribuição normal, sugerindo uma variedade maior de modelos com alta capacidade de paralelismo. Essa discrepância também pode indicar a presença de outliers intencionais, modelos topo de linha que se distanciam dos padrões médios da marca.

Por outro lado, no gráfico referente aos processadores Intel, os pontos seguem de forma mais consistente a linha de referência, principalmente na região central da distribuição. Ainda há alguma dispersão nas pontas, mas menos acentuada do que no caso da AMD. Isso sugere uma distribuição mais simétrica e concentrada, com uma menor variação no número de núcleos entre os modelos analisados. Em outras palavras, os modelos Intel, nesse conjunto, tendem a apresentar uma distribuição mais homogênea em relação à quantidade de núcleos.

Essa visualização é extremamente útil para a análise de desempenho, pois evidencia como as duas marcas têm estratégias diferentes de arquitetura. A AMD aparenta oferecer uma gama mais ampla de opções com alto número de núcleos, o que pode beneficiar tarefas que exigem paralelismo intensivo, como modelagem 3D, processamento de vídeo e execução de máquinas virtuais. Já a Intel, com sua distribuição mais centrada, pode estar focando em uma eficiência mais previsível por núcleo, o que é vantajoso em aplicações com menos paralelismo, mas que exigem resposta rápida por thread.

Em resumo, os gráficos não apenas mostram desvios da normalidade, mas também ajudam a entender o posicionamento de mercado e o foco de desempenho de cada fabricante, permitindo uma análise mais estratégica sobre qual arquitetura melhor se adequa a determinadas necessidades de uso.

#### 5.2.3 Gráfico de Dispersão entre [Preço AMD] e [Preço Intel]
![IMAGEM GRÁFICO DE DISPERSÃO](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Grafico%20de%20Dispersao/grafico%20de%20dispersao%20-%20pre%C3%A7o%20intel.png)
![IMAGEM GRÁFICO DE DISPERSÃO](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Grafico%20de%20Dispersao/gr%C3%A1fico%20de%20dispers%C3%A3o%20-%20pre%C3%A7o%20amd.png)

Os gráficos apresentados comparam a distribuição dos preços dos processadores AMD e Intel com uma distribuição normal teórica, permitindo uma análise visual sobre o comportamento estatístico desse atributo econômico fundamental na escolha de um processador.

No caso da AMD, observa-se que, embora muitos pontos centrais estejam próximos da linha de normalidade, há uma curvatura acentuada nas extremidades superiores. Isso indica que existe um número considerável de processadores com valores muito acima da média, o que rompe a simetria esperada pela normal. Esses pontos mais altos sugerem a presença de modelos premium, que podem oferecer recursos superiores como mais núcleos, cache ampliado, ou frequências maiores, características que justificam os preços elevados, mas que também configuram outliers econômicos na distribuição.

O gráfico referente aos processadores Intel apresenta um comportamento bastante semelhante. A maioria dos preços está bem alinhada à linha de referência, mas nas extremidades superiores novamente ocorre um desvio marcante, sugerindo também a existência de modelos de alto custo, fora do padrão médio da linha. Essa semelhança entre as marcas indica que ambas possuem uma base de modelos com preços moderados e alguns produtos mais sofisticados com valores significativamente elevados.

Essa visualização é extremamente útil na análise de desempenho, pois o preço de um processador muitas vezes está atrelado às suas capacidades técnicas. Quando se percebe uma cauda longa positiva nos gráficos de preço, como ocorre aqui, entende-se que existem segmentações no mercado, desde modelos acessíveis até processadores voltados ao público entusiasta ou profissional, que demandam máximo desempenho.

Dessa forma, os gráficos não apenas mostram desvios da normalidade, mas evidenciam a estratégia de diversificação de produtos adotada por AMD e Intel. Isso é crucial para o consumidor e o analista de desempenho, pois permite cruzar essas informações com outras variáveis (como núcleos e frequência) para entender se o investimento feito em modelos mais caros realmente se traduz em maior performance.


### 5.3. Gráfico Boxplot 
#### 5.3.1 Gráfico Boxplot da Variável Categórica [Frequência AMD] e [Frequência Intel]
![IMAGEM BOXPLOT](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Boxplot/boxplot%20-%20frequencia%20amd.png)
![IMAGEM BOXPLOT](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Boxplot/boxplot%20-%20frequencia%20intel.png)

Os gráficos de boxplot apresentados permitem uma análise clara e objetiva da distribuição das frequências (em GHz) dos processadores das marcas AMD e Intel. Esse tipo de gráfico é bastante útil para identificar o comportamento central dos dados, a dispersão, a simetria e a presença de valores atípicos, elementos que ajudam a interpretar a consistência e a performance média dos processadores.

No boxplot da AMD, observa-se uma distribuição relativamente simétrica e compacta, com a maioria das frequências concentradas entre aproximadamente 3,0 GHz e 4,0 GHz. A linha central (mediana) está ligeiramente abaixo dos 3,5 GHz, sugerindo que metade dos modelos testados possui frequências abaixo desse valor e a outra metade, acima. Há apenas um outlier visível, com frequência acima de 4,5 GHz, indicando um modelo que ultrapassa consideravelmente o padrão dos demais, provavelmente voltado a alto desempenho. O intervalo interquartil (IQR) é bem definido, o que demonstra consistência e pouca variação entre os modelos.

Já no boxplot da Intel, apesar do mesmo tipo de estrutura, notam-se anomalias visuais significativas: os valores da variável "Speed.GHz" aparecem em milhares, indicando um provável erro de escala (possivelmente os dados foram inseridos em megahertz em vez de gigahertz, sem conversão adequada). Mesmo assim, a estrutura do gráfico ainda permite observar a presença de dois outliers extremos, com valores visivelmente distantes do restante. Desconsiderando esse problema de escala, nota-se que a mediana e a faixa interquartil também são estreitas, sugerindo uniformidade nos modelos mais comuns.

A importância desses boxplots na análise de desempenho é significativa: eles fornecem uma visão rápida sobre a estabilidade e amplitude das frequências oferecidas pelas marcas. A AMD demonstra consistência e um pequeno grau de variação, com raros modelos de frequência extrema. Isso pode indicar uma estratégia de mercado voltada a manter uma base sólida e confiável de desempenho. Já a Intel, mesmo com a distorção aparente nos dados, também parece operar com um núcleo estável de modelos, mas os outliers indicam que há variações ou registros anômalos que podem mascarar a análise real.

Em conjunto, esses gráficos mostram que, para além dos valores máximos ou médios, é essencial observar a distribuição e a regularidade da performance oferecida. Em decisões que envolvem custo-benefício e previsibilidade de desempenho, essas informações se tornam valiosas, tanto para consumidores quanto para profissionais da área de tecnologia e engenharia.

#### 5.3.2 Gráfico Boxplot da Variável Categórica [Núcleo AMD] e [Núcleo Intel]
![IMAGEM BOXPLOT](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Boxplot/boxplot%20-%20cores%20amd.png)
![IMAGEM BOXPLOT](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Boxplot/boxplot%20-%20cores%20intel.png)

Os boxplots apresentados ilustram a distribuição da quantidade de núcleos dos processadores AMD e Intel, oferecendo uma visão clara sobre a dispersão, a concentração e os valores extremos dessa característica fundamental de desempenho.

No gráfico da AMD, observamos uma mediana próxima de 6 núcleos, com a maior parte dos processadores concentrada entre 6 e 8 núcleos. No entanto, o boxplot também revela a presença de diversos outliers, com modelos que possuem até 32 núcleos. Essa característica indica que a AMD oferece uma ampla variedade de modelos com múltiplos núcleos, ampliando suas opções para aplicações que exigem processamento paralelo intenso, como servidores, renderização gráfica ou virtualização. Os outliers não são erros, mas sim modelos extremos intencionais, que elevam significativamente a capacidade de multitarefa.

Por outro lado, o gráfico da Intel mostra uma distribuição mais compacta e simétrica, com a mediana também em torno de 8 núcleos, e com os dados variando aproximadamente entre 4 e 16 núcleos, sem presença de outliers visíveis. Essa estrutura indica que a Intel mantém uma distribuição mais uniforme entre seus modelos, com foco em manter estabilidade e previsibilidade de performance. Embora não alcance os extremos da AMD em termos de número de núcleos, essa consistência pode ser vantajosa para quem busca confiabilidade sem grandes variações entre modelos.

A importância dessa análise está no fato de que a quantidade de núcleos impacta diretamente no desempenho multitarefa de um processador. Processos que se beneficiam de paralelismo, como edição de vídeo, jogos modernos e tarefas com múltiplos processos simultâneos, serão influenciados por essa variável. Portanto, compreender como cada fabricante distribui seus modelos nesse aspecto ajuda a identificar qual atende melhor às necessidades específicas de performance.

Em síntese, enquanto a AMD aposta em diversidade e alto número de núcleos para nichos de alto desempenho, a Intel parece manter um equilíbrio mais uniforme e voltado à eficiência média e os boxplots tornam essa diferença facilmente visível e comparável.


#### 5.3.3 Gráfico Boxplot da Variável Categórica [Preço AMD] e [Preço Intel]
![IMAGEM BOXPLOT](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Boxplot/boxplot%20-%20pre%C3%A7o%20amd.png)
![IMAGEM BOXPLOT](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Boxplot/boxplot%20-%20pre%C3%A7o%20intel.png)

Ao comparar os preços dos processadores AMD e Intel com base nos gráficos apresentados, a gente percebe rapidamente que as duas marcas seguem caminhos bem diferentes. Isso influencia diretamente no que a gente leva pra casa em termos de desempenho e custo-benefício.

No gráfico da AMD, os preços estão bastante concentrados entre $200 e $500. Essa faixa mostra que a marca tem como proposta oferecer processadores acessíveis, que entregam um bom desempenho, especialmente quando se trata de tarefas que usam vários núcleos ao mesmo tempo. E é aí que a AMD ganha força. Ela consegue colocar no mercado modelos mais baratos, mas que não deixam a desejar quando o assunto é desempenho em multitarefa, edição de vídeo, softwares pesados ou mesmo jogos modernos. Além disso, aparecem alguns modelos com preços bem mais altos, chegando até $1700, que são voltados para quem precisa de muito poder de fogo. Esses são os chamados outliers nos gráficos, mas eles fazem parte da linha premium da AMD, voltada para usuários mais exigentes, como profissionais que trabalham com renderização 3D ou servidores.

Ou seja, com a AMD, dá pra montar uma máquina de entrada ou até mesmo uma estação de trabalho sem necessariamente estourar o orçamento. É uma marca que entrega mais núcleos por menos dinheiro na maioria das vezes. Para quem quer economizar e ainda assim ter uma boa performance, ela se torna uma opção muito atraente.

Agora, quando a gente olha para o gráfico da Intel, o cenário é diferente. Os preços médios dos processadores já começam mais altos. Muitos modelos ficam entre $500 e $1300 e, em alguns casos, passam dos $3000. Isso mostra que a Intel aposta mais em uma faixa intermediária para cima, mesmo nos modelos que seriam considerados comuns. A distribuição dos preços é mais equilibrada e não tem tantos processadores com valores muito baixos ou muito altos. Isso indica uma proposta voltada para consistência e desempenho controlado. A Intel tem fama de entregar um processamento estável, com foco em performance por núcleo, o que é ótimo para jogos, softwares que exigem velocidade de resposta e aplicações onde o uso paralelo de muitos núcleos não faz tanta diferença.

Mas claro, essa estabilidade e confiança têm um preço. Quem opta por um processador Intel, na média, vai pagar mais. E é aí que entra o ponto principal dessa análise: o quanto você está disposto a investir para o tipo de desempenho que você precisa.

Se você está montando um computador e tem um orçamento limitado, mas quer o máximo possível de desempenho, principalmente para tarefas simultâneas, a AMD é quase sempre a melhor escolha. Com ela, é possível comprar processadores com mais núcleos e boa performance por um preço significativamente menor. Mas, se você valoriza estabilidade, tradição da marca ou pretende usar o computador em tarefas que exigem precisão e resposta rápida, como jogos, por exemplo, a Intel pode justificar esse investimento maior.

No fundo, essa comparação deixa claro que não existe uma marca melhor de forma absoluta. Existe sim a marca que faz mais sentido para o seu bolso e para o seu tipo de uso. Os gráficos não apenas mostram números, eles contam a história de como cada empresa pensa seus produtos e para quem eles são feitos.

Então, antes de decidir, vale se perguntar: você quer gastar menos e ainda ter um bom desempenho, talvez até mais núcleos? Ou está disposto a pagar mais para ter um processador com uma performance mais previsível e refinada? Com base nos dados analisados, essa resposta fica muito mais clara.

#### 5.3.4 Gráfico Boxplot da Variável Categórica [Cache AMD] e [Cache Intel]
![IMAGEM BOXPLOT](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Boxplot/boxplot%20-%20cache%20intel.png)
![IMAGEM BOXPLOT](https://github.com/EstatisticaNaMatematica/Trabalho-Estat-stica-Amd-vs-Intel/blob/main/Boxplot/boxplot%20-%20cache%20amd.png)


Os gráficos apresentados são boxplots que comparam a distribuição da memória cache (em megabytes) dos processadores das marcas AMD e Intel. A memória cache é um componente crucial para o desempenho do processador, pois permite o acesso mais rápido a dados frequentemente utilizados.

No boxplot da AMD, observa-se que a maior parte dos processadores possui memória cache concentrada entre aproximadamente 50 MB e 350 MB. A mediana (linha central do boxplot) está em torno de 150 MB, indicando que metade dos modelos analisados tem até esse valor de cache. Há também a presença de outliers valores significativamente acima da média que chegam a ultrapassar 1600 MB, demonstrando que a AMD possui alguns modelos com desempenho elevado, embora sejam exceções dentro do conjunto analisado. A distribuição dos dados é relativamente dispersa, o que indica uma grande variedade de modelos, desde os mais básicos até os mais potentes.

Já no boxplot da Intel, nota-se uma maior concentração de memória cache. A maioria dos processadores se encontra na faixa entre 400 MB e 1200 MB, com uma mediana próxima de 600 MB. Isso evidencia que os processadores Intel, de forma geral, oferecem maior capacidade de cache em comparação com os da AMD. Assim como no gráfico anterior, há outliers presentes, indicando a existência de modelos com cache ainda mais elevado, chegando a mais de 3000 MB.

Comparando os dois boxplots, fica evidente que os processadores Intel apresentam, em média, maior capacidade de cache do que os da AMD. A variação entre os modelos da Intel também é mais homogênea, enquanto os da AMD exibem maior dispersão e uma concentração de modelos com cache menor. Apesar de a AMD contar com alguns modelos de alto desempenho, eles são poucos e destoam da maioria dos processadores da marca.

Considerando que a quantidade de memória cache influencia diretamente no desempenho do processador especialmente em tarefas mais exigentes, pode-se concluir que, em média, os processadores Intel oferecem maior potencial de desempenho que os da AMD nesse aspecto. No entanto, a variedade encontrada nos modelos AMD pode ser vantajosa para usuários que procuram soluções mais econômicas ou específicas.

-----

## 6\. Justificativa de Utilização de Cada Medida

### 6.1. Medidas de Tendência Central (Média, Mediana, Moda)

  * **Média:** A média foi utilizada para obter uma noção geral dos valores mais representativos em variáveis contínuas como preço, cache, núcleos e threads. Por exemplo, observando os dados da AMD, a média do preço tende a ser puxada para cima devido à presença de modelos da linha Threadripper, como o 2990WX, que custa $1700. Já na Intel, essa distorção é ainda mais forte com processadores como o Xeon Gold 6154, que custa mais de $3500. Isso mostra que, apesar de útil, a média deve ser usada com cautela em distribuições assimétricas.
  * **Mediana:** A mediana se mostrou uma medida essencial, já que continha valores que puxavam a média para cima. Ela foi especialmente útil nas análises de preço e número de núcleos, sem ser distorcida por valores extremos. No caso da AMD, enquanto a média de preços é puxada para cima por modelos de alto desempenho como os da linha Threadripper, a mediana se mantém na faixa de $250 a $400, que representa melhor os modelos mais populares, como os da série FX e Ryzen 7.  O mesmo acontece com os processadores da Intel, onde a mediana ajuda a destacar os produtos que realmente representam a maior parte, deixando de lado os valores mais inflacionados dos modelos topo de linha.
  * **Moda:** A moda foi aplicada para identificar os valores mais frequentes. especialmente em variáveis discretas como número de núcleos e threads. Tanto na AMD quanto na Intel, observou-se que os processadores com 4 ou 6 núcleos são os mais comuns, sugerindo que esse é o padrão mais utilizado em desktops convencionais.

### 6.2. Medidas de Dispersão (Desvio Padrão, Amplitude, Intervalo Interquartil - IQR)

  * **Desvio Padrão:** O desvio padrão foi essencial para quantificar o quanto os valores se afastam da média. Na AMD, o desvio padrão dos preços foi mais alto por conta da grande variação entre modelos simples como o FX-4100 e modelos de alto desempenho como o Threadripper 2970WX. A Intel também apresentou grande dispersão de preços, com destaque para a linha Xeon, que foge do padrão doméstico.
  * **Amplitude:** A amplitude foi útil pra mostrar de forma clara o quanto os preços variam. No caso da AMD, a diferença entre o processador mais barato e o mais caro passa de $1600. Já na Intel, essa diferença passa de $3300. Isso mostra como as duas marcas têm modelos bem variados, indo desde os mais básicos até os mais potentes e caros, pra atender públicos diferentes.
  * **Intervalo Interquartil (IQR):** O IQR ajudou a isolar os 50% centrais dos dados, sendo especialmente útil para filtrar os outliers. No caso da AMD, ele permitiu identificar que os modelos mais comuns (como FX-8350 e Ryzen 7 2700X) estão concentrados entre o segundo e o terceiro quartil de preços, ou seja, nem os mais básicos, nem os mais caros. O mesmo vale para Intel, com modelos como o Core i7-8700K e i5-9600K posicionados na parte central da distribuição.

### 6.3. Medidas de Posição (Quartis, Percentis)

  * **Quartis/Percentis:** Essas medidas foram utilizadas para entender como os dados se distribuem e para identificar valores extremos. Por exemplo, os modelos da linha Xeon Gold da Intel estão todos acima do 75º percentil em termos de preço, sendo considerados outliers de alto custo. Já na AMD, os modelos FX ocupam o primeiro e segundo quartis, confirmando que são os modelos mais acessíveis.
Além disso, os percentis foram úteis para entender a evolução técnica, já que os processadores com maior número de threads e cache tendem a ocupar as faixas superiores da distribuição em ambas as marcas.

### 6.4. Medidas de Associação (Coeficiente de Correlação de Pearson/Spearman)

  * **Coeficiente de Correlação de Pearson:** Essa correlação foi usada para entender como duas características numéricas se relacionam linearmente. Na AMD, percebeu-se uma relação moderada a forte, indicando que, geralmente, conforme uma característica aumenta, a outra também tende a subir. Já na Intel, essa relação foi um pouco mais fraca em alguns casos, devido à existência de modelos que apesar de terem características menores, apresentam preços elevados por conta de algumas funcionalidades.
  
-----

## 7\. Testes Estatísticos Utilizados

### 7.1. TESTE DE NORMALIDADE DE SHAPIRO-WILK

  * **Objetivo:** Verificar se uma amostra de dados numéricos segue uma distribuição normal. Esse teste é bastante usado porque tem boa potência mesmo com amostras pequenas ou moderadas, ajudando a decidir se análises que pressupõem normalidade são adequadas

  * **Hipóteses:**
      * **H0 (Hipótese Nula):**  Os dados seguem uma distribuição normal. 
      * **H1 (Hipótese Alternativa):** Os dados não seguem uma distribuição normal.

  * **Resultado:**
    ```
    # Código R do teste
    ## TESTE SHAPIRO-WILK PARA "PREÇO AMD"
    shapiro.test((precamd))
    ## Shapiro-Wilk normality test
    ## data:  (precamd)
    ## W = 0.66226, p-value = 4.606e-07
    ## NAO SEGUE DISTRIBUICAO NORMAL
    ```
      * **P-valor:** 4.606e-07
      * **Interpretação:**  Com um p-valor muito menor que 0.05, rejeitamos a hipótese nula de que os dados seguem uma distribuição normal. Portanto, há evidências suficientes para afirmar que a variável "Preço AMD" não segue uma distribuição normal.
    ```
    ## TESTE SHAPIRO-WILK PARA "FREQUÊNCIA AMD"
    shapiro.test(freqamd)
    ## Shapiro-Wilk normality test
    ## data:  freqamd
    ## W = 0.97433, p-value = 0.6631
    ## NÃO SEGUE DISTRIBUIÇÃO NORMAL
    ```
    * **P-valor:** 0.6631
    * **Interpretação:** Como o p-valor é maior que 0.05, não rejeitamos a hipótese nula. Isso indica que não há evidências suficientes para afirmar que os dados da variável "Frequência AMD" desviam da normalidade, ou seja, essa variável pode ser considerada normalmente distribuída.
    ```
    ## TESTE SHAPIRO-WILK PARA "NÚCLEOS AMD"
    shapiro.test(nuclamd)
    ## Shapiro-Wilk normality test
    ## data:  nuclamd
    ## W = 0.6728, p-value = 6.422e-07
    ## NÃO SEGUE DISTRIBUIÇÃO NORMAL
    ```
    * **P-valor:**= 6.422e-07
    * **Interpretação:** O p-valor é muito menor que 0.05, portanto rejeitamos a hipótese nula. Isso indica que a variável "Núcleos AMD" não segue uma distribuição normal.
    ```
    ##TESTE SHAPIRO-WILK PARA "PREÇO INTEL"
    shapiro.test(precintel)
    ## Shapiro-Wilk normality test
    ## data:  precintel
    ## W = 0.77587, p-value = 1.904e-05
    ## NÃO SEGUE DISTRIBUIÇÃO NORMAL
    ```
    * **P-valor:** 1.904e-05
    * **Interpretação:** Com p-valor inferior a 0.05, rejeitamos a hipótese nula. Logo, os dados referentes a "Preço Intel" não seguem uma distribuição normal.
    ```
    ##TESTE SHAPIRO-WILK PARA "FREQUÊNCIA INTEL"
    shapiro.test(freqintel)
    ## Shapiro-Wilk normality test
    ## data:  freqintel
    ## W = 0.97836, p-value = 0.7658
    ## NÃO SEGUE DISTRIBUIÇÃO NORMAL
    ```
    * **P-valor:** 0.7658
    * **Interpretação:** O p-valor é maior que 0.05, não rejeitamos a hipótese nula, indicando que a variável "Frequência Intel" pode ser considerada normalmente distribuída.

-----

## 8\. Análise e Discussão dos Resultados Obtidos

Nesta seção, será discutido os achados mais importantes da análise em relação às questões motivadoras. 

  * **Para a Questão 1 (Onde pode facilitar, a compra para algumas pessoas referente a essas duas marcas.):**

      * Ao comparar os preços dos processadores AMD e Intel, ficou claro que a AMD oferece modelos com valores mais acessíveis. Enquanto existem alguns modelos mais caros, a maioria dos processadores da AMD está na faixa de preço entre $250 a $400. Já na Intel, os preços variam muito mais, indo desde valores mais baixos até modelos que ultrapassam os $3.000.
   Essa diferença mostra que a AMD pode ser uma escolha mais viável para quem quer gastar menos ou está buscando um bom processador com orçamento limitado. A marca cobre melhor os modelos de entrada e intermediários, o que pode facilitar bastante a vida de quem precisa montar um computador sem investir tanto dinheiro.
   Portanto, para quem quer economizar e ainda assim ter um processador com desempenho razoável, os modelos da AMD aparecem como uma opção mais acessível na maioria dos casos.
  * **Para a Questão 2 (Curiosidade sobre algumas informações, por exemplo desempenho, custo benefício, e que nem citado antes, auxilio para comprar quaisquer desses CPU's analisados.):**

      * Ao analisar os dados, ficou evidente que informações como número de núcleos, frequência e preço são fundamentais para entender o desempenho geral dos processadores. Na AMD, por exemplo, há uma tendência clara: quanto mais núcleos, maior o preço  o que é esperado, já que mais núcleos geralmente significam maior capacidade de processamento simultâneo, ou seja, mais desempenho.
   Já na Intel, essa relação entre núcleos e preço nem sempre acontece. Existem modelos com poucos núcleos, mas preços altos. Isso pode estar ligado a outros recursos internos, voltados para uso mais técnico ou profissional, como no caso dos processadores Xeon.
   Além disso, o desempenho também depende de outros fatores, como a frequência de operação, que influencia na velocidade com que as tarefas são realizadas. Mesmo assim, notamos que nem sempre o processador com frequência maior será o melhor custo-benefício tudo depende do equilíbrio entre características técnicas e preço.
   Outra coisa importante é que os valores analisados não seguem um padrão certinho. Em vez de olhar só para a média dos preços, foi mais útil observar medidas como a mediana, que mostram o valor que está mais no centro da distribuição, evitando distorções causadas por modelos muito caros ou muito baratos.
   No fim, o que percebemos foi que a AMD costuma entregar mais desempenho por um preço menor, sendo uma boa escolha para quem quer uma máquina eficiente, mas sem gastar muito. A Intel, por outro lado, pode ser vantajosa em situações mais específicas, quando o usuário precisa de alguma função diferenciada, mesmo que isso signifique pagar mais caro.
  
-----

## 9\. Conclusão

Este trabalho teve como foco analisar e comparar processadores das marcas AMD e Intel, buscando entender melhor onde a compra pode ser mais acessível e o que influencia no custo e desempenho desses equipamentos. A ideia foi ajudar quem precisa escolher entre essas opções e não sabe por onde começar.
   Durante a análise, ficou claro que a AMD oferece modelos com preços mais baixos, especialmente nas linhas FX e Ryzen, sendo mais acessível para o público em geral. Já a Intel apresenta uma variação maior de preços, com modelos que, mesmo tendo menos núcleos, podem custar bem mais por causa de recursos mais específicos.
   Também vimos que quanto mais núcleos e mais recursos técnicos, maior tende a ser o valor do processador principalmente na AMD. No entanto, nem sempre isso se aplica à Intel, onde os preços parecem depender de outros fatores além do desempenho bruto.
   Essas observações podem ser úteis para tomar decisões mais conscientes na hora da compra, considerando o equilíbrio entre o que se precisa e o quanto se pode investir.

### Limitações e Trabalhos Futuros

Mesmo trazendo observações valiosas, é importante reconhecer que essa análise tem algumas limitações. Os dados utilizados, por exemplo, não contemplam fatores como o consumo de energia, a geração de calor ou o desempenho em situações específicas como em jogos, programas de edição ou ambientes corporativos. Pensando em estudos futuros, seria interessante reunir mais informações técnicas, como resultados de benchmarks e testes práticos que mostrem o comportamento real dos processadores em diferentes tarefas. Além disso, seria útil atualizar e ampliar a base de dados com modelos mais recentes, ou até incluir outras marcas, o que tornaria a comparação mais abrangente. Também valeria a pena explorar outras formas de análise, como dividir os modelos por faixa de preço ou tipo de uso, ajudando a montar perfis mais claros de consumidores e permitindo recomendações mais personalizadas.

-----

