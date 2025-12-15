# Ajuste-S2-PICOFOX

## Fundamento

El código del presente repositorio tiene por objetivo realizar un ajuste lineal para determinar el factor de sensibilidad del instrumento frente a una determinada especie.

Este método se basa en lo descrito en el manual de usuario del instrumento S2 PICOFOX, donde se indica que el factor de sensibildad se calcula mediante la siguiente ecuación:

<img width="137" height="48" alt="lagrida_latex_editor" src="https://github.com/user-attachments/assets/ce1b13f2-3db4-427e-bc7b-59a6451c9ca9" />

Donde N_i y N_Ga corresponden al número de cuentas de la especie de interés y del Galio (estándar interno) respectivamente, mientras que C_i y C_Ga corresponden a las concentraciones de la especie de interés y del Galio respectivamente.

El código requiere de un set de datos concentraciones y cuentas conocidas como entradas y entrega como salida un valor para el factor de sensibilidad del instumento frente a la especie de interés y opcionalmente la gráfica del ajuste (incluir en imputs: graf=True).

Se realiza un ajuste de parámetros por método de mínimos cuadrados a la siguiente función de ajuste basada en la ecuación del manual de usuario:

<img width="119" height="29" alt="lagrida_latex_editor (1)" src="https://github.com/user-attachments/assets/ec44e404-6b29-44bf-b2e5-e10bd14a1eab" />

Donde en cada punto la variable independiente (x) corresponde al siguiente coeficiente:

<img width="129" height="48" alt="lagrida_latex_editor (2)" src="https://github.com/user-attachments/assets/69db154f-f32c-4fb3-8ba7-941063bde36a" />

Mientras que la variable dependiente correspondería al número de cuentas de la especie de interés (N_i).

## Librerías requeridas

El código hace uso del las librerías de python: numpy, matplotlib.pyplot, scipy.optimize y scipy.stats.

## Imputs, outputs y sintaxis de la función

ajuste_lineal_PICOFOX(N_i, N_Ga, C_i, C_Ga, SI_0 = 1, graf = False, prt = False)

- N_i: lista de python que contenga set de datos de cuentas de especie de interés.
- N_Ga: lista de python que contega set de datos de cuentas de Galio.
- C_i: lista de pYthon que contenga set de datos de concentración de especie de interés.
- C_Ga: lista de python que contenga set de datos de concentración de Galio.
- SI_0: estimación inicial del factor de sensibilidad; tiene valor 1 por defecto.
- graf: indicador de graficación; True entrega gráfica del ajuste, False no entrega gráfica, tiene valor False por defecto.
- prt: indicador de impresión de valor; True imprime el valor del output, False no imprime ningún valor; tiene valor False por defecto.

El output de la función corresponde a la estimación del factor de sensibilidad (S_i).
