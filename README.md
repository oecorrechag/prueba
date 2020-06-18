# Proyecto Montreal
# <center> Analisis y ajuste de la serie de tiempo de la energia electrica en Colombia entre 1995 - 2018.
Actividad Final Clase Fundamentos de Analitica
Actividad Final Clase Redes Neuronales
  
**Universidad Nacional de Colombia**

La energía eléctrica es la forma de energía que resulta de la existencia de una diferencia de potencial entre dos puntos, lo que permite establecer una corriente eléctrica entre ambos cuando se los pone en contacto por medio de un conductor eléctrico. La energía eléctrica puede transformarse en muchas otras formas de energía, tales como la energía lumínica o luz, la energía mecánica y la energía térmica.

Actualmente la energía eléctrica se puede obtener de distintos medios, que se dividen principalmente en:

* Renovables:
  + Centrales termoeléctricas solares
  + Centrales solares fotovoltaicas
  + Centrales eólicas
  + Centrales hidroeléctricas    (Principal en Colombia)
  + Centrales geo-termoeléctricas
* No renovables:
  + Centrales nucleares
  + Combustibles fósiles:

**Problema**

Se cuenta con 23 archivos en los cuales se encuentra los precios diarios por hora de la energía eléctrica, los archivos tienen de diferentes extensiones y con diferentes dimensiones. Se necesita lectura de estos, unificación, análisis y realizar el ajuste por redes neuronales (tipo a consideración), encontrar el rezago pertinente y los hiperparámetros que mejor ajusten el modelo.

**Objetivo**

Realizar el estudio la estructura temporal o dinámica de los datos de la energía eléctrica en Colombia para posteriormente realizar pronóstico del precio.

**Análisis** 

Se encontraron 238 registros nulos y 1951 registros duplicados que fueron retirados. Se organiza la serie de tiempo por precio medio diario.

![alt text](https://github.com/oecorrechag/Proyecto-Montreal-Energia/blob/master/mean_day.png)

**Nota:** El pico que se encuentra entre los años 2015 y 2016 se debe al fenomeno del niño, por lo que no se debe ni modificar ni retirar. 

![alt text](https://github.com/oecorrechag/Proyecto-Montreal-Energia/blob/master/maximo_laborales.png)

De la figura anterior se observa que para los días entre lunes a viernes (días laborales), el precio máximo por hora se presenta entre las 6 y las 9 (horario prime time) las horas con el precio mayor de energía eléctrica. Los días no laborales también presentan los mayores precios en horario prime time, pero con precios menores que los días laborales.

![alt text](https://github.com/oecorrechag/Proyecto-Montreal-Energia/blob/master/dia.png)

De la figura anterior se observa que el precio promedio es mayor al iniciar el mes, y esto va decayendo gradualmente a través del mes. 

![alt text](https://github.com/oecorrechag/Proyecto-Montreal-Energia/blob/master/mes.png)

De la figura anterior se observa que el precio promedio es mayor en los meses de marzo y octubre siendo estos los meses correspondientes a temporada húmeda, y precios bajos entre los meses de diciembre a marzo y julio a agosto, meses correspondientes a temporada seca.

![alt text](https://github.com/oecorrechag/Proyecto-Montreal-Energia/blob/master/serie.PNG)

![alt text](https://github.com/oecorrechag/Proyecto-Montreal-Energia/blob/master/serie_diaria.png)

De las dos anteriores graficas se puede observar que la serie se suavisa, sin embargo la serie que se ajustara seria la segunda, promedio diario.

**Nota:** El resto del análisis se encuentra en el archivo Python.

**Modelo**

![alt text](https://github.com/oecorrechag/Proyecto-Montreal-Energia/blob/master/modelo.PNG)

Se realizo un ajuste de una red neuronal LSTM con un rezago de L = 3, función de perdida MSE, y optimizador Adam. 

![alt text](https://github.com/oecorrechag/Proyecto-Montreal-Energia/blob/master/fit.png)

De la figura anterior el modelo se ajusta bien hasta llegar a octubre 2015, donde el modelo no logra ajustar correctamente los precios, sin embargo, los demás precios si logra predecirlos lo mejor posible, por lo cual es necesario más datos o modificar la arquitectura usada.

**Resultados y conclusiones**

Se obtuvo un RSME 11.79 en train y 111.5 en test, esta diferencia de error se da por el fenómeno del niño. Para un próximo análisis se realizará un ajuste con redes neuronales convolucionales, otro ajuste con modelos para series de tiempo clásicos (ARIMAS), otro ajuste reduciendo el tamaño de test ya que se cuenta con una gran cantidad de datos y otro ajuste omitiendo los datos afectados por el fenómeno del niño. 

**Bibliografia**

Comisión de regulación de energía y gas (CREG). (2020). Estructura Tarifaria. [Figura]. Recuperado de: https://www.creg.gov.co/

Keras. (2020). LSTM layer. Recuperado de: https://keras.io
