Atividade Avaliativa I
================
Naiara Ferreira de Jesus
</br> Estat 2020.2

------------------------------------------------------------------------

**Questão 1**

**(a)** Está errado,pois o as hastes desse boxplot vai até os valores
maxímos e mínimos, sendo assim a mala mais pesada é a de 30kg.

**(b)** O peso mediano é de 7,5kg.

**(c)** A distância interquartílica é de 6,5.

**(d)** 24 malas **Questão 2**

**(d)** 6,40+5,20/2= 5,80

**Questão 3** **(a)** criando o vetor X

``` r
X <- c(58,67,68,68,70,70,72,72,75,79,80,80,80,84,90,90,90,94,100,110)
```

**(b)** Calculando média,mediana, quartil e desvio padrão

``` r
mean(X)
```

    ## [1] 79.85

``` r
median(X)
```

    ## [1] 79.5

``` r
quantile(X)
```

    ##    0%   25%   50%   75%  100% 
    ##  58.0  70.0  79.5  90.0 110.0

``` r
sd(X)
```

    ## [1] 12.78681

Primeiro quartil é 70, a média de 79,85, a mediana é, 79,5 O terceiro
quartil é 90,e O desvio padrão é de aproximadamenente 13 batimentos.

**(c)** Criando histograma

``` r
hist(X)
```

![](readme_files/figure-gfm/unnamed-chunk-3-1.png)<!-- --> Sim , pois a
média é maior que a mediana, ocasionado uma leve assimetria á direita do
gráfico,assim para representar esses dados o ideal é a mediana.

\*Questão 4\*\*

``` r
library(readr)
frango_dieta <- read_csv("~/repositorios_Github/01_atividade-avaliativa/dados/tidy/frango_dieta.csv")
```

    ## New names:
    ## * `` -> ...1

    ## Rows: 578 Columns: 5

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## dbl (5): ...1, peso, tempo, frango, dieta

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

**(a)** sim, pois cada coluna é uma variável.

**(b)** Calculando a média

``` r
mean(frango_dieta$peso)
```

    ## [1] 121.8183

``` r
round(mean(frango_dieta$peso), 2)
```

    ## [1] 121.82

A média dos pesos do frangos é de 121,82.

**(c)** Calculando o desvio padrão

``` r
sd(frango_dieta$peso)
```

    ## [1] 71.07196

``` r
round(sd(frango_dieta$peso) )
```

    ## [1] 71

O desvio padrão dos pesos é de 71.

**(d)** A Variavél peso é quantitativa cotínua e frango dieta e tempo
quantutativa discreta.

**Questão 5** Rodando o código

``` r
N <- 1000
x <- rnbinom(N, 4, .5)
hist(
x,
xlim = c(min(x), max(x)),
probability = T,
nclass = max(x) - min(x) + 1,
col = 'lightblue', xlab = ' ', ylab = ' ', axes = F,
main = 'Positive Skewed'
)
lines(density(x, bw = 1), col = 'red', lwd = 3)
```

![](readme_files/figure-gfm/unnamed-chunk-7-1.png)<!-- --> Observando a
curva vermelha,está visível que possui uma grande assimetria entre os
dados obtidos,possuindo uma concentração maior dos dados á direita do
gráfico, sendo assim entre a média e a mediana, a mais indicada para ser
a medida resumo desse tipo de gráfico é a mediana,já que esses valores
não irá afetar tanto ela diferentemente da média que sofre interferência
quando s tem valores extremose.

**Questão 6**

**(a)** Importando dataset

``` r
library(readr)
dados_co2 <- read_csv("~/repositorios_Github/01_atividade-avaliativa/dados/brutos/dados_co2.csv")
```

    ## Rows: 39 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## dbl (13): ano, jan, fev, mar, abr, mai, jun, jul, ago, set, out, nov, dez

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

**(b)** Não está no formato tidy, pois a variável mês está espalhada
formando novas colunas,e os valores coletados não estão em uma coluna
específica.

**(c)** Organizando na forma tidy

``` r
co2_tidy <-dados_co2%>% pivot_longer(
  !ano,names_to = "mes",
  values_to = "ppm"
)
```

**(d)** Escrevendo arquivo csv

``` r
write_csv(dados_co2,"dados,tidy,co2_tidy.csv")
```

**(e)** Lendo arquivo csv

``` r
library(readr)
co2_tidy <- read_csv("~/repositorios_Github/01_atividade-avaliativa/dados/tidy/co2_tidy.csv")
```

    ## Rows: 39 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## dbl (13): ano, jan, fev, mar, abr, mai, jun, jul, ago, set, out, nov, dez

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

Rodando o código

    co2_tidy %>%
    group_by(ano) %>% 
    summarise(media = round(mean (ppm), 2)) %>%
    ggplot(aes(ano, media, group = 1)) +
    geom_line(color = "blue", size = 1)

A média teve um aumento substancial com o passar dos anos.

**Questão 7**

**(a)** construindo uma tribble

``` r
peso_altura <- tribble(
  ~nome, ~altura, ~peso,
  "Ana", 155, 50,
  "Ludmilla", 158, 61,
  "Cristina", 162, 65,
  "Tereza",   168, 68,
  "Patricia", 170, 69, 
  "Mariana",  170, 65,
  "Ana Paula", 172, 82,
  "Dirce",    173, 79,
)
```

**(b)** As variáveis peso e altura são quantitativas contínuas.

**(c)** Calculando a média, mediana e desvio padrão

``` r
mean(peso_altura$peso)
```

    ## [1] 67.375

``` r
mean(peso_altura$altura)
```

    ## [1] 166

``` r
median(peso_altura$peso)
```

    ## [1] 66.5

``` r
median(peso_altura$altura)
```

    ## [1] 169

``` r
sd(peso_altura$peso)
```

    ## [1] 10.04188

``` r
sd(peso_altura$altura)
```

    ## [1] 6.78233

Arredondando a média e mediana do peso e o desvio pdrão do peso e altura

``` r
round(mean(peso_altura$peso),2)
```

    ## [1] 67.38

``` r
round(median(peso_altura$peso),2)
```

    ## [1] 66.5

``` r
round(sd(peso_altura$peso),2)
```

    ## [1] 10.04

``` r
round(sd(peso_altura$altura),2)
```

    ## [1] 6.78

A média do peso é 67.38, a mediana é de 66.5, e o desvio padrão é de
10.04. A média da altura é de 166,a mediana é 169, e o desvio padrão é
de 6.78.

**(d)** Gráfico R

``` r
plot(peso_altura$peso, 
     peso_altura$altura)
```

![](readme_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

Sim, há uma concentração de pessoas com pesos de 65 á 70 kg,e uma
concentração entre as alturas de 1,65 á 1,70 cm.
