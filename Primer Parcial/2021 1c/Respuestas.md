# Pregunta 1
**En que esta basado el cifrado simetrico DES? Explicar la idea general, que es lo que se busca en el algoritmo. Si trabajasen en un banco y alguien propone utilizar este protocolo, que aconsejarian?**
El cifrado simetrico DES esta basado en redes Feistel. La idea general es que se parte el texto plano en dos mitades, y la clave en varias partes. Luego, con un proceso iterativo se van transformando y rotando las mitades de lugar, hasta llegar a las 16 iteraciones. La entrada de este algoritmo es de 64 bits y la clave tambien, aunque tiene solo 56 bits efectivos.
Originalmente, DES tenia claves de 64 bits, pero esa seguridad se rompio en 1992, en donde la seguridad llego a niveles que hoy en dia se podrian romper facilmente con brute forcing (2^43 intentos). Es por eso que DES hoy en dia se considera quebrado.
Sin embargo, existe como alternativa 3-DES, que posee claves de 112 bits, por lo que al dia de hoy sigue siendo segura. Si fuese empleado de ese banco, diria que es mucha mejor idea utilizar 3-DES antes que DES.
Algo a tener en cuenta es que 3-DES tarda 3 veces mas en ejecutar que DES, el cual no es especialmente rapido de ejecutar en un principio.
# Pregunta 2
Supongase que se desea encriptar un mensaje con $M \in \{0, 1, 2\}$ utilizando una clave simetrica compartida $K \in \{0, 1, 2\}$. Los datos se representan con dos bits: $\{00, 01, 11\}$ y las claves tambien.
## Punto A
**Explicar si este esquema da las garantias de un One Time Pad**
Veamos los posibles valores de C, suponiendo que los valores de $M$ y $K$ son una distribucion uniforme

|        | m=$00$ | m=$01$ | m=$10$ |
| ------ | ------ | ------ | ------ |
| k=$00$ | c=$11$ | c=$10$ | c=$01$ |
| k=$01$ | c=$10$ | c=$11$ | c=$00$ |
| k=$10$ | c=$01$ | c=$00$ | c=$11$ |
Podemos ver que:
- c=$11$ tiene $1/3$ de probabilidades de ocurrir
- c=$00$ tiene $2/9$ de probabilidades de ocurrir
- c=$01$ tiene $2/9$ de probabilidades de ocurrir
- c=$10$ tiene $2/9$ de probabilidades de ocurrir
Podemos montar el siguiente ataque:
- El atacante $A$ emite $m_1 = 00$ y $m_2 = 01$
- El atacante usa esta logica:
	- Si el mensaje cifrado es $00$, emito $2$
	- De lo contrario, emito $1$.
- Podemos ver en la tabla que el atacante acierta 66% de las veces, por lo que no hay secreto perfecto

| $m$ | $k$ | $c$ | $m'$ | Acerto? |
| --- | --- | --- | ---- | ------- |
| 00  | 00  | 11  | 1    | SI      |
| 00  | 01  | 10  | 1    | SI      |
| 00  | 10  | 01  | 1    | SI      |
| 01  | 00  | 10  | 1    | NO      |
| 01  | 01  | 11  | 1    | NO      |
| 01  | 10  | 00  | 2    | SI      |

## Punto B
**Ofrecer una alternativa al esquema anterior que ofrezca las garantias de seguridad de One Time Pad manteniendo los mismos M y K**
Defino mi funcion de encripcion de la siguiente forma:
$ENC_k(m) = F_k(m) \oplus m$, con $F_k$ funcion pseudoaleatoria
# Pregunta 3
**Plantear un algoritmo de encripcion simple basado en un algoritmo de sustitucion polialfabetica. Como y bajo que condiciones puedo usarlo para implementar con el un esquema de OTP?**
Puedo definir un cifrado Vigenere modificado, tal que la clave tenga la misma longitud que el mensaje original. Con esta condicion, puedo utilizarlo para implementar un OTP

# Pregunta 4
**Lo importante al encriptar un mensaje con un MAC es que este demostrado que para esta primitiva es computacionalmente complejo encontrar la preimagen, eventuales colisiones y segundas preimagenes**
FALSO. Porque NO se encripta un mensaje con un MAC. En cambio, el MAC sirve para etiquetar un mensaje.
# Pregunta 5
**La ventaja del modo de encripcion en CBC es que es paralelizable**
FALSO. Esto se debe a que en CBC, la encripcion se da de la siguiente forma:
- Se define un $IV$ aleatorio
- Se parte al mensaje m en bloques de igual longitud de la siguiente forma: $m = m_1 m_2 m_3 ... m_n$
- $c_1 = ENC_k(IV \oplus m_1)$
- $c_n = ENC_K(c_{n-1} \oplus m_n)$
- El mensaje cifrado queda $c = c_1 c_2 c_3 ... c_n$
# Pregunta 6
**Un experto en seguridad afirma que un sistema de Encripcion basada en una primitiva segura $E_k$ es CPA-Secure. El emisor, al enviar un mensaje m, obtiene un numero al azar r y envia $(r, e_k(r) \oplus m)$**
VERDADERO. Es CPA-Secure porque no es deterministica.
Montamos un ataque CPA:
- El atacante obtiene acceso a $ENC_k(m)$
- El atacante emite $m_0$ y $m_1$
- El atacante obtiene $c$
- El atacante no tiene forma de saber a que mensaje se corresponde $c$ por mas que haya usado el oraculo de encripcion, ya que estamos hablando de  un cifrado no deterministico
# Pregunta 7
**Una firma digital basada en un algoritmo simetrico requiere utilizar primitivas de Hash**
FALSO. Esto se debe a que las firmas digitales sirven para verificar la autenticidad de las claves publcas en un esquema de encripcion asimetrico, por lo que no se podrian basar nunca en un algoritmo simetrico
# Pregunta 8
**El siguiente protocolo permite el intercambio de claves de sesion de largo plazo mediante dos entidades A y B. El protocolo arranca una vez que A y B generaron una clave K mediante un algoritmo de intercambio seguro de claves.**
![](Pasted%20image%2020240502174953.png)
**donde K es una clave simetrica generada por un protocolo de intercambio de clave como DH, sk_a y sk_b son claves de sesion de largo plazo para comunicarse con A y B respectivamente,y n_a y n_b son nonces. A* y B* son numeros que permiten verificar la integridad de las claves de sesion de largo plazo.**
## Punto A
**Cual es el proposito de los nonces en este protocolo?**
El proposito de los nonces es evitar ataques de replay
## Punto B
**Mediante que primitiva criptografica podrian implementarse la generacion de A* y B*?**
Mediante el uso de firmas digitales
# Pregunta 9
**Plantear un experimento $Exp_{CCA}(A, n)$ y demostrar por que en un criptosistema basado en una funcion pseudoaleatoria $ENC_k = F_k(r) \oplus m$ el atacante no tiene exito**
Planteamos el experimento:
- El atacante recibe un oraculo para acceder a $ENC_k$ y a $DEC_k$
- El atacante pide la encripcion del mensaje $m_0 = 0^n$ y de $m_1 = 1^n$ -> obtiene $c$
- El atacante pide la desencripcion de $c$ y calcula $c \oplus m_x$, con $x$ siendo el que correspondia a $c$
- El atacante ahora conoce $F_k(r)$
- El atacante emite los mensajes
# Pregunta 10
**El algoritmo de El Gamal permite la generacion entre Alice y Bob de una clave de sesion por un canal inseguro**
