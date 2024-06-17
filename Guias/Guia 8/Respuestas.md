# Ejercicio 1
## Parte A
- **Informacion de autenticacion (A):** la huella de la persona (algo que soy)
- **Informacion complementaria (C):** (AFIS) almacenar todas las huellas dactilares recolectadas en formato de template
- **Funciones de complementacion (F):** ndea
- **Funcion de autenticacion (L):** (AFIS) compara las huellas enviadas desde las estaciones locales o remotas contra las almacenadas en el sistema
- **Funciones de seleccion (S):** La misma que C. Si quiero actualizar una huella, la borro y la vuelvo a poner.
## Parte B
- Clonacion de template
- Templates similares
## Parte C
- Scanner sucio
- Dedo lastimado
## Parte D
- Podria ocurrir, dado que el sistema es probabilistico y no de matching exacto como en el caso de las claves. Existen muchos casos de hermanos que pueden desbloquear los celulares del otro porque tienen huellas parecidas.
# Ejercicio 2
La formula a recordar es $P = {{T \times G} \over N}$ con:
- $T$: tiempo dedicado a las pruebas
- $G$: numero de pruebas por segundo
- $N$: tamaño del espacio de claves

## Parte A
El espacio de claves es $8^{10}$
## Parte B
El espacio de claves es $36^{10}$
## Parte C
Si se le agregan 10 bits de salt, entonces para adivinar una unica clave las probabilidades son las mismas
$36^{10} \times 2^{10}$