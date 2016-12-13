# Gráficos para varias variables

En este capítulo se presentan funciones para la creación de gráficos que involucran varias variables.

## Función `plot` \index{plot} \index{diagrama de dispersión}

La función `plot` permite crear gráficos de dispersión entre dos variables cuantiativas. La estructura de la función con los argumentos más usuales se muestran a continuación


```r
plot(x, y, type, main, sub, xlab, ylab)
```

Los argumentos de la función `plot` son:

- `x`: vector numérico con las coordenadas del eje horizontal.
- `y`: vector numérico con las coordenadas del eje vertical
- `type`: tipo de gráfico a dibujar. Las opciones son:
    - `'p'` para obtener puntos, esta es la opción por defecto.
    - `'l'` para obtener líneas.
    - `'b'` para obtener los puntos y líneas que unen los puntos.
    - `'c'` para obtener sólo las líneas y dejando los espacios donde estaban los puntos obtenidos con la opción `'b'`.
    - `'o'` para obtener los puntos y lineas superpuestas.
    - `'h'` para obtener líneas verticales desde el origen hasta el valor $y_i$ de cada punto, similar a un histograma.
    - `'s'` para obtener escalones.
    - `'S'` similar al anterior.
    - `'n'` para que no dibuje.
- `...`: otros parámetros gráficos que pueden ser pasados como argumentos para `plot`.

### Ejemplo {-}
Crear 16 parejas de puntos tales que $x=-5, -4, \ldots, 9, 10$ con $y=-10+(x-3)^2$, dibujar los nueve diagramas de dispersión de $y$ contra $x$ usando todos los valores posibles para el parámetro `type`.

A continuación se muestra el código para crear las 16 parejas de $x$ e $y$. Los nueve diagramas de dispersión se observan en la Figura \@ref(fig:ex1plot), de esta figura se observa claramente el efecto que tiene el parámetro `type` en la construcción del diagrama de dispersión.


```r
x <- -5:10
y <- -10 + (x-3)^2
par(mfrow=c(3, 3))
plot(x=x, y=y, type='p', main="con type='p'")
plot(x=x, y=y, type='l', main="con type='l'")
plot(x=x, y=y, type='b', main="con type='b'")
plot(x=x, y=y, type='c', main="con type='c'")
plot(x=x, y=y, type='o', main="con type='o'")
plot(x=x, y=y, type='h', main="con type='h'")
plot(x=x, y=y, type='s', main="con type='s'")
plot(x=x, y=y, type='S', main="con type='S'")
plot(x=x, y=y, type='n', main="con type='n'")
```

![(\#fig:ex1plot)Efecto del parámetro `type` en la función `plot`.](03_graphs2v_files/figure-latex/ex1plot-1.pdf) 

### Ejemplo {-}
Como ilustración vamos a crear un diagrama de dispersión entre el precio de apartamentos usados en la ciudad de Medellín y el área de los apartamentos. El código necesario para cargar la base de datos y construir el diagrama de dispersión se muestra a continuación.


```r
url <- 'https://raw.githubusercontent.com/fhernanb/datos/master/aptos2015'
datos <- read.table(file=url, header=T)

par(mfrow=c(1, 2))
plot(x=datos$mt2, y=datos$precio,)
plot(x=datos$mt2, y=datos$precio, pch='.',
     xlab='Área del apartamento (m2)', ylab='Precio (millones de pesos)')
```

![(\#fig:ex2plot)Diagrama de dispersión del precio del apartamento versus área del apartamento. A la izquierda el diagrama de dispersión sin editar y a la derecha el diagrama de dispersión mejorado](03_graphs2v_files/figure-latex/ex2plot-1.pdf) 

En la Figura \@ref(fig:ex2plot) se presenta el diagrama de dispersión entre precio y área de los apartamentos, de este diagrama se observa claramente que a medida que los apartamentos tienen mayor área el precio promedio y la variabilidad del precio aumentan. Para el diagrama de dispersión de la derecha se usó el parámetro `pch='.'` con el objetivo de obtener pequeños puntos que representen cada apartamento y que no se traslapen debido a que se tienen 694 observaciones en la base de datos.

## Función `persp` \index{persp}
La función `persp` dibuja superfices en tres dimensiones y es posible rotar la superficie para obtener una perpectiva apropiada. La estructura de la función con los argumentos más usuales se muestran a continuación.


```r
persp(x, y, z, main, sub, theta, phi, r, col, border, box, axes, nticks)
```

Los argumentos de la función `plot` son:

- `x`: vector numérico con los valores de $x$ donde fue evaluada la función o superficie.
- `y`: vector numérico con los valores de $y$ donde fue evaluada la función o superficie.
- `z`: matriz que contiene las alturas $z$ de la supercifie para cada combinación de $x$ e $y$.
- `main`: vector numérico con las coordenadas del eje vertical.
- `sub`: vector numérico con las coordenadas del eje vertical.
- `theta, phi`: ángulo para la visión de la superficie, `theta` para la dirección azimutal y `phi` para latitud. Ver Figura \@ref(fig:globo) para una ilustración de los ángulos.
- `r`: vector numérico con las coordenadas del eje vertical.
- `col`: 
- `col`: 
- `col`: 
- `col`: 

\begin{figure}

{\centering \includegraphics[width=0.25\linewidth]{images/IC412528} 

}

\caption{Ilustración de los angulos theta y phi para la función persp. Figura tomada de https://i-msdn.sec.s-msft.com/dynimg/IC412528.png}(\#fig:globo)
\end{figure}


### Ejemplo {-}


```r
fun <- function(x, y) {
  sin(x^2 + y^2)
}

x <- seq(from=-2, to=2, length.out=50)
y <- seq(from=-2, to=2, length.out=50)
z <- outer(x, y, fun)

par(mfrow=c(2, 2), mar=c(1, 1, 2, 1))
persp(x, y, z, zlim=c(-1, 1.5), col='aquamarine', main='')
persp(x, y, z, zlim=c(-1, 1.5), theta=15, phi=15, col='lightpink',
      main='theta=15, phi=15')
persp(x, y, z, zlim=c(-1, 1.5), theta=45, phi=30, col='yellow1',
      main='theta=45, phi=30')
persp(x, y, z, zlim=c(-1, 1.5), theta=60, phi=50, col='lightblue',
      main='theta=60, phi=50')
```

![(\#fig:ex1persp)Superficie generada con `persp` y diferentes valores de theta y phi.](03_graphs2v_files/figure-latex/ex1persp-1.pdf) 


## Función `pairs` \index{pairs} 
## Función `contour` \index{contour} \index{gráfico de contornos}

