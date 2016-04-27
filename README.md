# 27-abril-2016
ruido blanco, métodos para pronosticar

### 27 de baril de 2016 ###

## RUIDO BLANCO ##

pib <- read.csv("C:\\Users\\SALA-C9\\Desktop\\PIB TRIMESTRAL A PRECIOS DE 2008.csv") ## si no le digo nada del header por logica da true
## dec = es para que acepte los decimales que tienen los datos
pibts <- ts(pib[,2], start = 1993, frequency = 4)
pibts
plot (pibts)
Acf(pibts)
View(pibts)

## meanf pronostica la serie de tiempo a traves de la media
# nombre <- meanf(nombre serie, h), h son los periodos que se quieren pronosticar
pibtsmeanf <- meanf(pibts, 4) ## 4 puntos en la grafica, 
View (pibtsmeanf)
plot(pibtsmeanf)

## metodo ingenuo agarra el ultimo valor de la serie de tiempo
pibtsnaive <- naive(pibts, 4)
plot(pibtsnaive)
rwf(pibtsnaive, 4) ## alternativo, hace lo mismo que el naive

## ingenuo estacional
pibtssnai <- snaive(pibts, 4)
plot(pibtssnai)

## metodo de la deriva
pibtsrwf <- rwf(pibts, 4,drift = T ) ## es lo que activa que sea el metodo de la deriva
plot(pibtsrwf)

evalmeandf <- accuracy(pibtsmeanf)
evalnaive <- accuracy(pibtsnaive)
evalsnai <- accuracy(pibtssnai)
evalrwf <- accuracy(pibtsrwf)
evalmeandf
evalnaive
evalsnai
evalrwf

## con los valores que poporciona abajo el mejor metodo sera el que los valores
## de MAPE Y MASE se aproximen mas a 0
## MAE, MAPE, RMSE, MASE los que estan mas cercanos a cero, quiere decir que es el
## mejor pronostico
## comparando los resultados el mejor metodo es el metodo de la deriva
