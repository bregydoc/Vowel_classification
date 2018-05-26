# Reconocimiento y caracterización de sonidos de vocales en español.

#####  Autores: 

1. Alexander Ortega
2. Joshi Lopez 
3. Bregy Malpartida

## Introducción

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur vel fermentum enim. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Cras enim metus, elementum id vulputate quis, vestibulum quis lorem. Quisque id est suscipit, pretium ipsum et, tempus ipsum. Duis efficitur maximus massa, eget fermentum lectus sagittis id. Quisque a lacus eget ipsum convallis rutrum. Nunc ultricies purus ut pellentesque convallis. Aliquam sed libero sit amet turpis suscipit volutpat. Sed rutrum leo lectus, vel ornare massa consequat ut. Aenean egestas eget nulla vitae pharetra. Suspendisse dignissim dolor sed pharetra semper.


## Objetivos

* Conocer la forma actual con la que los investigadores realizan el procesamiento y clasificación de señales de audio.
* Entender a detalle los distintos métodos de clasificación y segmentación de señales digitales (audio).
* Lorem ipsum dolor sit amet, consectetur adipiscing elit.

## Estado del arte

### 1. Vowel Classification based on LPC and ANN [***R. B. Shinde***]

#### ¿Que se hizo en el paper?

Intentaron clasificar el sonido de vocales en ingles usando métodos basados en Coeficientes de Predicción Linear (Linear Prediction Coefficient) y Redes Neuronales Artificiales. Usando estos métodos llegaron a un 98.7% de eficiencia.

#### ¿Como se realizó la clasificación?

Primero generaron una base de datos de vocales en ingles con 5 personas y 5 muestras por vocal por persona ('A', 'E', 'I', 'O' y 'U'). Con la base de datos ya lista, construyeron un VCS (Vowel Classification System), en la figura 1 se detalla la forma en que se organiza este sistema.


| ![image-20180525200851379](https://k62.kn3.net/2/1/E/5/E/5/EE4.png) |
| :----------------------------------------------------------: |
| Figura 1. Diagrama de bloques del sistema propuesto por Shinde. |



Lo siguiente para la clasificación de las vocales fue proceder con el algoritmo para extraer las caracteristicas intrinsecas en las señales de audio (features). A continuación se realizo un proceso de pre énfasis. 
El proceso de pre énfasis consiste en un sistema de primer orden:

<p align="center">
	<img src="https://k62.kn3.net/1/0/B/5/4/B/8E8.png"/>
</p>


los autores usaron  a = 0.95.

Posterior al pre énfasis se realizó un proceso de framing que significa segmentar la señal en pequeños frames, a continuación se realizó "Hamming Windowing" a cada frame, el proceso de Windowing representó usar la siguiente función.

<p align="center">
<img src="https://k62.kn3.net/A/7/5/F/1/8/E32.png"/>
</p>



A continuación se aplico una transformación a frecuencia (FFT)  a cada frame y a continuación se calcularon los coeficientes de predicción lineal (LPC) de la siguiente forma : 

<p align="center">
<img src="https://k62.kn3.net/2/B/3/E/8/E/44C.png"/>
</p>

donde la longitud del resultado de LPC debería de ser menor o igual a la longitud de X.

Antes de pasar a la etapa de clasificación se aplico una transformación discreta de coseno (DCT en ingles), para esto se usó:



<p align="center">
<img src="https://k62.kn3.net/D/A/1/1/A/1/B2D.png"/>, donde:
</p>

<p align="center">
<img src="https://k62.kn3.net/9/7/0/1/9/B/5B9.png"/>
</p>

Finalmente se obtuvieron un total de 75 muestras de audio de 5 diferentes personas que hacen un total de 375 caracteristicas (features).


|  <img src="https://k62.kn3.net/7/8/4/D/A/8/C56.png"/>  |
| :----------------------------------------------------: |
| Figura 2. Red neural que usaron para la clasificación. |


Finalmente, para clasificar las caracteristicas que se obtuvieron con el preprocesamiento se unso una red neuronal de 3 capas donde la capa intermedia (capa oculta) cuenta con 20 neuronas, se usó el método de backpropagation para entrenar dicha red y se logró un 90.9%. 

En la fig. 3 se puede apreciar la matriz de confusión del proceso de entrenamiento y en la fig. 4  la matriz de confusión del proceso de testing.


| <img src="https://k62.kn3.net/9/F/6/3/C/C/A7B.png" style="height: auto; width: 350px"/> |
| :----------------------------------------------------------: |
|        Figura 3. Matriz de confusíon de entramiento.         |





| <img src="https://k62.kn3.net/D/9/F/4/6/1/17C.png" style="height: auto; width: 360px"/> |
| :----------------------------------------------------------: |
|          Figura 4. Matriz de confusíon de testing.           |


#### Conclusiones

Consiguieron un modelo predictivo bastante preciso, lograron un 91.5% de "accuracy" con 88 iteración en el proceso de entrenamiento de la red neuronal. Individualmente, se logró un 100% de reconocimiento correcto con las vocales A, E, O, U; para la vocal I se consiguió 93.3% de precisión. (Ver fig. 5).


| <img src="https://k62.kn3.net/6/7/7/D/5/C/1CB.png"/> |
| :--------------------------------------------------: |
|      Figura 5. Precisión individual por vocal.       |



### 2. Cepstral Analysis [***Deepa Kundur***]

#### ¿Que se hizo en el paper?

Se expuso y explicó los conceptos de análisis Cepstral y deconvolución.

#### ¿Como se realizo…?

Kundur propusó el siguiente diagrama de bloques en la Figura#

| ![](https://k62.kn3.net/B/A/8/5/D/7/181.png) |
| :------------------------------------------: |
|                  Figura 1.                   |



Entra al sistema una señal (la voz en este caso) y es discretizada, es decir, inicialmente la señal de voz entra al sistema como una señal en dominio de tiempo, la cual posteriormente es transforomada a dominio de muestras.

<p align="center">
	<img src="https://k62.kn3.net/8/D/F/7/B/2/9AA.png"/>
</p>

Se presenta una convolución en tiempo discreto, la cual tambien se puede analizar como un producto en el dominio de la frecuencia. Al aplicarle una FFT(Fast Fourier Transform) o transformada rápida de Fourier, obtemos:

<p align="center">
	<img src="https://k62.kn3.net/3/4/5/8/7/B/973.png"/>
</p>

Se aplica un artificio matemático que consiste en separar ambas funciones multiplicadas y tomarlas como logaritmos de sus magnitudes para poder obtener:

<p align="center">
	<img src="https://k62.kn3.net/6/4/D/1/E/C/054.png"/>
</p>

Finalmente se aplica una IFFT(Inverse Fast Fourier Transform) o transformada rápida inversa de Fourier en el dominio cepstral.

<p align="center">
	<img src="https://k62.kn3.net/F/E/1/7/D/A/E94.png"/>
</p>

Como resultado de esta transformada inversa se tiene la variable independiente “quefrency” la cual tiene como unidad de trabajo el tiempo.

Cabe resaltar que las áreas de mayor interés se encuentran entre los 0 a 10 ms de la señal de voz cepstrum. 

#### Comentarios adicionales

Al ser un paper guía deja algunas variables al aire, es decir, nos sugieren tomar 1 muestra masculina y una femenina por cada vocal - "a", "e", "i", "o", "u"-  y tomar en cuenta variables como el tipo de microfono  a utilizar, tipo de computador, el software, el ambiente en el que grabamos las muestras, entre otras. Pienso que estas variables podrían reducirse al tomar una base de muestras más grande de diferentes personas a diferentes tonos.



### 3. Algorithms for Vowel Recognition in Fluent Speech Based on Formant Positions [***Miroslav Stanek***]

#### ¿Que se hizo en el paper?

 Un formante es una concentración de energía acústica alrededor de una frecuencia particular en la señal del habla.

El algoritmo de Stanek reconoce las frecuencias de las dos formantes principales, las cuales determinan una vocal.  

#### ¿Como se realizó el reconocimiento de las formantes?

Stanek propone el siguiente diagrama de bloques en la Figura 1:


| <img src="https://k62.kn3.net/A/3/6/5/7/9/C6F.png" style="width: 300px ;heigth: auto;"/> |
| :----------------------------------------------------------: |
|                        Figura 1. ...                         |


Se empieza con la entrada de la señal del habla, la cual es muestreada a 8kHz y normalizando su amplitud.Luego se procede a segmentarse usando ventanas de Hamming; en bloques de 20 ms sin sobreposicionamiento.

Cada segmento se procesa en secuencia y se analiza si es una secuencia con información sobre una vocal ; si es así, se obtienen sus coeficientes de predicción linear. El orden de predicción linear es 10 y el espectro LPC  es dado por estos coeficientes.

La determinación de las formantes se basa en la interacción entre el espectro LPC y su derivación.

El siguiente paso es la comparación las formantes determinadas con formantes comunes ya determinadas.



#### Conclusiones

El algoritmo de reconocimiento de vocales planteado es aunque sencillo, es medianamente eficaz al observar los resultados en el paper ya que el error alcanza valores de 5% a 60%, aunque esto se compensa con su mediano costo computacional.



### 5. A Comparative Study of Formant Frequencies Estimation Techniques  [***Dorra Gargouri***]

### 6. Malayalam Vowel Recognition Based On Linear Predictive Coding Parameters and k-NN Algorithm [***T. M. Thasleema***]

#### ¿Que se hizo en el paper?

Se utiliza un modelo de codificación predictiva lineal para el reconocimiento de vocales,luego utiliza             k-vecino más cercanos para clasificar la señal de habla en clases.

#### ¿Como se realizo el reconocimiento basado en LPC y k vecinos más cercanos?

En aplicaciones del habla, la principal ventaja usualmente se atribuye a las caracteristicas de todos los polos del espectro de la vocal.En comparacion con otras tecnicas de modelo espectral no parámetrico,LPC es mejor comprimiendo la informacion del espectro en pocos coeficientes de filtro que pueden ser cuantificados de manera eficiente.

Dado que las señales de habla solo son estables en un periodo pequeño, LPC es un metodo de estimacion de pocos terminos.El metodo LPC considera una muestra de habla en tiempo n, s(n) y la aproxima con una combinación linear de p muestras pasadas de la siguiente forma:

<p align="center">
<img src="https://k62.kn3.net/E/0/C/D/C/C/5F1.png"/ style="width: 350px ;heigth: auto; "\>
</p>

donde los coeficientes a~1~ , a~2~, ............. a ~p~ se asumen constantes en el marco de analisis de voz.

A la primera expresión se le incluye  un termino de exitación Gu(n)

<p align="center">
<img src="https://k62.kn3.net/B/6/9/E/C/7/6D5.png"/ style="width: 210px ;heigth: auto; "\>
</p>

donde u(n) es una excitación normalizada y G es la ganancia de esta.Al expresar  en el dominio z se obtiene la relacion:

<p align="center">
<img src="https://k62.kn3.net/3/2/D/8/C/3/C79.png"/ style="width: 210px ;heigth: auto; "\>
</p>

En consecuencia, la funcion de transferencia H(z) es:

<p align="center">
<img src="https://k62.kn3.net/E/E/9/1/9/6/21E.png"/ style="width: 280px ;heigth: auto; "\>
</p>

Los parametros principales que se pueden obtener del modelo LPC es la clasificación de hablado/no hablado, el periodo de habla, la ganancia y los coeficientes a~i~ ,se debe tener en cuenta de que a mayor el orden del modelo, el modelo de polos representara los sonidos hablados de mejor manera.

La clasificación por k vecinos más cercanos se da gracias a la proximidad de un patron desconocido a un patron determinado por una clase.Una clase puede ser caracterizada por uno o mas patrones.El metodo de k vecinos más cercanos es una clasificación no parametrica, donde la probabilidad es estimada por la frecuencia  de vecinos más cercanos a el patron desconocido.La clasificación por k vecinos más cercanos se  basa en los parametros obtenidos en el modelo LPC.

#### Conclusiones

La precisión del reconocimiento usando la extraccion de parametros por LPC según los resultados del paper es de 94%, aunque la clasificación por k vecinos mas cercanos da una mejora en la precision del reconocimiento,el costo computacional  es mayor comparado con otros metodos de clasificacion

### On the performance of the quefrency-weighted cepstral coefficients in vowel recognition [***K.K. PALIWAL***]





## Conclusiones

