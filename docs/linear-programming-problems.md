# Problema

# P1

## Enunciado

**Alimentación de vacas**
Una granjera quiere asegurar de que sus vacas reciban un dieta diara que contenga al menos **22 gramos (g) de grasa**, **38g de carbohidratos** y **7 g de proteína**. Además, desea que la dieta diaria de cada vaca contenga como máximo **4g de sodio** y **5g de potasio**. Tiene acceso a 3 alimentos diferentes: alimento X, Y y Z que puede mezclar para crear una mezcla para las vacas.

- El alimento X contiene 7g de grasa, 10g de carbohidratos, 3g de proteína, 1g de sodio y 4g de potasio y tiene un precio de **$0.25 por onza**.
- El alimento Y contiene 12g de grasa, 12g de carbohidratos, 1g de proteína, 1g de sodio y 2g de potasio y tiene un precio de **$0.30 por onza**.
- El alimento Z contiene 8g de grasa, 12g de carbohidratos, 3g de proteína, 5g de sodio y 5g de potasio y tiene un precio de **$0.20 por onza**.

Formular un programa lineal que determine una mezcla de los alimentos X, Y, y Z que satisfaga los requerimientos nutricionales de una vaca al menor costo posible.

## Solución

**Variables de decisión**

- $x = $ onzas del alimento X.
- $y = $ onzas del alimento Y.
- $z = $ onzas del alimento Z.

**Función Objetivo**
Minimizar $\rightarrow$ $0.25x + 0.3y + 0.2z$

**Restricciones**
De grasa

- $7x + 12y + 8z \ge 22$

De carbohidratos

- $10x + 12y + 12z \ge 38$

De proteína

- $3x + y + 3z \ge 7$

De sodio

- $x + y + 5z \le 5$

De potasio

- $4x + 2y + 5z \le 5$

De no negatividad

- $x, y, z \ge 0$
