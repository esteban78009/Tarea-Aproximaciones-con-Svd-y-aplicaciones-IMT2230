# Tarea-Aproximaciones-con-Svd-y-aplicaciones-IMT2230 


Repositorio de la Seccion 2 de la tarea 2 de IMT2230

## Introduccio y contexto:

Fashion-MNIST es un dataset publico conocido por tener 70000 imagenes de diversas prendas en blanco y negro , esto con objetivos como ser usado en modelos clasificatorios o por redes neuronales, o sensillamete para ser usado como practica en casos de manipulacion numerica, como es nuestro caso
En este mini proyecto se hizo uso de SVD para descomponer todas las imagenes de este set en funcion de sus "Eige ropás" es decir, usar tecnicas de algebra lineal para poder descomponer imagenes en fragmentos de datos mas pequeños, de tal forma que podamos expresar estas mismas en relacion a unos pocos vectores

Para esto expresamos la matriz relacionada a todos las imagenes, de tal forma que tenemos una matriz: $$A ^ {70000 \times 784}$$

Usando esta matriz le aplicaremos SVD a su matriz centrada , es decir:
$$\tilde{X} = X - \mathbf{1}\bar{x}^\top, \text{ donde } \bar{x} = \frac{1}{n}X^\top\mathbf{1}$$


## Ejecucion

Primero Analisaremos la importancia de cada valor singular, para poder determinar luego cuantos valores son suficiente para recuperar con cierta precision una ropa cualquiera, de esta forma, cuando graficamos la importancia de cada valor singular, queda de la forma:

![alt text](https://github.com/esteban78009/Tarea-Aproximaciones-con-Svd-y-aplicaciones-IMT2230/blob/d170b840f2b020d959aa09cce4f94f7245592a4f/graficos/image.png)

![alt text](https://github.com/esteban78009/Tarea-Aproximaciones-con-Svd-y-aplicaciones-IMT2230/blob/d170b840f2b020d959aa09cce4f94f7245592a4f/graficos/image-1.png)

De aqui podemos ver que el peso de cada vector propio disminuye significativamente en los valores singulares cercanos al 20 , luego Usando SVD se hizo la Descomposicion en valores singulares, de esta forma "re transformamos" los vectores en imagenes, obtiendo las Siguientes imagenes relacionadas a los vectores propios, estas mismas las llamaremos "eigen ropas"

![alt text](https://github.com/esteban78009/Tarea-Aproximaciones-con-Svd-y-aplicaciones-IMT2230/blob/d170b840f2b020d959aa09cce4f94f7245592a4f/graficos/image-2.png)

De estas mismas podemos notar ciertos datos curiosos; podemos notar que se vislumbran cosas como que tanto la componente 1, 6 , 7 9 10 y 11 parecen ser camisas, el resto es una extraña superposicion entre diferentes prendas, por ejemplo el 4 parece , en cierta perspectiva, un zapato, y la componente 8 no es identificable, pareciendo mas una mandibula que otra cosa

Luego del analisis de las "Eigen ropas" vamos a hacer la prueba de como se ven ciertas imagenes, descomponiendola en diversos rangos de vectorers singulares, de esta forma pódemos analizar cuando las imagenes empiezan a ser reconocibles en funcion a la cantidad de vectores singulares o "eigen ropas"
para analizar esto mismo usaremos la siguiente formula:

$$\hat{x}_k = \bar{x} + \sum_{i=1}^{k} z_i v_i, \qquad z_i = \tilde{x}^\top v_i$$

Tal que $\hat{x}_k$ es la aproximacion de k vectores singulares de cada vector original , $\bar{x}$ es el vector "central" nacido de la media de todos los vectores , $z_i$ representa el "peso" de cada vector , es decir, cuanto de la imagen original representa cada componente $v_i$ es el vector singular asocido,es decir, nuestra "eigen ropa", tal que podemos notar que la suma de todas las "eigen ropas" son Exactamente lo mismo al vector original que buscamos recomponer

![alt text](https://github.com/esteban78009/Tarea-Aproximaciones-con-Svd-y-aplicaciones-IMT2230/blob/d170b840f2b020d959aa09cce4f94f7245592a4f/graficos/image-3.png)

De esta forma podemos notar ciertos fenomenos curiosos, de partida gran parte de las imagenes son levemente reconocibles en su primera componente, obteniendo una mejora sigficativa de precision en la 3ra a 7tipa componente, desde la 100ta componente ya es seguro que representa cada imagen, obteniendo una "leve precision" cuando aumentamos a 300 en relacion a la cantidad de vectores que estamos usando, ademas, como comfirmacion del metodo, podemos notar que la imagen original es exactamente igual a la imagen usando 784 vectores.

# verificacion de resultados

En caso de querer verificar los siguientes resultados, se debe de ejecutar el archivo notebook.ipynb usando el requirements provisto, recomiendo la ejecucion de esta misma usando python 3.12 , puesto que esta fue la version usada originalmente