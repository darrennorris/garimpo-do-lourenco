# Amapa-mine
Mineração e desmatamento no Amapá. Mining and deforestation in Amapá.

<img align="right" src="www/lourenco.jpg" alt="Gold mine" width="300" style="margin-top: 20px">

Código de [R](https://cran.r-project.org/) e dados para calcular 
métricas de paisagem associadas com a exploração de recursos minerários. 

As métricas de paisagem são a forma que os ecólogos de paisagem usam 
para descrever os padrões espaciais de paisagens para depois avaliar 
a influência destes padrões espaciais nos padrões e processos ecológicos.

Objetivo é calcular métricas de paisagem e descrever a composição e a configuração da paisagem no entorno do Garimpo do Lourenço.


## Conteúdo
Os dados aqui apresentados (gráficos, mapas) representam conteúdo do 
domínio público, disponibilizados pelos institutos, órgãos e entidades
federais, estaduais e privados ([IBGE](https://www.ibge.gov.br/),  [MapBiomas](https://mapbiomas.org/), [Agência Nacional de Mineração](https://dados.gov.br/dataset/sistema-de-informacoes-geograficas-da-mineracao-sigmine) ). O conteúdo está aqui apresentado para divulgação ampla, respetiando as obrigações de transparência, assim para agilizar e 
facilitar o desenvolvimento técnico científco. O conteúdo não representar versões ou produtos  finais e não devem ser apresentados/relatados/compartilhados/interpretados como conclusivos. 

Os mapas e cartogramas ficam na pasta [figures](https://github.com/darrennorris/ZEEAmapa/tree/main/figures) (formato .png e .tif), dados geoespaciais na pasta [vector](https://github.com/darrennorris/ZEEAmapa/tree/main/vector) (formato shapefile e GPKG) e dados tabulados na pasta [dados](https://github.com/darrennorris/ZEEAmapa/tree/main/dados) (copia de dados disponibilisados pela [abjData](https://github.com/abjur/abjData), definicão de siglas etc) .

- [Mapas](#mapas)
  * [Desenvolvimento e Vulnerabilidade](#desenvolvimento-e-vulnerabilidade)
  * [Educação e maternidade](#educacao)
- [Mineração](#mineracao)


#Estabelecer a extensão da área de estudo
#Mineração pode aumentar a perda da floresta até 70 km além dos limites 
#do processo de mineração:
#Sonter et. al. 2017.
#Mining drives extensive deforestation in the Brazilian Amazon
#https://www.nature.com/articles/s41467-017-00557-w
#https://earthengine.google.com/timelapse/#v=-1.70085,-56.45017,8.939,latLng&t=2.70

#Aqui vamos incluir um raio de 20 km alem 
#do ponto de accesso para o Garimpo do Lourenço em 1985.
#Isso repesentar uma area quadrado de 40 x 40 km (1600 km2).
garimpo <- data.frame(nome = "garimpo do Lourenço", 
           coord_x = -51.630871, 
           coord_y = 2.318514)
#Converter para objeto espacial
sf_garimpo <- st_as_sf(garimpo, 
               coords = c("coord_x", "coord_y"),
            crs = 4326)
plot(sf_garimpo)
mapview(sf_garimpo) #verificar com mapa de base (OpenStreetMap)


Pacotes necessarios: 
library(sf)
library(tidyverse)
library(landscapemetrics)
library(terra)
library(readxl)
library(mapview)
library(units)