# Ejercicio 1
![](Pasted%20image%2020240318162408.png)
## Parte A
- $P(c=1) = P(m=a) \cdot P(k=k_1) = 0.25 \cdot 0.5 = 0.125$
- $P(c=2) = ( P(m=a) \cdot P(k=k_2) ) + ( P(m=b) \cdot P(k=k_1))$
  $= 0.25 \cdot 0.25 + 0.75 \cdot 0.5$
  $= 0.4375$
- $P(c=3) = (P(k=k_2) \cdot P(m=b)) + (P(k=k_3) \cdot P(m=a))$
  $= 0.25 \cdot 0.75 + 0.25 \cdot 0.25$
  $= 0.25$
- $P(c=4) = P(k=k_3) \cdot P(m=b) = 0.25 \cdot 0.75 = 0.1875$
- NOTA: las probabilidades suman 1 -> esta bien hecho
## Parte B
### Forma 1
Objetivo: probar que $P(m) \neq P(m|c)$
- Tomo $m=a$ y $c=1$
- $P(m=a) = 0.25$
- $P(m=a|c=1) = 1$
- Podemos ver que no hay secreto perfecto
### Forma 2
Objetivo: probar que $P(c) = P(c|m)$
- Tomo $c=4$ y $m=b$
- $P(c=4) = 0.1875$
- $P(c=4|m=b) = P(k=k_3) = 0.25$
- Podemos ver que no hay secreto perfecto
## Forma 3
Objetivo: probar que $P(c|m1) = P(c|m2)$
- Tomo $c=4$, $m_1=a$, $m_2 = b$
- $P(c=4|m=a) = 0$
- $P(c=4|m=b) = P(k=k_3) = 0.25$
- Podemos ver que no hay secreto perfecto
## Forma 4
Objetivo: definir $m_1$ y $m_2$ tal que no pueda adivinar cual es el mensaje cifrado
- Defino $m_1 = a$, $m_2 = b$, obtengo $c = 1$.
- Podemos ver que no hay secreto perfecto, porque si obtengo $c=1$ solo es posible que $m=m_1$.

# Ejercicio 2
![](Pasted%20image%2020240318171342.png)
La afirmacion es **VERDADERA**. Esto se debe a que un requerimiento del secreto perfecto es que, dado un texto cifrado, la probabilidad de que el mensaje plano sea $m$ es igual para cualquier $m \in C$.

# Ejercicio 3
![](Pasted%20image%2020240318171735.png)
## Parte A
Si se encripta un solo simbolo, el cifrado de rotacion tiene secreto perfecto porque $P(M=m|C=c)$ es igual para cualquier $m$ perteneciente al espacio de mensajes.
Ademas, estariamos haciendo un One Time Pad.
## Parte B
?
## Parte C
Si usamos cifrado de Vigenere y definimos una clave de longitud igual a la longitud del mensaje, tenemos secreto perfecto.
Esto se debe a que cuando las longitudes son iguales, el Vigenere se convierte en One Time Pad. Esta demostrado por teorema que todo lo que se pueda descomponer en One Time Pad es secreto perfecto.
# Ejercicio 4
![](Pasted%20image%2020240318173738.png)
## Parte A
El criptosistema elige el periodo 2, y luego elige la clave AB. Para cifrar el mensaje HOLA, le suma 1 a las letras H, L y le suma 2 a las letras O, A. El mensaje cifrado queda: IQOC.
## Parte B
Primero tenemos en cuenta que:
- $P(b'=0) = P(c=XXY)$, con $X,Y \in \Sigma$
Calculamos:
- $P(C=XXY|(m=aab \land t=1)) = 1$ porque las primeras dos letras siempre van a rotar igual, entonces la primera letra siempre va a ser igual a la segunda
- $P(C=XXY|(m=abb \land t=1)) = 0$ porque las primeras dos letras siempre van a rotar igual, entonces la primera letra siempre va a ser distinta de la segunda
- $P(C=XXY|(m=aab \land (t=2 \lor t=3))) = \frac 1 {26}$ porque queremos que la primera letra de la clave de cifrado sea igual a la segunda. Esto tiene una probabilidad de $\frac 1 {26}$.
-  $P(C=XXY|(m=abb \land (t=2 \lor t=3))) = \frac 1 {26}$ porque queremos que la primera letra de la clave de cifrado este un lugar a la izquierda de la segunda. Esto tiene una probabilidad de $\frac 1 {26}$.
Teniendo en cuenta los resultados anteriores, tenemos que:

$$
P(b'=0|m=aab)
= \frac 1 3 P(C=XXY|(m=aab \land t=1)) + \frac 2 3 P(C=XXY|(m=aab \land (t=2 \lor t=3)))
= \frac 1 3 \cdot 1 + \frac 2 3 \cdot \frac 1 {26}
= 0.410
$$

tambien sabemos que:

$$
P(b'=0|m=abb)
= \frac 1 3 P(C=XXY|(m=abb \land t=1)) + \frac 2 3 P(C=XXY|(m=abb \land (t=2 \lor t=3)))
= \frac 1 3 \cdot 0 + \frac 2 3 \cdot \frac 1 {26}
= 0.077
$$

Como conclusion, tenemos que hay mas chances de que el atacante devuelva 0 si el mensaje original es $aab$, por lo que no es un mensaje perfecto.
## Parte C
Por lo expuesto en el parrafo anterior, no estamos hablando de un secreto perfecto.
# Ejercicio 5
Demo, se saltea
# Ejercicio 6
Con el modo ECB, si hay un error en un bloque del texto cifrado transmitido, solamente afecta al bloque de texto claro correspondiente.
## Parte A
**En el modo CBC (ver figura) un error de un bit en P1, a través de cuántos bloques de texto cifrado se propaga?**
![](Pasted%20image%2020240325164124.png)
El CBC utiliza una encripcion secuencial, en donde cada bloque utiliza un cifrado que proviene del bloque anterior. Esto significa que si falla un bit en el primer bloque, todo el resto de los mensajes se encriptara de forma incorrecta, por lo que no se podra desencriptar.

## Parte B
**En el modo CBC, un error de un bit en C1, a través de cuántos bloques de texto descrifrado se propaga?**
Un error en c1 afecta al descifrado de P1 y P2, porque ambos necesitan c1 para descifrar el mensaje adecuado.

## Parte C
**Si se produce un error de un bit en la transmisión de un carácter del texto cifrado en modo CFB de ocho bits, ¿hasta dónde se propaga el error?**
Asumimos que el tamaño del IV es $n$, y que es multiplo de 8. CFB de 8 bits significa que cada bloque tiene 8 bits.
En CFB, si se produce un error de un bit en la transmision de un caracter del texto cifrado, se afecta la desencripcion del primer bloque, asi como los siguientes $n/8$ bloques.
# Ejercicio 7
Considerando el siguiente cifrado de Bloque:
$E(K,M) = (K \cdot M)(mod 32)$
La idea aca es que queremos encriptar numeros del 0 al 31.
## Parte A
**¿cuál es el tamaño del bloque? ¿cuál es el espacio efectivo de la clave?**
Estamos trabajando en $mod 32$ que es igual a $2^5$, por lo que el tamaño de bloque es el 5.
Siempre hay que usar numeros primos como clave, para no tener problemas del tipo: 0 y 32 se representan como 0 en $mod32$. Al u;sar numeros que sean primos o que no sean divisores de 32 nos evitamos estos problemas.
Por ende, el espacio efectivo de la clave es $\#$ todos los numeros < 32 que son coprimos a 32, que es igual a 16.
## Parte B
**Encriptar el mensaje 24 17 26 25 12 usando modo CBC con vector de inicialización IV = 19 y K = 7.**
- Encuentro los m: $m = 24 17 26 25 12 \implies$
	- $m_0 = 24$
	- $m_1 = 17$
	- $m_2 = 26$
	- $m_3 = 25$
	- $m_4 = 12$
- Encuentro los c:
	- $c_0 = ENC(m_0 \oplus IV) = ENC(24 \oplus 19) = ENC(11) = (11 \times 7)mod32  = 13$
	- $c_1 = ENC(m1 \oplus c_0) = ENC(17 \oplus 13) = ENC(28) = (28 \times 7)mod32 = 4$
	- $c_2 = ENC(m2 \oplus c_1) = ENC(26 \oplus 4) = ENC(30) = (30 \times 7)mod32 = 18$
	- $c_3 = 13$
	- $c_4 = 7$
- Concluimos que c = 13 4 18 13 7

## Parte C
**Desencriptar en modo CBC.**
- Encuentro los m:
	- $m_0 = DEC(c_0) \oplus IV$
	- $m1 = DEC(c_1) \oplus c_0$
	- $m_2 = DEC(c_2) \oplus c_1$
	- $m_3 = DEC(c_3) \oplus c_2$
- En este caso particular, definimos DEC(x) como encontrar $n$ tal que $(n \times 7)mod32 = x$.

# Ejercicio 8
**Una clave débil para DES es una clave K tal que $E_k(E_k(x)) = x \space \forall x$. Esto significa que la clave es debil si al encriptar dos veces un mensaje con la misma clave, es como si no se hubiera encriptado nunca.**
**Analizar por qué una clave formada por todos sus bits en 0, o todos sus bits en 1, es una clave débil de DES. ¿Cuáles serían otras dos claves débiles?**
El algoritmo DES consiste en partir el mensaje en dos mitades, y hacer $\oplus$ entre cada mitad del mensaje y cada mitad de una clave K, repitiendo esto 16 veces.
Si se eligiera como clave 0000 0000 o 1111 1111, el problema es que cada dos ciclos de los 16, el mensaje volveria a ser el original (porque si al mensaje se le hace $\oplus$ con los mismos bits un numero par de veces, el mensaje cifrado termina siendo igual al original).