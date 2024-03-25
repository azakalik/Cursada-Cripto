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