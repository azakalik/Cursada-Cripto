# Pregunta 1
**Una autoridad certificante puede certificarse a si misma**
VERDADERO. Existen las autoridades certificantes root, que se certifican asi mismas y entre ellas.
# Pregunta 2
**Cualquier criptosistema que cumple ser CCA-Secure garantiza integridad**
FALSO. El cifrado puede ser CCA-Secure, pero esto no impide que un atacante reutilice un mensaje cifrado antiguo. Para prevenir esto hay que incluir MACs.
# Pregunta 3
**Base64 es un algoritmo de encripcion simetrico muy conocido**
FALSO. Base64 NO es un algoritmo de encripcion, ya que no posee clave. Es un sistema de codificacion.
# Pregunta 4
**El algoritmo AES se basa en Feistel-Networks para encriptar simetricamente**
FALSO. AES se basa en una estructura matricial
# Pregunta 5
**Si un criptosistema es MAC-Forge resistant, entonces es CCA**
FALSO
# Pregunta 6
## Punto A
**Explicar que es el salt en las funciones de hashing y por que su uso es importante**

## Punto B
**¿ Cómo se podría utilizar el hash en un sistema de registro de claves de acceso (passwords) en una base de datos?**
Para protegerse ante las consecuencias de un acceso indeseado a una base de datos que guarda claves de la gente, se pueden guardar los hashes en vez de guardar las claves.
De esta forma, un intruso solo podra ver hashes que no le serviran para nada.
# Pregunta 7
**Un sistema de encripcion simetrico**
Es seguro siempre y cuando se use una funcion pseudoaleatoria
# Pregunta 8
**En criptografía asimétrica, en caso de que quiera enviar un mensaje que solo una persona pueda leerlo, lo encripto con mi llave pública**
FALSO. Lo debo encriptar con la llave publica de la persona que quiero que lo lea. De esa forma, el mensaje solo se podra desencriptar con la llave privada de esa persona, por lo que solo el podra leer el mensaje que envie.
# Pregunta 9
**No existe ningun mecanismo para quebrar un criptosistema que tiene seguridad perfecta**
VERDADERO. La idea de la seguridad perfecta es que sea imposible saber (o al menos aproximar) cual es el mensaje que se corresponde a un texto cifrado
# Pregunta 10
**Dado el siguiente protocolo de intercambio/generación de una clave simétrica (k1 || k2), y asumiendo que tanto A como B están en posesión de CertA y CertB**
1. $A \to B: Sig_A(k_1)$
2. $B \to A: Sig_B(k_1\ ||\ k_2)$
Este sistema no funciona. Lo unico que se estan intercambiando son firmas, que corresponden a un hash de las claves. Por lo que B nunca tiene acceso a $k_1$