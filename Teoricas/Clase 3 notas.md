# Secreto perfecto
1) P(m) = P(m|c) -> la probabilidad de que el mensaje sea X es la misma si conocemos el cifrado o no
2) P(c) = P(c|m) -> la probabilidad de que el cifrado sea X es la misma si conocemos el mensaje o no
3) P(c|m1) = P(c|m2) -> la probabilidad de que el cifrado sea X es la misma para cualquier mensaje
Todas las anteriores son equivalentes. Demostrando una, ya demostramos todas.
Cuando yo supongo que algo es secreto perfecto y quiero demostrarlo, me conviene hacer alguno de esos 3.
Cuando ya se que no hay secreto perfecto y lo quiero demostrar, me conviene hacer un ejemplo de Eavesdropping en la cual la probabilidad no de 0.5.

# Ejemplos
## Ejemplo demostrar que no es secreto perfecto
Definimos:
- GEN = 
- ENC = {ENC(1) = 2, ENC(2) = 1}
Sabemos que:
- P(m0) = P(m1) = 0.5 -> probabilidad del mensaje
- P(k0) = 0.7 -> probabilidad de la clave
- P(k1) = 0.3
Calculamos:
- P(c=1) = P(m0 ^ k0) + P(m1 ^ k1)
		= 0.5 * 0.7 + 0.5 + 0.3
		= 0.5
- P(c=2) = 0.5 por lo anterior
Probamos que:
- P(m) = P(m|c) para todos m, c
- P(m0) = P(m0|1) entonces
- 0.5 = ( P(m0) x P(1|m0) ) / P(1) = 0.5^0.7/0.5 = 0.7
- Nos queda que la probabilidad de que el mensaje sea 0 cuando yo veo un 1 es 0.7
- Por lo tanto, ya no hay secreto perfecto
## Ejemplo demostrar que es secreto perfecto

| b     | k   | c   | b'  | acerto? |
| ----- | --- | --- | --- | ------- |
| 0(m0) | k0  | 1   | 0   | SI      |
| 0(m1) | k1  | 2   | 1   | NO      |
| 1(m0) | k0  | 2   | 1   | SI      |
| 1(m1) | k1  | 1   | 0   | NO      |
- Si el adversario ve 1 -> emite b' = 0
- Para todos los demas casos -> emite b' = 1
- Viendo la tabla, vemos que el atacante acierta siempre que la clave es k0 -> en el 70% de los casos. Por lo tanto, NO hay secreto perfecto.
	- P(b = b') = P(b=0 ^ b' = 0) + P(b = 1 ^ b' = 1) = 0.7