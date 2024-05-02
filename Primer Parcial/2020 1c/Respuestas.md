# Ejercicio 1
![](Pasted%20image%2020240430180607.png)
La primera es verdadera.
# Ejercicio 2
![](Pasted%20image%2020240430180705.png)
Falso. La encripcion de cada $C_n$ en CBC requiere de $C_{n-1}$.
La encripcion CBC tiene el siguiente esquema:
$C_1 = ENC_k(m_1 \oplus IV)$
$C_n = ENC_k(m_n \oplus C_{n-1})$
# Ejercicio 3
![](Pasted%20image%2020240430181137.png)
Falso. MAC no sirve para encriptar un mensaje, sirve para generar una etiqueta.
# Ejercicio 4
![](Pasted%20image%2020240430181245.png)
Falso. Las firmas digitales estan basadas en algoritmos de encripcion asimetricos.
# Ejercicio 5
![](Pasted%20image%2020240430181520.png)
FALSO
# Ejercicio 6
![](Pasted%20image%2020240430181621.png)
# Ejercicio 7
## Punto A
El proposito de los nonces es evitar ataques del tipo **replay**. De esta manera, un atacante no puede guardar mensajes viejos y repetirlos mas adelante, porque no tendran el mismo nonce.
## Punto B
La generacion de A* y B* podria implementarse utilizando algun algoritmo de MAC
# Ejercicio 8
![](Pasted%20image%2020240501215903.png)
El cifrado simetrico DES (Data Encryption Standard) fue creado por IBM y perfeccionado por el departamento de defensa de USA. La idea de este cifrado, era poder cifrar mensajes de longitud variable, dividiendolo en partes y haciendo una serie de iteraciones que iba mezclando dichas partes.
Si alguien propusiera usar este protocolo, le diria que no se puede bajo ningun concepto, dado que en 1992 se encontro una forma especial de ataque que reducia la seguridad de DES a niveles peligrosos. Es por eso que hoy en dia se recomienda usar 3-DES, cuyas claves tienen una longitud de encripcion de 112 bits y no se pueden romper con fuerza bruta.\
# Ejercicio 9
![](Pasted%20image%2020240501220241.png)
Suponemos que el mensaje es $00$
- Hay 33% de probabilidades de la clave sea $00$ -> hay 33% de probabilidades que que el cifrado sea $11$
- Hay 33% de probabilidades de la clave sea $01$ -> hay 33% de probabilidades que que el cifrado sea $10$
- Hay 33% de probabilidades de la clave sea $11$ -> hay 33% de probabilidades que que el cifrado sea $00$
Repitiendo lo anterior para los mensajes $01$ y $10$, vemos que la probabilidad de que un mensaje cifrado $c$ sea igual a un texto plano $m$ es igual para cualquier $m$ del espacio de mensajes.
Por este motivo, podemos considerar que tenemos garantias de seguridad.
Si realizamos Eavesdropping:
- El atacante emite $m_1$ y $m_2$
- El atacante recibe $c$
- El atacante no tiene forma de determinar con certeza != 50% cual de los mensajes era el que se encripto