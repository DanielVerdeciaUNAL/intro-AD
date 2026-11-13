# Respuestas del taller de análisis multiobjetivo para problemas discretos

**Nombre:** Daniel Fernando Verdecia Goyeneche
**Documento:** 1006456802
**Curso:** Introducción al Análisis de Decisiones. Universidad Nacional de Colombia, Sede Medellín
**Profesora:** Patricia Jaramillo Álvarez, PhD

Las cifras de este documento provienen del cuaderno `TALLER_MO_DISCRETO_SELECCION_AUTOMOVIL.ipynb`.

## Caso: selección de un automóvil (Toyota, año modelo 2026)

Se reemplazaron los modelos del enunciado por seis Toyota 2026 que conservan su estructura (sedán, sedán híbrido, SUV de tres filas, SUV compacto, SUV mediano y minivan). Los costos de combustible y mantenimiento son valores a cinco años en USD (KBB), el precio es el MSRP base más el cargo de entrega (Toyota), la seguridad es la calificación global de la NHTSA y la carga se mide con todas las plazas en uso. Los detalles y las fuentes están en la sección 1 del cuaderno.

| Alternativa | Precio de compra (USD) | Combustible 5 años (USD) | Mantenimiento 5 años (USD) | Seguridad (1 a 5) | Carga (pies cúbicos) | Pasajeros |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| A1: Corolla Sedán | 24.320 | 4.365 | 1.780 | 5 | 13,1 | 5 |
| A2: Corolla Sedán Híbrido | 26.170 | 3.126 | 2.294 | 5 | 13,1 | 5 |
| A3: Grand Highlander SUV | 43.355 | 6.550 | 2.219 | 5 | 20,6 | 8 |
| A4: Corolla Cross SUV | 26.485 | 4.864 | 1.831 | 5 | 24,0 | 5 |
| A5: 4Runner SUV | 43.365 | 6.945 | 1.723 | 4 | 48,4 | 5 |
| A6: Sienna Minivan | 41.915 | 4.306 | 1.645 | 5 | 33,5 | 8 |

## 1. Alternativas dominadas

El algoritmo encuentra una sola alternativa dominada: **A3: Grand Highlander SUV**, dominada por **A6: Sienna Minivan**. El Sienna cuesta 1.440 USD menos en el precio de compra (41.915 frente a 43.355), gasta 2.244 USD menos en combustible y 574 USD menos en mantenimiento a cinco años. Tiene la misma calificación de seguridad (5 estrellas) y las mismas 8 plazas, y ofrece más espacio de carga (33,5 frente a 20,6 pies cúbicos). En el camino de valor y en la gráfica de araña se observa lo mismo: la línea del Grand Highlander nunca queda por encima de la del Sienna, y solo coincide con ella en seguridad y pasajeros.

Las otras cinco alternativas no son dominadas. El Corolla es el más barato, el Corolla Híbrido el de menor gasto de combustible, el Sienna el de menor mantenimiento y el 4Runner el de mayor carga. El Corolla Cross no tiene el mejor valor en ningún criterio (en seguridad comparte el máximo con otras cuatro alternativas), pero ofrece más carga que los dos sedanes con un precio cercano al del Corolla Híbrido, y ninguna alternativa lo supera en todos los criterios a la vez.

Eliminar el Grand Highlander no cambia el valor ideal ni el peor de ningún criterio, de modo que la normalización y las distancias de las otras cinco alternativas serían las mismas. Como la tabla del enunciado pide la jerarquía de las seis alternativas, se conservan en el cálculo y se interpreta el Grand Highlander como una alternativa que no puede resultar la mejor.

## 2. Programación de compromiso con pesos iguales

| Alternativa | Jerarquía compromiso p=1 | Jerarquía compromiso p=2 | Jerarquía compromiso p=infinito |
|---|:---:|:---:|:---:|
| A1: Corolla Sedán | 2 | 3 | 3 |
| A2: Corolla Sedán Híbrido | 4 | 4 | 3 |
| A3: Grand Highlander SUV | 5 | 5 | 2 |
| A4: Corolla Cross SUV | 3 | 2 | 3 |
| A5: 4Runner SUV | 6 | 6 | 3 |
| A6: Sienna Minivan | 1 | 1 | 1 |

Distancias al ideal que sustentan la jerarquía:

| Alternativa | Distancia p=1 | Distancia p=2 | Distancia p=infinito |
|---|:---:|:---:|:---:|
| A1: Corolla Sedán | 0,4221 | 0,2443 | 0,1667 |
| A2: Corolla Sedán Híbrido | 0,5162 | 0,2891 | 0,1667 |
| A3: Grand Highlander SUV | 0,5947 | 0,2984 | 0,1666 |
| A4: Corolla Cross SUV | 0,4244 | 0,2224 | 0,1667 |
| A5: 4Runner SUV | 0,6867 | 0,3339 | 0,1667 |
| A6: Sienna Minivan | 0,2758 | 0,1769 | 0,1540 |

**Comparación de las soluciones.** Las tres métricas coinciden en el primer lugar: **A6: Sienna Minivan**, con distancias de 0,2758 (p=1), 0,1769 (p=2) y 0,1540 (p=infinito). Ninguno de sus criterios está en el peor valor. Su punto débil es el precio, con una distancia normalizada de 0,92, pero lo compensa con el menor costo de mantenimiento, la mejor seguridad, ocho plazas y una carga intermedia. El Corolla, el Corolla Híbrido, el Corolla Cross y el 4Runner tienen al menos un criterio en su peor valor, y eso los deja más lejos del ideal en las tres métricas.

El Grand Highlander (quinto en p=1 y p=2) y el 4Runner (sexto en ambas) ocupan los dos últimos lugares. Esto es coherente con el análisis de dominancia: el primero está dominado por el Sienna y el segundo tiene la menor seguridad, el mayor costo de combustible y el precio más alto.

Entre el Corolla y el Corolla Cross hay un cambio de orden. Con p=1 el Corolla queda segundo y el Corolla Cross tercero, pero la diferencia es de solo 0,0024, prácticamente un empate. Con p=2 el Corolla Cross pasa adelante, porque la métrica euclidiana penaliza más los desempeños extremos y el Corolla tiene dos criterios en su peor valor (carga y pasajeros) frente a uno del Corolla Cross (pasajeros).

La métrica p=infinito aporta poca información en este caso. Solo mide el criterio con peor desempeño, y como el Corolla, el Corolla Híbrido, el Corolla Cross y el 4Runner tienen al menos un criterio en su peor valor, los cuatro obtienen la misma distancia máxima de 1/6 (0,1667) y quedan empatados en el tercer puesto. El Grand Highlander aparece segundo solo por una diferencia de 0,00009, que proviene de que su precio está 10 USD por debajo del peor valor (el del 4Runner). Es un efecto de la normalización y no una ventaja real, porque el Sienna lo domina.

**Conclusión.** Con pesos iguales el Sienna es la mejor alternativa de forma consistente. La conclusión es sólida porque las tres métricas la respaldan y porque el Sienna domina a una de las alternativas, mientras que ninguna lo domina a él.

## 3. Programación de compromiso con los pesos del decisor

**Perfil del decisor.** Comprador que usará el vehículo para transportar a su familia y que prioriza el costo (50 %) y la seguridad (30 %), y da menos peso a la capacidad (20 %). Dentro del costo, el precio pesa 50 %, el combustible 30 % y el mantenimiento 20 %. Dentro de la capacidad, los pasajeros pesan 60 % y la carga 40 %.

Pesos usados:

| Criterio | Wi |
|---|:---:|
| Precio de compra | 0,25 |
| Combustible | 0,15 |
| Mantenimiento | 0,10 |
| Seguridad | 0,30 |
| Carga | 0,08 |
| Pasajeros | 0,12 |

| Alternativa | Jerarquía compromiso p=1 | Jerarquía compromiso p=2 | Jerarquía compromiso p=infinito |
|---|:---:|:---:|:---:|
| A1: Corolla Sedán | 1 | 1 | 1 |
| A2: Corolla Sedán Híbrido | 4 | 3 | 1 |
| A3: Grand Highlander SUV | 5 | 5 | 5 |
| A4: Corolla Cross SUV | 2 | 2 | 1 |
| A5: 4Runner SUV | 6 | 6 | 6 |
| A6: Sienna Minivan | 3 | 4 | 4 |

Distancias al ideal que sustentan la jerarquía:

| Alternativa | Distancia p=1 | Distancia p=2 | Distancia p=infinito |
|---|:---:|:---:|:---:|
| A1: Corolla Sedán | 0,2695 | 0,1536 | 0,1200 |
| A2: Corolla Sedán Híbrido | 0,3243 | 0,1772 | 0,1200 |
| A3: Grand Highlander SUV | 0,5358 | 0,3038 | 0,2499 |
| A4: Corolla Cross SUV | 0,3006 | 0,1541 | 0,1200 |
| A5: 4Runner SUV | 0,8320 | 0,4354 | 0,3000 |
| A6: Sienna Minivan | 0,3111 | 0,2380 | 0,2310 |

**Comparación con los pesos iguales.** Sí hay una diferencia, y afecta a la alternativa ganadora. Con pesos iguales el Sienna es el primero en las tres métricas. Con los pesos del decisor baja al puesto 3 en p=1 y al puesto 4 en p=2 y p=infinito, y el primer lugar lo ocupa el **A1: Corolla Sedán** (en p=infinito lo comparte con el Corolla Híbrido y el Corolla Cross). La causa es que el perfil asigna 50 % al costo, y el Sienna es uno de los tres vehículos más caros (41.915 USD, con una distancia normalizada de 0,92 al mejor precio). Sus ventajas en pasajeros y mantenimiento pesan menos en este perfil, con 12 % y 10 % respectivamente.

Otros aspectos no cambian. Con p=1 y p=2, los mismos cuatro vehículos (Corolla, Corolla Cross, Corolla Híbrido y Sienna) ocupan los cuatro primeros puestos en ambos escenarios, y el Grand Highlander y el 4Runner siguen en el quinto y el sexto lugar. El peso de 30 % en seguridad no altera el orden entre los cinco modelos con cinco estrellas, porque todos tienen distancia cero en ese criterio. Su efecto es castigar al 4Runner (cuatro estrellas), que ya era el último con pesos iguales.

En p=infinito, el Corolla, el Corolla Híbrido y el Corolla Cross empatan en 0,12. Los tres tienen cinco plazas, que es el peor valor en pasajeros, y el peso de ese criterio (0,12) define su distancia máxima. Con p=2 la diferencia entre el Corolla y el Corolla Cross es de solo 0,0005, por lo que también se pueden considerar empatados en esa métrica.

**Conclusión y elección.** Elegiría el **Toyota Corolla (A1)**, por las siguientes razones:

1. Ocupa el primer lugar con p=1 y con p=2, y comparte el primero con p=infinito, es decir, es la mejor alternativa o una de las mejores en las tres métricas.
2. Es el vehículo más barato en precio (24.320 USD) y el de menor costo total a cinco años (30.465 USD, sumando precio, combustible y mantenimiento), que son los criterios con mayor peso en mi perfil.
3. Tiene la calificación máxima de seguridad de la NHTSA (cinco estrellas).

El Corolla cede en carga (13,1 pies cúbicos, la más baja junto con el Corolla Híbrido) y en número de plazas (cinco, frente a las ocho del Sienna y del Grand Highlander). Ambos criterios pertenecen a Capacidad, que en mi perfil pesa 20 %, por eso la decisión resulta aceptable. El Corolla Híbrido, aunque gasta 1.239 USD menos en combustible en cinco años, cuesta 1.850 USD más de compra y 514 USD más en mantenimiento, de modo que su costo total a cinco años es 1.125 USD mayor, y el ahorro de combustible no compensa ese sobrecosto.

La elección depende de las necesidades que representa el perfil. Si se requiriera más espacio de carga sin salir de las alternativas de menor costo, la opción sería el Corolla Cross (24,0 pies cúbicos), a cambio de 2.715 USD más a cinco años. Si hubiera que transportar ocho personas, la mejor opción sería el Sienna, que con pesos iguales es la primera y que supera al Grand Highlander, la otra alternativa de ocho plazas, en los dos escenarios.
