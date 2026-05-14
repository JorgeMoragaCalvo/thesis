# Problemas

## P1

### Enunciado

**Alimentación de vacas**
Una granjera quiere asegurar de que sus vacas reciban un dieta diara que contenga al menos **22 gramos (g) de grasa**, **38g de carbohidratos** y **7 g de proteína**. Además, desea que la dieta diaria de cada vaca contenga como máximo **4g de sodio** y **5g de potasio**. Tiene acceso a 3 alimentos diferentes: alimento X, Y y Z que puede mezclar para crear una mezcla para las vacas.

- El alimento X contiene 7g de grasa, 10g de carbohidratos, 3g de proteína, 1g de sodio y 4g de potasio y tiene un precio de **$0.25 por onza**.
- El alimento Y contiene 12g de grasa, 12g de carbohidratos, 1g de proteína, 1g de sodio y 2g de potasio y tiene un precio de **$0.30 por onza**.
- El alimento Z contiene 8g de grasa, 12g de carbohidratos, 3g de proteína, 5g de sodio y 5g de potasio y tiene un precio de **$0.20 por onza**.

Formular un programa lineal que determine una mezcla de los alimentos X, Y, y Z que satisfaga los requerimientos nutricionales de una vaca al menor costo posible.

### Solución

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

## P2

### Enunciado

Se quiere producir mermelada de ruibardo y fresa. Un tarro de mermelada de ruibardo requiere de **1 kg de ruibardo** y **3 kg de azúcar** y la ganancia es de `$3000` por tarro. Un tarro de fresa requiere **2k de fresas** y **2 kg de azúcar** y la ganancia es de `$4000` por tarro. Las cantidades disponibles son 4 kg de ruibardo, 12 kg de fresas y 18 kg de azúcar. Se quiere maximizar la ganancia.

### Solución

**Variables de decisión**

- $x_r = $ cantidad de tarros de ruibardo a producir.
- $x_f = $ cantidad de tarros de fresas a producir.

**Función Objetivo**
Maximizar $\rightarrow$ $3000x_r + 4000x_f$

**Restricciones**
De ruibardo

- $x_r \le 4$

De fresas

- $x_f \le 12$

De azúcar

- $3x_r + 2x_f \le 18$

De no negatividad

- $x_r, x_f \ge 0$
