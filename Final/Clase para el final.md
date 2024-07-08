# Segun tipo de empresa
## Para empresa chica
Yo pacto con el equipo de pentest
- Que partes testear -> porque es costoso y lleva tiempo
- Si entras a tal DB, no toques nada
## Para empresa grande
### Blue team
- se encarga de la **defensa**
	- respuesta a incidentes (que hacemos si nos hackean la aplicacion)
	- escaneo de vulnerabilidades (y ver que se arreglen)
- es propio de la empresa -> es caro tenerlo, tiene que valer la pena
- se encargan de cosas mas puntuales, como testear determinada API o sistema
### Red team
- se encargan de testear al blue team, **ataque**
- buscan evaluar cosas mas globales que el blue team, como las politicas de la empresa y interaccion entre sistemas
- se encargan tambien de cosas fisicas, como entrar a la empresa o hacer phishing a los empleados
### Purple team
- Para ahorrar costos, es tanto **blue** como **red**
- Estan capacitados tanto para **defensa** como **ataque**
## Green team
- Se encargan de la parte legal
- Yo hackeo la DB de mi cliente, pero esa DB tenia datos privados. Estoy rompiendo leyes de confidencialidad
- Hay leyes de proteccion de datos personales. Si hay un leak, entonces la empresa tiene que pagar multa
# Pivoting
- Si un atacante compromete una PC, puede intentar comprometer a otra con mas privilegios -> privilege escalation

# Vulnerabilidades web
## XSS
- Inyectamos codigo dentro de un input, para ejecutar codigo dentro de la compu de otro
## SQLi
- Inyectamos codigo SQL
## CSRF
- Es cuando yo quiero que el usuario haga una accion no intencionada
- Dos ventanas activas
- Estamos logueados en una pagina (ejemplo: homebanking)
- Una pagina maliciosa nos pone un hipervinculo que se carga automaticamente (como una imagen de 1 pixel por ejemplo)
- Este hipervinculo es un URL malicioso que hace que se ejecute una accion en nuestra pagina de homebanking (donde teniamos una sesion activa).
- La solucion suele ser que no se pueda acceder directamente a ese URL malicioso, por ejemplo pidiendo que antes de entrar a "transferencias" se acceda al menu "mi cuenta"
## MITM / Masquerading
- Masquerading es MITM con suplantacion de identidad
## Replay attack
- Por ejemplo, evitar que se ejecute la misma transferencia 5 veces
## Broken authentication
- Tengo user y password en mi login. Si puedo hacer XSS para bypassearlo, entonces lo tengo broken
- Si me deja hacer bruteforcing (no tengo un max-tries) esta broken
- User enumeration: si yo pongo usuario: pepito y clave: xxx y me contesta "usuario pepito no existe", entonces estoy pudiendo ver que usuarios hay en el sistema. Esto esta MAL. Una vez que tuviera la lista de usuarios, les puedo hacer bruteforce a cada usuario.
## Broken access control
- El usuario de ID 32 puede acceder al endpoint /user/id=32
- No deberia poder pasar que ese usuario pueda acceder a /user/id=33
- Esto no tiene que ver con autenticacion, sino con control de accesos, porque yo no me estoy haciendo pasar por otra persona
# Setup de testeo para App Movil
- La aplicacion muy probablemente le vaya a pegar a una API
- Primero me fijo cual es la direccion de la API
	- la consigo analizando los paquetes de la red con Wireshark (en la misma wifi que el celular), pero van a estar encriptados
	- tambien en vez de un dispositivo movil podriamos usar un emulador, y desde wireshark ver todos los paquetes
	- si la conexion es HTTPS, los paquetes van a estar cifrados, entonces tal vez no siempre tiene sentido usar wireshark
	- otra forma es directamente analizar el APK de la aplicacion (por ejemplo tal vez descompilando el codigo java a bytecode)
- Tambien podemos correr la aplicacion en un entorno no seguro (como en un android rooteado)
	
# Setup de testeo para API
- No hay tanto setup como en app movil
- Empezamos a interactuar directamente con la API, con Postman o similar
- Una vez que tengo la direccion (IP) de la API, tengo que ver que endpoints hay
- Api discovery: me empiezo a fijar los endpoints mas normales, como /api, /api/register, etc. Hay herramientas que me permite automatizar esto, como Dirsearch y Gobuster, que tienen una lista de endpoints comunes
# Notas random
- Es util tener una red distinta por cada piso en un edificio de oficinas
- Con quien yo trabajo es muy importante. Si mi compu es altamente segura pero la de mi compañero no, entonces lo pueden targetear a el para atacarme a mi
- Siempre confiamos en otro eslabon. Por ejemplo, Gentoo linux es muy conocido porque uno compila su propio SO con sus propios drivers. Sin embargo, uno estaria confiando en el compilador en ese caso. La conclusion es que es imposible hacer todo solo sin confiar en herramientas externas
- TLS 1.0 es una version vieja y es vulnerable
- Se puede usar un timestamp para evitar ataques de replay
# Errores comunes en el parcial
## Wireshark
- Decir veo el wireshark para una pagina con HTTPS (aunque esta bien para HTTP o HTTPS con TLSv1 que ya esta roto)
- Decir hago MITM con wireshark -> puedo recibir datos pero no enviarlos
## DOS
- No esta bueno testear los DOS porque le tiras abajo la pagina al cliente, pero si puede haber indicios
- Esta mal decir "envio muchos requests hasta que me devuelva error 500", porque tal vez el sistema se levanta rapido
## Demasiada generosidad
- Le pedimos al cliente que nos haga un deploy especial para testear
- No siempre podemos asumir que tenemos una cuenta cargada en la plataforma
- El cliente no nos va a asignar recursos especiales para que nosotros hagamos nuestro trabajo
## Ataques poco viables
- Ejemplo 1: Leaks de informacion en una app mobile hacia el cache
- Ejemplo 2: me cuelgo en el wifi de la victima
## Mal entendimiento de los ataques
- Decir un ataque pero sin explicar en detalle como hacerlo
- Por ejemplo "hago un replay attack". A quien se lo envio? como? por que?

# Ejercicio de final
## Broken authentication
**Hipotesis**: la autenticacion no esta implementada de manera segura, permitiendo que se haga bruteforcing en el login.
**Prueba**: intentar hacer bruteforcing en el login utilizando un diccionario de claves, que comience con las claves mas faciles de adivinar. Inspeccionar la pantalla de registracion para ver si la misma permite poner una clave muy facil (como 1234). Ver si la aplicacion nos permite establecer claves muy faciles.
## Broken access control
**Hipotesis**: la aplicacion permite autenticarse para acceder a los datos de usuario. Es posible que un usuario pueda acceder a los datos de otro usuario.
**Prueba**: loguearse con el usuario de ID 1. Suponemos que se puede agarrar la data del usuario haciendo GET a /profile/info?id=n. Entonces intentemos hacer GET a /profile/info?id=2 y ver que pasa.
## Sensitive data exposure
**Hipotesis**: las tarjetas de credito de los clientes no estan correctamente protegidas
**Prueba**: verificar en base de datos si los datos confidenciales de los clientes se guardan de manera encriptada o no. Verificar que las claves se guarden hasheadas y no en texto plano.
## Credenciales harcodeadas
**Hipotesis**: para utilizar DummyPay se requiere la utilizacion de una API credential. Esta se encuentra en texto plano, como una constante en el codigo. Tambien es posible que aparezca en los logs por ejemplo. 
**Prueba**: descompilar el codigo del APK y buscar credenciales. Intentar hacer uso de herramientas automatizadas que hagan esto.
## SQLi
**Hipotesis**: si bien la API REST esta correctamente protegida, es posible que no se esten escapando todos los campos de input del usuario, lo que podria terminar en un SQL injection
**Prueba**: probar poniendo en los input secuencias como: ' OR 1=1'-- para ver si esto termina ejecutando codigo en la base de datos
## Replay attack
**Hipotesis**: la API REST permite que se le envie el mismo paquete dos veces, lo que puede ocasionar problemas en ciertos casos (como el de pedir un prestamo)
**Prueba**: intentar enviar el mismo paquete multiples veces para ver que pasa