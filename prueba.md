---

## Universidad de Costa Rica
### Escuela de Ingeniería Eléctrica
#### IE0405 - Modelos Probabilísticos de Señales y Sistemas

Segundo semestre del 2020

---

* Estudiante: **Jorge Daniel Rodríguez Hernández**
* Carné: **A95284**
* Grupo: **2**

# `L4` - *Proceso aleatorio sinusoidal en fase y en cuadratura*

Para darle solución a un proceso aleatorio sinusoidal en fase y cuadratura se decidio utilizar el codigo provisto para este fin por el profesor,
alterando las lineas de codigo pertinentes se logró alcanzar la solucion de dicho proceso aleatorio de manera satisfactoria, se procederá 
a realizar una breve explicacion del codigo y los resultados obtenidos.

Se importan todas las bibliotecas de python a utilizar

```python
import numpy as np
from scipy import stats
import matplotlib.pyplot as plt
```
se crean las constantes, las variables aleatorias y los vectores con los datos de las variables aleatorias que cumplen con los requerimientos del enunciado 
y se procede a evaluar los datos dentro de la función y se almacena los resultados.

```python

# Creación del vector de tiempo y frecuencia
T = 100			# número de elementos
t_final = 10	# tiempo en segundos
t = np.linspace(0, t_final, T)
wo = 3 
varianza_cuad = 8
media = 0

# Variables aleatorias A y Z
vaX = stats.norm(media, np.sqrt(varianza_cuad))
vaY = stats.norm(media, np.sqrt(varianza_cuad))

# Inicialización del proceso aleatorio X(t) con N realizaciones
N = 12
W_t = np.empty((N, len(t)))	# N funciones del tiempo x(t) con T puntos

# Creación de las muestras del proceso x(t) (A y Z independientes)
for i in range(N):
	X = vaX.rvs()
	Y = vaY.rvs()
	w_t =  X * np.cos(wo*t) +  Y * np.sin(wo*t)
	W_t[i,:] = w_t
	assert isinstance(w_t, object)
	plt.plot(t, w_t)
```
Se grafica los datos obtenidos en funcion del tiempo y la media.
```python
# Promedio de las N realizaciones en cada instante (cada punto en t)
P = [np.mean(W_t[:,i]) for i in range(len(t))]
plt.plot(t, P, lw=4)

# Graficar el resultado teórico del valor esperado
E = 0*t
plt.plot(t, E, '-.', lw=4)

# Mostrar las realizaciones, y su promedio calculado y teórico
plt.title('Realizaciones del proceso aleatorio $X(t)$')
plt.xlabel('$t$')
plt.ylabel('$x_i(t)$')
plt.show()
```
Se obtuvo la siguiente grafica

![Proceso Aleatorio](https://github.com/jorgedaniel-rodriguez/Tema4/blob/main/Proceso_aleatorio.png)

