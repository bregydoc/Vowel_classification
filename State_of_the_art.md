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

### Vowel Classification based on LPC and ANN [***R. B. Shinde***]

#### ¿Que se hizo en el paper?

Intentaron clasificar el sonido de vocales en ingles usando métodos basados en Coeficientes de Predicción Linear (Linear Prediction Coefficient) y Redes Neuronales Artificiales. Usando estos métodos llegaron a un 98.7% de eficiencia.

#### ¿Como se realizó?

Primero generaron una base de datos de vocales en ingles con 5 personas y 5 muestras por vocal por persona ('A', 'E', 'I', 'O' y 'U'). Con la base de datos ya lista, construyeron un VCS (Vowel Classification System), en la figura 1 se detalla la forma en que se organiza este sistema.![image-20180525200851379](https://k62.kn3.net/2/1/E/5/E/5/EE4.png)

<p style="text-align: center;">Figura 1. Diagrama de bloques del sistema propuesto por Shinde</p>



Lo siguiente para la clasificación de las vocales fue proceder con el algoritmo para extraer las caracteristicas intrinsecas en las señales de audio (features). A continuación se realizo un proceso de pre énfasis. 
El proceso de pre énfasis consiste en un sistema de primer orden: $$ H(z) = 1-az^{-1}, 0.9 < a < 1.0$$ , los autores usaron $$ a = 0.95$$.

Posterior al pre énfasis se realizó un proceso de framing que significa segmentar la señal en pequeños frames, a continuación se realizó "Hamming Windowing" a cada frame, el proceso de Windowing representó usar la siguiente función $$ w[n] = 0.54 - 0.46\cos{(\frac{2 \pi n}{N-1})}$$.

A continuación se aplico una transformación a frecuencia (FFT)  a cada frame y a continuación se calcularon los coeficientes de predicción lineal (LPC) de la siguiente forma : $ s[n]  = -A(2)*X(n-1) - A(3)*X(n-2) - … -A(N+1)*X(n-N)$, donde la longitud del resultado de LPC debería de ser menor o igual a la longitud de $$ X$$.

Antes de pasar a la etapa de clasificación se aplico una transformación discreta de coseno (DCT en ingles), para esto se usó $$ y[k] = wk \sum_{n=1}^{n}x[n]\cos\frac{\pi(2n-1)(k-1)}{2N}$$, donde 

$$wk = \left\{\begin{array}{ll} \frac{1}{\sqrt{N}} & k=1\\ \frac{\sqrt{2}}{N} & 2 \leq k \leq N \end{array} \right.$$

Finalmente se obtuvieron un total de 75 muestras de audio de 5 diferentes personas que hacen un total de 375 caracteristicas (features).

<img src="https://k62.kn3.net/7/8/4/D/A/8/C56.png"/>

<p style="text-align: center;">Figura 2. Red neural que usaron para la clasificación</p>

Finalmente, para clasificar las caracteristicas que se obtuvieron con el preprocesamiento se unso una red neuronal de 3 capas donde la capa intermedia (capa oculta) cuenta con 20 neuronas, se usó el método de backpropagation para entrenar dicha red y se logró un 90.9%







 



#### Conclusiones

Proin bibendum, ante non dapibus dignissim, nulla diam lobortis sem, ac commodo arcu tellus eget arcu. Aenean non orci a ligula placerat sollicitudin. Fusce varius lacus imperdiet aliquam euismod. Sed tincidunt porta mattis. Phasellus sed arcu vehicula, iaculis lectus nec, rhoncus erat. Cras rhoncus ante at leo maximus dictum...



### Cepstral Analysis [***Deepa Kundur***]



### Algorithms for Vowel Recognition in Fluent Speech Based on Formant Positions [***Miroslav Stanek***]

### Scale Transform in Speech Analysis [***S. Umesh***]

### A Comparative Study of Formant Frequencies Estimation Techniques  [***Dorra Gargouri***]

### Malayalam Vowel Recognition Based On Linear Predictive Coding Parameters and k-NN Algorithm [***T. M. Thasleema***]

### On the performance of the quefrency-weighted cepstral coefficients in vowel recognition [***K.K. PALIWAL***]





## Conclusiones

