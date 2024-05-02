# Primeros Cifrados
## Rotacion
![](Pasted%20image%2020240430184010.png)
- No es muy seguro porque se puede hacer brute-forcing con 27 intentos
## De sustitucion
- Reemplaza un simbolo por otro, segun una tabla predefinida
- Desventaja: las propiedades estadisticas del lenguaje no se ven afectadas
## Vigenere
- Es una sustitucion polialfabetica, en donde hay n alfabetos.
- Es basicamente ROT con distintas claves
![](Pasted%20image%2020240430184206.png)
- Ataque:
	- Determinar longitud del bloque
	- Analizar la clave de cada bloque por separado
	- Van a aparecer n-gramas repetidos
	- La longitud de la clave es MCD de la distancia entre anagramas
![](Pasted%20image%2020240430184346.png)
# Tipos de Ataques
## Ataque de Texto Cifrado
- El adversario solo dispone de mensajes cifrados y quiere obtener los mensajes
## Ataque de Texto Plano Conocido (indistinguishiability)
- El adversario conoce pares mensaje - texto cifrado y busca obtener un mensaje a partir de un texto cifrado
## Ataque de Texto Plano Escogido
- El adversario puede cifrar cualquier mensaje que quiera
## Ataque de Texto Cifrado Escogido
- El adversario puede obtener el descifrado de los textos cifrados que quiera
# Secreto perfecto
- Un criptosistema es seguro si ningun adversario puede computar cualquier funcion del texto plano a partir del mensaje cifrado que posee
- Un criptosistema posee la caracteristica de secreto perfecto si la probabilidad de que un mensaje cifrado $C$ sea un texto plano $P$ es igual a $1 \over n$, con $n$ siendo el espacio de textos cifrados
- Como el secreto perfecto es muy impractico, nos tenemos que conformar con que sea **computacionalmente muy dificil** de descifrar nuestro mensaje
# Criptosistema Simetrico
- Terna de algoritmos: ENC, DEC, GEN tal que DEC(ENC(x)) = x
## One Time Pad
- Consiste en aplicar XOR bit a bit a un mensaje, con una clave de la misma longitud del mensaje
- Esta demostrado que todos los criptosistemas con propiedad de secreto perfecto son un isomorfismo al OTP
- La desventaja es que se necesita una clave del largo del mensaje, y esta no se puede usar para mensajes distintos (porque sino $C_1 \oplus C_2 = m_1 \oplus m_2$)
# Criptosistemas de flujo
- Intercambian la clave del OTP (de longitud igual al mensaje original), con la salida de una funcion pseudoaleatoria (de longitud menor al mensaje a enviar)
- Teorema: si G(s) es un generador pseudoaleatorio, el criptosistema es indistinguible ante un atacante
- IMPORTANTE: los criptosistemas de flujo NO pueden reutilizar la misma clave para distintos mensajes (porque sino $C_1 \oplus C_2 = m_1 \oplus m_2$)
## Generadores pseudoaleatorios
- No esta demostrado que exista algo realmente pseudoaleatorio
- Son algoritmos deterministicos
- Expanden una semilla (seed) a una longitud deseada
## Reutilizacion de la clave con IV
### Modo no sincronizado
- Se calcula un IV distinto para cada mensaje a enviar y se hace XOR con la salida del generador pseudoaleatorio
### Modo sincronizado
- El generador pseudoaleatorio genera una salida muy larga, y se va usando de a pedacitos entre los distintos mensajes
## Pruebas de Seguridad
- Existen para medir la seguridad de un criptosistema
### Prueba de indistinguibilidad (o Eavesdropping, EAV)
- El atacante emite dos mensajes: $m_1$ y $m_2$
- Se genera una clave $k$
- Se cifra uno de los mensajes con la clave $k$, y el atacante lo recibe ($c$)
- El atacante tiene que decidir si ese $c$ corresponde a $m_1$ o a $m_2$
- El atacante gana si logra decidir con probabilidad != a 0.5
### Eavesdropping Multiple (MUL)
- El atacante emite dos listas de mensajes
- Se genera una clave $k$
- Se cifra una de las listas de mensajes
- El atacante recibe una de las listas cifradas, y tiene que averiguar cual era con probabilidad != 0.5 para ganar
- Para pasar la prueba tiene que ser no deterministico
### Texto plano escogido (CPA)
- El atacante puede encriptar todos los mensajes que quiera
- El atacante tiene que emitir dos mensajes
- Se genera una clave, se devuelve el mensaje cifrado al atacante
- El atacante tiene que adivinar a cual de los mensajes corresponde ese texto cifrado
- Para pasar la prueba, tiene que se no deterministico
- Si un criptosistema es CPA-Secure, tambien lo es para la prueba CPA con multiples mensajes
# Estado de un criptosistema
Puede ser
- Seguro
- Debilitado (existen adversarios con probabilidades no despreciables de exito, pero requiere de un gran esfuerzo computacional)
- Quebrado
# Primitivas de cifrado en bloque
- Definidos para mensajes de tamaño fijo
- Son primitivas y no criptosistemas. Forman criptosistemas al combinarse en diferentes modos
## Extension
- Si el mensaje a cifrar es mas largo que el tamano de bloque, se lo divide en bloques y se extiende el ultimo bloque
### Simple Pad
- Se rellena con 0s
- Problema cuando el mensaje termina en 0
- Sirve solo para casos donde se conoce la longitud del mensaje (como SSH)
### Des Pad
- Se rellena con un 1 y despues todos 0s
- No es necesario saber la longitud del mensaje a priori
- Problema cuando el mensaje tiene la longitud maxima, se genera un bloque entero de padding

## Encadenamiento
### ECB (electronic codebook)
- Se trata a cada bloque como un mensaje distinto, reutilizando para todos la misma clave
- Cifra cada bloque con la clave nada mas
- NO usar bajo ningun concepto, rompe la regla de no repetir la clave
### CBC (Cipher block chaining)
- Se genera un IV y una clave $k$
- Para obtener $C_0$, se hace XOR de $m_0$ con el $IV$, y se lo encripta con la clave $k$
- Para obtener $C_n$, se hace XOR de $m_n$ con $C_{n-1}$, y se lo encripta con la clave $k$
- Problema: el cifrado es secuencial, ya que para cifrar cada $C_n$ necesito $C_{n-1}$
- El descifrado es paralelizable una vez que ya me llego todo el texto cifrado
- Si se cifra mal un bloque, el error NO se propaga a todos los bloques
### CFB (Cipher feedback)
- Se usaba antes cuando la capacidad computacional era muy baja, ahora ya no
- No usa funcion DEC
- Para encriptar un mensaje, se cifra la clave $k \oplus IV$ para el mensaje 1, y luego se sigue cifrando eso mismo.
- El texto nunca se cifra, y solo se le aplica un XOR con la clave generada en cada paso
### OFB (Output feedback)
- Permite calcular los bits de la transformacion por adelantado
- Para hacer la clave de un bloque nuevo, se cifra la clave del bloque anterior
## Counter
- Permite acceso random
- Se genera un NONCE y un counter al principio
- Para cifrar cada bloque, se usa la funcion de cifrado con la clave $k$ de NONCE+counter
### Data Encryption Standard (DES)
- Desarrollada por IBM
- Se parte el mensaje en dos mitades
- Las partes se van transformando con una clave e intercambiando de lugar
- Se quebro en 1992
### 3-DES
- Consiste en hacer DES aplicando $ENC_{K_1}(DEC_{K_2}(ENC_{K_3}(m)))$
- La seguridad que brinda es de 112 bits y NO de 168
- 3 veces mas lenta que DES
### AES
- Reemplazo a DES
- Bloques de 128 bits
- Claves de 128, 192 o 256 bits
- Recomendado en al actualidad