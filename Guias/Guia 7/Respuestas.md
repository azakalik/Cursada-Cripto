# Ejercicio 1
## Enunciado
- P lee k
- Q no lee k
- Cuando p lee d, ve todos los archivos en el directorio y puede escribir sus propios archivos
- Cuando q lee d, no ve ni puede leer archivos creados por p
- Si un proceso trata de crear un archivo que ya existe en el directorio, entonces el archivo no es creado y se envía una señal de error al proceso
- Si un proceso trata de borrar un archivo que no existe o existe pero pertenece a otro proceso, entonces el archivo no es borrado y se envía una señal de error al proceso.
## Respuesta
- La idea es probar viendo el codigo que es posible 

# Ejercicio 2
Fluye informacion porque el valor de $Y$ termina siendo igual al valor de $X$.
Por lo tanto, $H(X | Y) < H(X)$, osea la entropia de $X$ dado $Y$ es menor a la entropia de $X$

# Ejercicio 3
## Parte A
- $H(X) = 1$ porque tiene dos valores posibles
- $H(Y) = 1$ porque tiene dos valores posibles
## Parte B
- $P(Z' = 0) = P(X=0 \land Y=0) \land P(X=0 \land Y=1) \land P(X=1 \land Y=0) = 0.75$
## Parte C
$H(X|Z') = $