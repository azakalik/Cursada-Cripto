# Ejercicio 1
## Punto 1
$Mac_k(m) =  G(k) \oplus m$, donde $G(x)$ generador pseudoaleatorio
No posee seguridad porque se puede montar el siguiente MAC-Forge:
- El atacante tiene acceso a $Mac_k(m)$
- El atacante pregunta por $Mac_k(000...0)$, y obtiene $G(k) \oplus 000...0$ como respuesta, que es igual a $G(k)$
- El atacante ahora puede emitir cualquier mensaje $X$, junto a $G(k) \oplus X$ como MAC, ya que conoce ambos valores, por lo que ganara la prueba
## Punto 2
$Mac_k(m) = k \oplus first\_n\_bits(m)$
Siempre que $|k| < |m|$, el atacante puede pedir el MAC de 000...000, y emitir el mensaje 000...001 con el mismo MAC, asi ganando la prueba.
Otra opcion podria ser pedir el MAC de $0^n$, y emitir ese MAC junto a el mensaje $0^{n+1}$
## Punto 3
$Mac_k(m) = Enc_k(|m|)$
El atacante puede elegir cualquier $m_1$ y pedir su MAC. Luego, el atacante envia ese MAC junto a cualquier $m_2$ tal que $|m_1| = |m_2|$
# Ejercicio 2
## Punto A
El atacante podria emitir $m_1 = 128\ bits\ en\ 0\ ||\ 128\ bits\ en\ 1$ y $m_2 = 128\ bits\ en\ 1\ ||\ 128\ bits\ en\ 0$.
Es facil darse cuenta que $m_1 \oplus m_2 = m_2 \oplus m_1$, por lo que MAC(m1) = MAC(m2)
# Ejercicio 3
Esta funcion de hash NO es valida para criptografia. Evaluemos los tres niveles de seguridad
## Resistencia a preimagenes
- Objetivo, dado $H(x) = Y$, encontrar $x$
- Supongamos que el atacante recibe $Y = 000...0$. Entonces ya sabe que $x$ debe tener un numero par de caracteres
- El atacante emite $x = 00$ y gana la prueba
## Resistencia a segundas preimagenes
- Objetivo: dado $x$ y $H(x) = Y$, encontrar $x'$ tal que $H(x') = Y)$
- Supongamos que el atacante recibe $x = 00$. El atacante entonces puede emitir $x' = 0000$, que tendra el mismo hash
## Resistencia a colisiones
- Objetivo: encontrar pares $(x_1,\ x_2)$ tal que $H(x_1) = H(x_2)$
- El atacante puede emitir $x_1 = 0$ y $x_2 = 000$, y ambos tendran el mismo hash
# Ejercicio 4
## Punto A
La funcion MAC sirve para generar una etiqueta a partir de un mensaje y una clave. La idea por detras de CBC-MAC, es poder generar una etiqueta a partir de un mensaje muy largo, partiendolo en bloques. Sin embargo, CBC-MAC a secas solo sirve para mensajes de longitud FIJA. De lo contrario, es susceptible a ataques de extension.
La construccion es la siguiente:
- Partir el mensaje en bloques de igual largo tal que $m = m_1m_2m_3...m_n$
- Calcular el MAC de la siguiente forma:
	- $MAC_k(m_j) = t_j$
	- $t_j = F_k(m_j \oplus t_{j-1})$ tal que $t_0 = 000...0$
	- $MAC_k(m) = t_n$
## Punto B
CBC-MAC nos permite expandir MAC para aceptar mensajes de longitudes muy largas. CBC-mode, nos permite expandir un criptosistema simetrico para cifrar mensajes de longitudes muy largas.
La construccion de CBC-mode es:
- Dividir un mensaje en partes iguales tal que $m = m_1m_2m_3...m_n$
- Elegir un IV aleatorio con la misma longitud que $m_t$
- $c_1 = ENC_k(m_1 \oplus IV)$
- $c_t = ENC_k(c_{t-1} \oplus m)$