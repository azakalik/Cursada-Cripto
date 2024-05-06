# Ejercicio 1
## Parte A
El espacio de claves es $36! \times 25$. Esto es porque los discos se pueden rotar entre si, y luego tenemos para elegir 25 combinaciones restantes.
## Parte B
El sistema NO admite secreto perfecto. Esto es facilmente demostrable con un experimento Eavesdropping.
- El atacante emite $m_1 = a^{32}$ y $m_2 = b^{32}$
- El atacante obtiene el texto cifrado $c$
- Si el mensaje contiene alguna $b$, entonces el atacante emite $1$. Si el mensaje contiene alguna $a$, entonces el atacante emite $2$.
La explicacion de las decisiones que toma el atacante es la siguiente. Para cifrar un texto, debemos escribir el texto plano en las maderas, y luego elegir alguna de las 25 rotaciones restantes. Por ende si emitimos el mensaje $a^{32}$, entonces es imposible que nuestro mensaje cifrado contenga alguna A.
El atacante gana esta prueba porque puede decidir cual de los dos mensajes emitio con una posibilidad mayor que el 50%.
# Ejercicio 2
## Parte A
El objetivo del protocolo es el mismo que el de DH, que es generar una clave de sesion entre dos partes y poder transmitirla en un medio inseguro.
Para hacer esto:
- A genera la clave de sesion $K$, y le pasa $K^a$ a B -> en este paso ningun atacante podria obtener $K$ a partir de $K^a$, ya que no conoce $a$
- B calcula $K^{ab}$ y se lo pasa a A -> en este paso el atacante no puede obtener ni $k$ ni $a$ ni $b$
- A obtiene $K^b$ a partir de $K^{ab}$ y se lo pasa a B
- B recibe $K^b$ y puede calcular $K$
- Ahora tanto A como B conocen el mismo $K$
La seguridad del protocolo radica en que es computacionalmente imposible que un atacante que este viendo los mensajes pueda conocer $K$ en cualquier momento dado. Esto se debe a que $K$ siempre viaja elevado a una potencia desconocida por el atacante, pero que A y B pueden agregar y quitar a gusto.
## Parte B
La diferencia, es que en DH la clave de sesion termina siendo $K^{ab}$, mientras que en este nuevo esquema la clave de sesion termina siendo $K$ a secas.
Esto implica que en este ultimo caso, A tiene el poder absoluto de decidir cual sera la clave final, mientras que en DH la clave final termina siendo un producto de algo calculado por A y algo calculado por B.
# Ejercicio 3
- La persona ingresa la URL del homebanking en el navegador y hace una consulta HTTP
- Junto a la respuesta, viene el certificado del servidor en donde esta hosteado el homebanking
- Dentro de dicho certificado, se encuentra una cadena de certificados que certifican las distintas autoridades certificantes hasta que se llega a un AC root
- El navegador primero analiza que el certificado de la AC root este en la lista de AC root que hay en el navegador o sistema operativo
- Una vez que verifica el paso anterior, comienza a verificar todos los certificados hasta llegar al certificado del homebanking
- Una vez evaluados todos los certificados, el navegador sabe que realmente esta comunicandose con el homebanking y no le estan haciendo un ataque del tipo Man In The Middle
- NOTA: el navegador tambien debe verificar lo siguiente de cada certificado
	- Que no haya expirado
	- Que no este presente en alguna lista de certificados revocados
# Ejercicio 4
Montamos un ataque MAC-Forge:
- Se genera un $k \in {0,1}$ no conocido por el atacante
- El atacante tiene acceso a $MAC_k(m)$
- El atacante calcula $t = MAC_k(0)$
	- Si $k=0$, entonces $t=0$
	- Si $k=1$, entonces $t=1$
- Ya sabiendo el valor de $k$, el atacante hace lo siguiente
	- Si $k=0$, emite $m=00$ y $t=0$
	- Si $k=1$, emite $m=00$ y $t=1$
- El atacante ganara la prueba en todos los casos
# Ejercicio 5
1. En el modo de encadenamiento para cifrados en bloque OFB -> **La salida $O_j$ de cada bloque de encripcion se genera encriptando la salida del bloque $O_{j-1}$**
2. El "CVV" o Code Verification Value es el codigo de Validacion de 3 o 4 digitos que se usa en las tarjetas de credito para demostrar posesion real del plastico en vta. telefonica. Que mecanismo criptografico seria el mas conveniente para realizar la validacion de dicho codigo en los servidores del banco emisor de la tarjeta y asi verificar que el mismo es valido, pero sin que el codigo este directamente accesible en las bases de datos. -> **Una firma degital basado en una clave publica distribuida de manera autenticada**
3. Que mecanismo criptografico seria mas conveniente utilizar para la distribucion de software en los mercados de apps que se utilizan en los dispositivos moviles? -> **Un esquema de firma digital sobre los binarios**