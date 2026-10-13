# Práctica 1 de SAD · SecureCorp — Respuestas

**Nombre y apellidos:Sergio Gonzalez Partida**
**Usuario:sgonzalez**

Responde con tus palabras, en 1-3 líneas. En la defensa te preguntaré lo mismo en voz alta.

**Contraseñas que has usado** (solo porque es un laboratorio; en una empresa, jamás en un fichero):

- Tu usuario:sgonzalez
- mtorres:

---

**1. (A1)** ¿Quién es el `issuer` de tu `ca.crt`? ¿Hasta qué fecha es válido? ¿Por qué el `subject`
y el `issuer` de la CA son iguales y los de `ldap.crt` no?
El issuer de ca.crt es C = ES. 
Es valido hasta el 4 de octubre de 2036 a hasta la hora 17:10:36.
El subject y el issuer son igual porque la misma entidad que es dueña del certificado lo ha firmado.Es decir es un certificado autofirmado.
Porque el subject de ldap.crt es el servidor LDAP y quien lo firma es el CA.

**2. (A3)** Pega el comando y el resultado de tus dos búsquedas:

```
a) miembros de rrhh:
Lucia y Marta
b) cn y mail de todas las personas:
lromero@securecorp.local      cn:Lucia Romero
mtorres@securecorp.local      cn:Sergio Gonzalez
sgonzalez@securecorp.local    cn:Marta Torres
```
Contraseña sgonzalez: Sergio2026
Contraseña mtorres: Marta2026
**3. (A4)** ¿Por qué la clave `ldap.key` tiene que ser de `openldap` y tener permisos 600?

Porque el servicio slapd se ejecuta como usuario openldap y necesita leer la clave privada. Los permisos 600 permiten leer y escribir únicamente al propietario, protegiendo la clave frente a otros usuarios.

**4. (A4)** ¿Qué valor has puesto en `SLAPD_SERVICES` y por qué?
SLAPD_SERVICES="ldaps:/// ldapi:///"

Porque ldaps:/// permite conexiones cifradas mediante TLS por el puerto 636, mientras que ldapi:/// permite la administración local. Se elimina ldap:/// para desactivar las conexiones sin cifrar por el puerto 389.

**5. (A4)** Antes de añadir `TLS_CACERT` en el cliente, `ldaps://` no funcionaba. ¿Por qué?

Porque el cliente no confiaba en la autoridad de certificación (CA) que había firmado el certificado del servidor. Al añadir TLS_CACERT con la ruta de ca.crt, el cliente puede verificar el certificado y establecer una conexión TLS segura.

**6. (B3)** Pega la salida de `klist` con tus dos tickets. ¿Para qué sirve cada uno? ¿Ha v>
contraseña por la red?




Ticket cache: FILE:/tmp/krb5cc_0
Default principal: sgonzalez@SECURECORP.LOCAL

Valid starting     Expires            Service principal
10/12/26 23:28:20  10/13/26 09:28:20  krbtgt/SECURECORP.LOCAL@SECURECORP.LOCAL
    renew until 10/19/26 23:28:20
10/12/26 23:28:30  10/13/26 09:28:20  host/web.securecorp.local@SECURECORP.LOCAL
    renew until 10/19/26 23:28:20

krbtgt/securecorp... , nos permite solicitar tickets para otros servicios sin necesidad de introdu
cir contrase;a
host/web.securecorp... , permite que la pagina web sepa quienes somos, es decir, nuestra identidad
```

```

**7. (C)** En el `docker-compose.yml`, ¿qué diferencia hay entre `build:` e `image:`? ¿Qué
significa la línea `- "8081:80"` del servicio `phpldapadmin`?

Buildm indica donde esta el dockerfile con el que se construye la imagen y image indica el nombre de la imagen que se utiliza para creaar el contenedor.
"8081:80" conecta el puerto 8081 del ordenador con el puerto 80 del contenedor phpldapadmin, permitiendo acceder desde el ordenador usando el puerto 8081.

**8. (C)** ¿Por qué en la máquina `web` no has tenido que escribir a mano `TLS_CACERT`, y en el
cliente sí? ¿Qué pasaría con esa línea del cliente si hicieras `./lab.sh reset`?

Porque en la maquina web se a;ade automaticamente durante la construccion de la imagen.
Se perderia la configuracion del cliente y tendriamos que volver a hacerla.
