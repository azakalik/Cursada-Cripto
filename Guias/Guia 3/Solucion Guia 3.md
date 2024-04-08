# Ejercicio 1
Definimos que un MAC posee seguridad si y solo si pasa la prueba de MAC-Forge.
1. No posee seguridad, porque yo puedo plantear un mensaje que sean todos 0s, y de esa forma obtener G(k). Dado que G(k) no cambia, se pierde la seguridad.
2. No posee seguridad. Si yo defino dos mensajes cuyos primeros k bits sean iguales, entonces tendran el mismo MAC.
3. No posee seguridad. Dos mensajes con la misma longitud van a tener el mismo MAC.
Concluimos que ninguno tenia seguridad, porque era trivial encontrar dos mensajes con el mismo MAC.

# Ejercicio 2
Defino el mensaje $m$ como 128 bits en 0 concatenado con 128 bits en 1.
Defino el mensaje $m'$ como 128 bits en 1 concatenado con 128 bits en 0.
Podemos ver que ambos mensajes son distintos, pero tienen el mismo MAC.
# Ejercicio 3
## Parte A
La funcion no es valida para criptografia. A continuacion analizamos los 3 niveles.
1. No es **resistente a colisiones**, porque $x_1 = 00$ y $x_2 = 11$ ambos tienen el mismo MAC (32 ceros)
2. No es **resistente a segundas preimagenes**, porque dado cualquier $x$, podemos encontrar otro $x'$ que tenga el mismo MAC. Si $x'$ tendra un numero par de caracteres si y solo si $x$ tiene un numero par de caracteres.
3. No es **resistente a preimagen**, porque dado un MAC $y$, podemos obtener un $x'$ que tenga el mismo MAC. Si $y$ es todos 0, entonces $x'$ tendra un numero par de caracteres. Si $y$ es todos 1, entonces $x'$ tendra un numero impar de caracteres.
## Parte B
Dado que el espacio de claves MAC es 2 (todos 0 o todos 1), entonces dos entradas $x_1$ y $x_2$ tienen $50\%$ de chances de colisionar.
# Ejercicio 4
Teorico, hacer mas adelante
# Ejercicio 5
## Parte A
```
spackjarrow@Zenbook-14:~$ cat text1
hoy es el primer lunes de abril
spackjarrow@Zenbook-14:~$ openssl dgst -md5 text1
MD5(text1)= 4893481cf3c2fe18773dabb1bd990050
```
## Parte B
```
spackjarrow@Zenbook-14:~$ cat text1
hoy es el primer lunes de abril
spackjarrow@Zenbook-14:~$ openssl dgst -sha1 text1
SHA1(text1)= fcebd0e92f4e5330390ef34c3010ab4908ae81fe
```
### Parte C
La diferencia principal que observo es que el SHA1 es mas largo que el MD5. Posiblemente el riesgo de colision sea menor en SHA1.
# Ejercicio 6
Este ejercicio se resuelve haciendo bruteforcing. Por ejemplo:
```
spackjarrow@Zenbook-14:~$ echo "1 uno" | openssl dgst -sha1
SHA1(stdin)= 86a76e0399c99c1d5b8c8751b7d5240b24b271f3
```