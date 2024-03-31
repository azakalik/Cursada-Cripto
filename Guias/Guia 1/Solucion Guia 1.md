# Ejercicio 1
Dar una definición formal de los algoritmos Gen, Enc y Dec para los siguientes esquemas:
- Cifrado de rotación
- Cifrado de sustitución monoalfabética
- Cifrado de Vigenère

## Cifrado de Rotacion
GEN: elegir un numero del 0 al 26 -> hay 27 posibilidades
ENC: c(i) + k = m(i)
DEC: m(i) -k = c(i)

## Cifrado de sust. monoalfabetica
GEN: elegir una rotacion del alfabeto original -> hay 27! posibilidades


# Ejercicio 2
El uso de dos sistemas de sustitucion simple uno sobre otro no provee mas seguridad que el uso de uno solo porque al usar N sistemas de sustitucion al mismo tiempo, el resultado es el mismo. Esto significa que cada letra esta asociada a otra unica letra, lo unico que cambiaria es como quedaria el alfabeto final.
Lo que se mantiene es que el espacio de claves sigue siendo 26!

# Ejercicio 3
**Descifrar el siguiente criptograma, sabiendo que fue encriptado usando el cifrado de rotación, que se corresponde a un texto en español (27 letras) y los espacios fueron suprimidos ¿Cuál fue la estrategia que utilizaste?**
V K X Y K B K X G K S G W A K Q Q G Y I U Y G Y W A K X K G Q R K S Z K J K Y K K Y I U S Y K M A Ñ X

La letra que mas se repite en el español es la E. La K se repite un monton, asi que la K debe ser la E.
## Ejercicio 4
### Parte a
**Cifrar según Vigenère el mensaje M = UN VINO DE MESA con la clave K = BACO sin usar la tabla, sólo con operaciones modulares.**

La clave K = BACO nos dice que:
- Al primer caracter le hago rot(1)
- Al segundo caracter le hago rot(2)
- Al tercer caracter le hago rot(3)
- Al cuarto caracter le hago rot(15)

Separo el mensaje que nos dan en len(K) ignorando los espacios:
UNVI NODE MESA
Le sumo la cantidad de lugares adecuados:
VOYW ...
### Parte b
**En un sistema de cifra de Vigenère la clave a usar puede ser CERO o bien COMPADRE, ¿cuál de las dos conviene usar y por qué?**
Nos conviene que la clave sea lo mas larga posible, asi hay menos posibilidad de que existan patrones en nuestro texto cifrado (y si hay se repiten menos).
Por ende, nos conviene que sea COMPADRE.
### Parte C
**Mostrar, con un ejemplo, que la composición de dos cifrados Vigenère resulta en otro cifrado Vigenère**
Si los dos cifrados Vigenere tienen la misma longitud. La solucion es trivial. Sin embargo, se complica mas cuando las longitudes de las claves que quiero combinar son distintas. La len de la clave resultado es el minimo comun multiplo de ambas len de los vigenere que quiero combinar.
Para hacer un ejemplo utilizando K1 = ABC y K2 = DE, ya sabemos que la clave resultado tiene len = 6.
Lo que hago es escribir K1 hasta llegar a la longitud requerida
K: ABCABC
Ahora finalmente le aplico K2 para obtener el K final
ABCABC
DEDEDE
Me queda asi:
**EGGFFH**

# Ejercicio 5
**Teniendo en cuenta que la frecuencia (aproximada) de aparición de letras en castellano es la siguiente:**
A  B C D E   F G H I J K L M N Ñ O P Q R S T U V W X Y Z
13 1 4 5 13 1 1  1 7 ? ? 5 3  7  0  9 3 1  7 8 4 4  1 ?   ? 1 ?
**Criptograma 1**
K O Z F V P C Y V C W V Z H M Z L C I O H I F I Z G J C Z T V V X I G J L Z H Y Z L G V M N V L Y Z
**Criptograma 2**
H H M B I W S I P S N N T A W V I T Q W M E A Q V N S P G Q J N W E L X M J D I B Y U G N N R M E U D E M Z I B T M Y M B M W U R B T I Z X N C W Z I U P Z U Q N R M E G J L W R V R O P M R E U M X X X A X D I P U V F E A S M B S A S C E T A E W O Y Y A K U S W E A B S A S C R E C I O M E W T Q O M Y A L M T X R A G E W S Q Q H J D X M V J E A F I R N D U I A N W
**Criptograma 3**
D E R T N Y L A N A O T A A B A D E A X C E E A I D E J L X H R S U A U J U M X E L A A T E C R T R N A Z B I R E S O X

# Ejercicio 6
Se recibe el siguiente criptograma:
JGAZN WINHY LZDYV BBJLC QHTNK UDQXM OXJNO ZMUSP NONYJ MTEJH QHQFO OPUPB CYAÑJ ONCNN QHNMO NDHKU TJMQC MOPNF AOXNT NLOAZ MJDQY MOZCJ RNBAO QTUIE NFAIX TLXJG AZMJA XJVAZ MUDNM YLNLJ MUMUY HVUMH TÑIGD XDQUC LSJPI BCUSF NUGXX GEEXK AEJME SJÑEN ASLHL BAEYJ ROJXA CQTCN MYPUC UNMJW OYNHZ NKUOG AJDUJ XENRY TENJS CNMON TYJNM JYFXF IGJMI BUUSN TFAPN FAFKU ROJNY CTUYN BYSGJ VACAU CGQWA ZMJJH JHSNT PAPXM GNECO GJUTE NCNGJ GEGAJ SPNUL GDMAÑ JDOFD NPUNN PNTGE NMJSN TTOFD
KIOXS SQNNF BATOC XMMNV ÑEZNM EZBOS NTUSQ BUDBT JRBBU YPQZI OQFTB ANIBV MEDDY RUMUP NAULB OMAED HVHNF OCJOS NMJ.

**Si se conoce que ha sido cifrado mediante el algoritmo de Vigenère, se pide:
a. Comprobar la longitud de la clave.**
	La longitud de la clave es la misma que la longitud del texto plano, ya que el cifrado de Vigenere no cambia la misma.
**b. Encontrar la clave del sistema y desencriptar sólo los diez primeros caracteres.**

# Ejercicio 7
**Se cuenta con un texto cifrado que es producto de transposición por columnas (cada “n” columnas se reacomodó el texto original) y un cifrado de rotación.**
**a) ¿Qué estrategia usarías para recuperar el mensaje original?**
	
**b) Si el texto cifrado tiene “m” caracteres, ¿cuántas pruebas requeriría un ataque de fuerza bruta?**
	Primero habria que tener en cuenta todas las combinaciones de columnas, por lo que nos quedaria m!, y a eso hay que hacerle todas las rotaciones, por lo que nos queda 26 por m! (creo)
