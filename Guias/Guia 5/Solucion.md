# Ejercicio 1
## Replay
Un ataque de replay es cuando un atacante intercepta una comunicacion entre A y B, y le envia a B un mensaje viejo de A. Este tipo de ataque se puede dar cuando se utiliza el protocolo de Needham-Schroeder (para intercambiar una clave simetrica entre dos entidades).
Este tipo de ataque se puede solucionar incluyendo un NONCE.
## Key Reuse
Este tipo de ataque fuerza a que A y B utilicen siempre la misma clave de sesion para comunicarse. La idea es que el atacante intercepta la conexion entre A y el KDC (en donde A le pide al KDC que genere una clave de sesion para utilizar con B). El atacante le envia a A una clave vieja de sesion, obligando a reutilizar esa en vez de utilizar una nueva.
Esto puede traer problemas, ya que si el atacante conoce la clave vieja de sesion (o tiene el tiempo para averiguarla), entonces podra interceptar toda comunicacion entre A y B.
La solucion que existe para Key Reuse es incluir un NONCE aleatorio en los mensajes. Entonces el receptor de ese NONCE luego enviara el NONCE con una transformacion, y de esa forma ambas partes saben que no se esta reutilizando una clave.
## Masquerading
Un atacante graba mensajes viejos de A hacia B. El atacante le envia estos mensajes viejos a B, y este no tiene forma de saber que no se esta comunicando realmente con A.
Este problema se resuelve utilizando timestamps. Si el mensaje que me llega es mas viejo que 5min entonces lo descarto.
## Man in the Middle
Este tipo de ataque ocurre cuando A quiere obtener la clave publica de B, suponiendo que ambas partes se quieren comunicar utilizando un criptosistema asimetrico.
En este caso, el ataque ocurre de la siguiente forma:
- A le pide a B su clave publica
- Un atacante C intercepta esa comunicacion, borrando el mensaje anterior
- C le pide a B su clave publica
- C le pasa a A la clave publica de B
- C le pide a A su clave publica
- En este punto, A y B piensan que estan comunicandose de manera segura, pero C recibe todos los mensajes de por medio, desencriptandolos con su clave privada y encriptandolos con la clave publica de B
Para solucionar este problema, se necesita O un medio seguro (poco factible) O el uso de certificados como X509
# Ejercicio 2
Si un adversario Z intercepta el primer mensaje, entonces podria efectuar un MITM attack, en donde:
- Z se guarda la clave publica de A
- Z le pide la clave publica a B y se la guarda
- Z le pasa su clave publica a B
- Z le pasa su clave publica a A
- Todos los mensajes que A envie a B, seran interceptados por Z. Z puede desencriptar todos los mensajes de la comunicacion, ya que tanto A como B encriptaran sus mensajes con la clave publica de Z
# Ejercicio 3
El problema con el protocolo es que en el paso 1, A le pasa a B un nonce y una clave de sesion, todo junto a una firma. Sin embargo, ese primer mensaje no viaja encriptado, por lo que un atacante podria obtener la clave de sesion y descifrar todos los mensajes de la comunicacion entre A y B.
Para solucionar el problema, existen estas opciones:
- Pasarse a un esquema de criptografia asimetrica, en donde A y B puedan generar una clave de sesion por un medio inseguro sin que un atacante pueda interceptarla
- Seguir en el esquema de criptografia simetrica, pero encontrar alguna forma mejor para que A y B se compartan la clave de sesion sin que un atacante pueda interceptarla. Por ejemplo: hacer uso de un KDC.
# Ejercicio 4
A NO debe permitir que los nonce sean iguales. De lo contrario, el atacante podria darse cuenta si N1 = N2, ya que viajan en texto plano. En este caso, $(N2)_{ks} = (N1)_{ks}$, entonces el atacante podria interceptar el cuarto mensaje de B hacia A, y enviarle $(N2)_{ks}$.
# Ejercicio 5
El protocolo original Needham-Schroeder tiene una vulnerabilidad a los ataques de replay, ya que las comunicaciones entre A y B no tienen un NONCE.
En el caso de la consigna, podemos ver que:
- En el paso 2, Bob genera un NONCE y se lo pasa a Alice
- En el paso 3, Alice genera un NONCE y se lo pasa a Trent
**no lo entendi muy bien**
# Ejercicio 6
Intercambio de claves Diffie-Hellman:
- A genera G, q, g y se lo pasa a B por un medio inseguro
- A calcula un X aleatorio entre 0 y q-1
- B calcula un Y aleatorio entre 0 y q-1
- A calcula $g^X$ y se lo pasa a B
- B calcula $g^Y$ y se lo pasa a A
- A y B calculan $g^{XY}$, que pasara a ser la clave de sesion entre los dos
Si hubiera 3 participantes:
- Se genera G, q, g
- A calcula un X aleatorio entre 0 y q-1
- B calcula un Y aleatorio entre 0 y q-1
- C calcula un Z aleatorio entre 0 y q-1
- A le pasa $g^x$ a B -> B calcula $g^{xy}$ y se lo pasa a C -> C calcula $g^{xyz}$
- B le pasa $g^y$ a C -> C calcula $g^{yz}$ y se lo pasa a A -> A calcula $g^{xyz}$
- C le pasa $g^z$ a A -> A calcula $g^{xz}$ y se lo pasa a B -> B calcula $g^{xyz}$
- Finalmente, todos tienen la clave de sesion
# Ejercicio 7
## Punto A
Supongamos que las firmas no estuvieran:
- A le manda $g^x$ a B
- Un atacante C intercepta el mensaje de A hacia B, y cambia $g^x$ por $g^z$, suponiendo que $z$ es la SK de C.
- Cuando A reciba el mensaje de B, se puede dar cuenta facilmente de que el $g^x$ que envio era incorrecto
En conclusion, las firmas verifican que nadie haya cambiado los valores de $g^x$ y $g^y$ durante la trasmision
## Punto B
# Ejercicio 8
## Punto A
- Es un ataque de **message integrity**
- Bob puede detectar este problema, dado que SIGN(x) no coincidira con el mensaje que recibio BOB (x').
- Esto se puede solucionar tanto con firma como con MAC
## Punto B
- Es un ataque de **replay**
- Para evitar este problema, no se puede utilizar ni Firmas digitales ni codigos MAC
## Punto C
- Este podira ser un ataque de **cheating**
- Para dirimir la cuestion, Bob puede verificar si el mensaje pasa VRFY con la clave publica de Alice o con la de Oscar
- El problema solo se puede resolver con firma digital, ya que si fuera con MAC entonces Alice y Oscar tendrian que revelar su clave privada
## Punto D
- Alice podria pedir que se compruebe si la firma pasa la funcion VRFY con el mensaje X y su clave publica. Si es el caso, entonces ella es culpable
# Ejercicio 9
