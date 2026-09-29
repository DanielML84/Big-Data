# Bubble Sort (ordenación de burbuja)

*Máster de FP en IA y Big Data · Sistemas de Big Data · Sesión 01*

## 1. Qué es y cómo funciona

Bubble Sort es un algoritmo de ordenación muy sencillo. Recorre la lista comparando cada elemento con el siguiente; si están en el orden equivocado, los intercambia. Tras cada pasada completa, el mayor de los elementos que quedaban sin ordenar "burbujea" hasta su posición final, al final de la lista. Se repite hasta que en una pasada no hace falta intercambiar nada.

### Ejemplo paso a paso con [5, 3, 8, 1]

- **Pasada 1:** (5,3) se intercambian → [3,5,8,1]; (5,8) no; (8,1) se intercambian → [3,5,1,8]. El 8 ya está en su sitio.
- **Pasada 2:** [3,1,5,8]. Ya están colocados el 5 y el 8.
- **Pasada 3:** [1,3,5,8]. Lista ordenada.

## 2. Código en Python

```python
def bubble_sort(lista):
    n = len(lista)
    for i in range(n - 1):
        hubo_intercambio = False
        for j in range(n - 1 - i):      # el final ya está ordenado
            if lista[j] > lista[j + 1]:
                lista[j], lista[j + 1] = lista[j + 1], lista[j]
                hubo_intercambio = True
        if not hubo_intercambio:        # si no cambió nada, ya está ordenada
            break
    return lista
```

**Qué hace cada parte:** el bucle exterior cuenta las pasadas; el interior compara vecinos y llega cada vez un elemento menos lejos, porque el final ya está ordenado; la variable `hubo_intercambio` permite parar antes si la lista ya estaba ordenada. Esa optimización es la que hace que el mejor caso sea O(n).

## 3. Complejidad

| Caso     | Complejidad | Cuándo ocurre |
|----------|-------------|---------------|
| Mejor    | O(n)        | Lista ya ordenada, con la parada anticipada: una sola pasada sin intercambios. Sin esa optimización sería O(n²) también. |
| Peor     | O(n²)       | Lista en orden inverso: hacen falta todas las pasadas y todos los intercambios. |
| Promedio | O(n²)       | Lista desordenada al azar. |

- **Comparaciones en el peor caso:** n(n−1)/2, de ahí el término n².
- **Espacio:** O(1). Es in-place, no necesita lista auxiliar.
- **Estable:** sí, los elementos iguales mantienen su orden relativo.

## 4. ¿Es adecuado para Big Data?

**No.** El crecimiento es cuadrático: al multiplicar por 10 el número de datos, el tiempo se multiplica por 100.

## 5. Vídeo recomendado

Bubble Sort - Bubble Sort Algorithm - Algoritmo de Ordenación Burbuja - Java:

<https://www.youtube.com/watch?v=Nt0_NcSDSRw>

## 7. Puesta en común (15 min)

### Guion para exponer (1-2 minutos)

- **Qué hace:** compara elementos vecinos y los intercambia si están mal ordenados; en cada pasada el mayor "burbujea" hasta el final.
- **Complejidad:** mejor caso O(n) con parada anticipada; caso promedio y peor caso O(n²). Espacio O(1) y estable.
- **Por qué no sirve para Big Data:** con 10 millones de registros serían del orden de 10¹⁴ operaciones, unos 3 años en el modelo teórico, frente a segundos con un O(n log n).
- **Conclusión:** útil para aprender, no para datos masivos.

### Debate: ¿qué usaríamos para ordenar 10 millones de registros?

- **Timsort (`sorted()` / `.sort()` de Python):** O(n log n) en el peor caso y O(n) en el mejor, estable, aprovecha tramos ya ordenados. Es la opción práctica si los datos caben en memoria.
- **Merge Sort:** O(n log n) en todos los casos, predecible. Cuesta O(n) de memoria extra.
- **Quick Sort:** muy rápido en promedio, pero su peor caso es O(n²) si se elige mal el pivote.
- **External Merge Sort:** si los datos no caben en memoria, se ordenan por trozos y se mezclan. Es la idea en la que se basan muchos sistemas de Big Data.

**Propuesta:** Timsort o Merge Sort si caben en RAM, y External Merge Sort si no. Es una propuesta para contrastar con la pareja y con el resto de la clase.

## 8. Fuentes para citar

- Material de la sesión 01 (SBD 5074): tabla de complejidad y ejercicio de tiempos.
- YouTube
- Big O Cheat Sheet (bigocheatsheet.com) para contrastar las complejidades.
