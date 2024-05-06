# Ejercicio 1
## Parte A
El mensaje NO tiene secreto perfecto en este espacio de mensajes.
Hagamos un ataque Eavesdropping:
- Se genera un $k \in 2, 3$ que el atacante no conoce
- El atacante emite $m_1 = {aaaaaa}$ y $m_2 = bbbbbb$
- El atacante obtiene el texto cifrado $c$
- El atacante toma la siguiente decision
	- Si el texto cifrado es $aaaaaa$, el atacante emite $1$
	- Si el texto cifrado es $bbbbbb$, el atacante emite $2$
- En conclusion, el atacante acierta el 100% de las veces
## Parte B
Aca tampoco hay secreto perfecto.
Primero notemos los siguientes casos:
- $ENC_{k=2}(abcdef) = acebdf$
- $ENC_{k=3}(abcdef) = adbecf$
- $ENC_{k=2}(fedcba) = fdbeca$
- $ENC_{k=3}(fedcba) = fcebda$

Hacemos un ataque Eavesdropping:
- Se genera un $k \in {2, 3}$, que el atacante desconoce
- El atacante emite $m_1 = {abcdef}$ y $m_2 = fedcba$
- El atacante obtiene el texto cifrado $c$ y toma estas decisiones
	- Si $c={acebdf}$ o $c=adbecf$, entonces emite $1$
	- Si $c = fdbeca$ o $c=fcebda$, entonces emite $2$
- El atacante acierta el 100% de las veces
# Ejercicio 2
## Protocolo 1
**Pasos que efectua B con el mensaje recibido:**
Una vez que B recibe $Enc_{k1}(x\ ||\ H(k_2\ ||\ x))$, hace los siguientes pasos:
- Obtiene $x\ ||\ H(k_2\ ||\ x)$ haciendo $Dec_{k1}(Enc_{k1}(x\ ||\ H(k_2\ ||\ x)))$
- Calcula $H(k_2\ ||\ x)$ y se fija que sea igual al obtenido
- Obtiene el mensaje $x$
**Aspectos preservados:**
- **Confidencialidad**: SI. Porque el mensaje viaja encriptado con un algoritmo de encripcion simetrico seguro
- **Integridad**: SI. Porque el mensaje encriptado adentro contiene un Hash del mensaje original, por lo que es facil verificar si se ha alterado algun bit
- **No repudio**: NO. No hay manera de identificar si un mensaje ha sido escrito por A o por B
- **Seguridad ante ataque de replay**: NO. No hay manera de verificar a A o B le estan enviando mensajes viejos
## Protocolo 2
**Pasos que efectua B con el mensaje recibido**
Una vez que B recibe $Enc_{k}(x\ ||\ Sign_{kprA}(H(x)))$, hace los siguientes pasos:
- Obtiene $x\ ||\ Sign_{kprA}(H(x))$ a partir de $Dec_k(Enc_{k}(x\ ||\ Sign_{kprA}(H(x))))$
- Calcula $H(x)$ y confirma que coincide con el que le llego, usando la clave publica de A
- Se queda con el mensaje $x$
**Aspectos preservados:**
- **Confidencialidad**: SI.
- **Integridad**: SI.
- **No repudio**: SI. A no tiene forma de negar que envio un mensaje que esta firmado con su clave privada.
- **Seguridad ante ataque de replay**: NO. No hay forma de saber si un atacante esta enviando mensajes antiguos.
# Ejercicio 3
## Parte A
Para efectuar la desencripcion:
- El receptor comienza descifrando $c_1$. $m_1 = IV_1 \oplus F_k()$
- $c_1 = IV_2 \oplus F_k(m_1 \oplus IV_1))$, entonces $m_1 = F_k^{-1}(c_1 \oplus IV_2) \oplus IV_1$
- $c_i = m_{i-1} \oplus F_k(m_i \oplus c_{i-1}))$, entonces $m_i = F_k^{-1}(c_i \oplus m_{i-1}) \oplus c_{i-1}$
- Podemos notar que para obtener $m_i$, necesitamos $m_{i-1}$ y $c_{i-1}$ en todos los casos
## Parte B
Si un bit de $c_j$ se altera durante la transmision entonces todos los $c_k$ con $k >= j$ se descifraran mal
# Ejercicio 4
## PKI
- Significa Public Key Infrastructure
- Se encarga de cosas como:
	- Distribuir la clave publica de distintos hosts de internet
	- Ver que las claves publicas no esten en una lista de revocadas
	- Autentificar las claves publicas con firmas (de acuerdo con el estandar X509)
	- Verificar certificados
		- Viendo que no esten expirados
		- Viendo que el CN coincida con el esperado
## KDC
- Significa Key Distribution Center
- Se encarga de generar claves de sesion entre dos hosts de una red
- La idea general es que comparte una clave de sesion distinta con cada miembro de la red, y luego genera una clave de sesion entre los hosts A y B cuando alguno de estos asi lo solicita
## Similitudes
Todos los algoritmos de encripcion requieren que exista una o mas claves, de lo contrario cualquier tercero podria ver los mensajes en texto plano.
Ambos se encargan de que dos hosts se pongan de acuerdo en una o mas claves para utilizar, ya sea un algoritmo simetrico o asimetrico.
## Diferencias
PKI se encarga de distribuir de manera segura las claves publicas de cada host, y poder verificar que no sea alguien haciendose pasar por ese host.
KDC se encarga de generar una nueva clave de sesion unica para cada nueva conexion entre dos hosts.
En conclusion, KDC genera claves pero PKI no.

# Ejercicio 5
1. El siguiente protocolo ... -> **Es un protocolo de intercambio de claves**
2. Un criptosistema ... -> **Es inmune a CPA si $c=<r, F_k(r) \oplus m>$
3. La construccion CBC-MAC es una construccion segura para MAC -> **Si los mensajes son de longitud fija y el vector IV es aleatorio**