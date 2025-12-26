# Ajuste-S2-PICOFOX

## Fundamento

Los códigos del presente repositorio tiene por objetivo realizar un ajuste lineal para calibrar las mediciones del PICOFOX mediante dos esquemas diferentes, el primero busca determinar el factor de sensibilidad del instrumento frente a una determinada especie, mientras que el segundo determina un parámetro de corrección para las mediciones entregadas por este.

## Ajuste de factor de sensibilidad

El primer método se basa en lo descrito en el manual de usuario del instrumento S2 PICOFOX, donde se indica que el factor de sensibildad se calcula mediante la siguiente ecuación:

<img width="137" height="48" alt="lagrida_latex_editor" src="https://github.com/user-attachments/assets/ce1b13f2-3db4-427e-bc7b-59a6451c9ca9" />

Donde N_i y N_Ga corresponden al número de cuentas de la especie de interés y del Galio (estándar interno) respectivamente, mientras que C_i y C_Ga corresponden a las concentraciones de la especie de interés y del Galio respectivamente.

El código Ajuste_PICOFOX.ipynb requiere de un set de datos concentraciones y cuentas conocidas como entradas y entrega como salida un valor para el factor de sensibilidad del instumento frente a la especie de interés y opcionalmente la gráfica del ajuste (incluir en imputs: graf=True).

Se realiza un ajuste de parámetros por método de mínimos cuadrados a la siguiente función de ajuste basada en la ecuación del manual de usuario:

<img width="119" height="29" alt="lagrida_latex_editor (1)" src="https://github.com/user-attachments/assets/ec44e404-6b29-44bf-b2e5-e10bd14a1eab" />

Donde en cada punto la variable independiente (x) corresponde al siguiente coeficiente:

<img width="129" height="48" alt="lagrida_latex_editor (2)" src="https://github.com/user-attachments/assets/69db154f-f32c-4fb3-8ba7-941063bde36a" />

Mientras que la variable dependiente correspondería al número de cuentas de la especie de interés (N_i).

### Librerías requeridas

El código hace uso del las librerías de python: numpy, matplotlib.pyplot, scipy.optimize y scipy.stats.

### Imputs, outputs y sintaxis de la función

ajuste_lineal_PICOFOX(N_i, N_Ga, C_i, C_Ga, SI_0 = 1, graf = False, prt = False)

- N_i: lista de python que contenga set de datos de cuentas de especie de interés.
- N_Ga: lista de python que contega set de datos de cuentas de Galio.
- C_i: lista de pYthon que contenga set de datos de concentración de especie de interés.
- C_Ga: lista de python que contenga set de datos de concentración de Galio.
- SI_0: estimación inicial del factor de sensibilidad; tiene valor 1 por defecto.
- graf: indicador de graficación; True entrega gráfica del ajuste, False no entrega gráfica, tiene valor False por defecto.
- prt: indicador de impresión de valor; True imprime el valor del output, False no imprime ningún valor; tiene valor False por defecto.

El output de la función corresponde a la estimación del factor de sensibilidad (S_i).

## Ajuste directo de concentración

El segundo método ajusta un parámetro como factor de corrección de la concentración medida por el instrumento, asumiendo que esta es directamente proporcional a la concentración real del elemento de interés.

El modelo de ajuste de este esquema corresponde a una función lineal con intercepto igual a cero, de la siguiente forma:

<img width="248" height="23" alt="lagrida_latex_editor" src="https://github.com/user-attachments/assets/08999d7b-7706-4d44-b0a0-5794f3efcd9f" />

Donde C_corregida corresponde a la concentración corregida, P_corrección al parámetro de corrección y c a la concentración medida por el equipo. El parámetro de esta función se ajusta por método de mínimos cuadrados.

Cabe resaltar que el parámetro P_corrección sirve a la vez como medida de la precisión del instrumento, ya que cuanto más cercano a 1 sea su valor, más certera es la medición que el PICOFOX entrega para el elemento al que se le está calibrando.

### Librerías requeridas

El código hace uso del las librerías de python: numpy, matplotlib.pyplot, scipy.optimize y scipy.stats.

### Imputs, outputs y sintaxis de la función

corrector_conc_PICOFOX(C_PICOFOX, C_conocidas, FC_0 = 1, graf = False, r = False, prt = False)

- C_PICOFOX: lista de python que contenga set de datos de concentraciones medidas por el equipo de la especie de interés.
- C_conocidas: lista de python que contega set de datos de concentraciones conocidas de la especie de interés.
- FC_0: estimación inicial del parámetro de corrección; tiene valor 1 por defecto.
- graf: indicador de graficación; True entrega gráfica del ajuste, False no entrega gráfica, tiene valor False por defecto.
- r: indicador de impresión de coeficiente de correlación de pearson (r) entre los set de datos entregados; True imprime r, False no imprime ningún valor; tiene valor False por defecto.
- prt: indicador de impresión de valor; True imprime el valor del output, False no imprime ningún valor; tiene valor False por defecto.

El output de la función corresponde a la estimación del parámetro de corrección (P_correción).
