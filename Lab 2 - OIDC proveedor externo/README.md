![Logos](../img/Logo-IBM-INCO.PNG)
# Implementando OpenId y SSO en Datapower

# Laboratorio 2 - OIDC con proveedor Externo de identidades

En este laboratorio crearemos y configuraremos los objetos de datapower para brindar autenticación de credenciales de usaurio usando conectores de OpenID. La validación de la credencial se hará contra google.

## Pasos del laboratorio

**Requisitos**

- Cuenta de google
- Registro de DNS Externo para Datapower

**Paso 1** Acceder a la consola de gestión de DataPower

1. En la vm de trabajo, abrimos una ventana de firefox y accedemos a la cónsola de administración de datapower en `https://datapower:9090`

![IDG - Consola Datapower](../img/IDG%20-%20Login%20consola%20Datapower.PNG)

Las credenciales de acceso:

  * Usuario __student__
  * password __Passw0rd__
  * Domain __student__

**Paso 2** Registrar a datapower como cliente de OIDC de Google

1. Abrimos pestaña en firefox con esta dirección `https://console.developers.google.com/project`

2. Usamos nuestra cuenta de usuario de Google para acceder. *Nota:* Google solicitará validar la conexión con el ambiente de la Dejamos

![Google Cloud resource manager](../img/Google%20-%20Cloud%20resource%20manager.PNG)

3. Creamos un nuevo proyecto presionando [Crear Proyecto] y le colocamos el nombre `datapower-gatewy`

![Google Cloud resource manager](../img/Google%20-%20New%20Project.PNG)

4. Accedemos a las credenciales del Proyecto

![Google Credenciales](../img/Google%20-%20Menu%20Credenciales.PNG)

5. Creamos una pantalla de consentimiento para usuarios externos y pulsamos el botón [Crear].

![Google Pantalla consentimiento](../img/Google%20-%20Pantalla%20consentimiento.PNG)

6. Acedemos a la opción de credenciales y pulsamos el botón [Crear credenciales] y seleccionamos `ID de cliente OAuth`. Llenamos el formulario de acuerdo a la siguiente imagen

![Google Credencial OAuth](../img/Google%20-%20Credencial%20OAuth.PNG)

Colocamos el nombre de nuestro cliente y creamos el URI de redirección apuntando al DNS de nuestro Datapower. - ulsamos el botón [Crear]

7. Copiamos el ID de cliente y la clave generadas por Google

![Google claves de OAuth](../img/Google%20-%20Claves%20OAuth.PNG)


**Paso 3** Crear y configurar servicio de multiprotocolo para peticiones de OIDC

1. Creamos un nuevo servicio multi-protocol configurandolo de la siguiente formato

* __Name__: `google-login-Service`
* __URL__: `http://127.0.0.1:2090/`
* En la sección __Proxy Settings__
  * __Request type__: `Non-XML`
  * __Response type__: `Pass through`
* Regresamos a la sección principal y en __Front side protocol__ pulsamos el botón [Add]

![Google - Configuración del MPG](../img/Google%20-%20MPG%20Config.PNG)

2. Creamos el Front side handler para nuestra petición como se muestra en la imágenes

![Google - Configuración del Front side Handler](../img/Google%20-%20MPG%20FrontSide%20Handler.PNG)

3. Creamos una nueva política de procesamiento para nuestro multi protocolo. Para ello, pulsamos (+)

4. En la sección principal, creamos una nueva política de procesamiento
* __Policy name__: `google-login`
* Creamos una nueva regla, seleccionando la dirección `Client to server`
  * Configuramos la acción match en `All`
  * Agregamos una acción AAA como se muestra en las siguientes imágenes. Al terminar, agregaremos una acción `Result` para cerrar la regla

![Google - MPG Processing Policy](../img/IDG%20-%20MPG%20ReqRule%20AAA%20paso%201.PNG)

Creamos una nueva política de login social presionando el botón [+]

![Google - MPG AAA policy](../img/Google%20-%20MPG%20AAA%20Social%20Login%20Policy.PNG)

Creamos un validador para nuestro token pulsando (+) en el campo `JWT Validator`

![Google - MPG JWK Validator](../img/Google%20-%20MPG%20AAA%20JWK%20validator.PNG)

El resto de los formularios de la política AAA se llenan de esta forma

![IDG - MPG  Request Rule](../img/IDG%20-%20MPG%20ReqRule%20AAA%20paso%203.PNG)

![IDG - MPG  Request Rule](../img/IDG%20-%20MPG%20ReqRule%20AAA%20paso%204.PNG)

* Crearmos una nueva regla, seleccionando la dirección `Server to Client`
  * Configuramos la acción match en `All`
  * Anexaremos una acción GatewayScript para procesar el token de retorno de nuestro servicio de OIDC. Esto lo hacemos para presentarlo en el repsonse en formato JSON.

![IDG - MPG  Response Rule](../img/IDG%20-%20MPG%20RespRule%20GwScript%201.PNG)

![IDG - MPG  Response Rule](../img/IDG%20-%20MPG%20RespRule%20GwScript%202.PNG)

Guardamos todos los cambios y verifiquemos que el servicio esté arriba.

**Paso 4**  Crear un cache de certificado de OAuth para mejor performance

1. En la configuración del multi-protocol, creamos un nuevo XML Manager presionando el botón (+)

![Google XML Manager](../img/Google%20-%20XML%20Manager.PNG)

2. Creamos la entrada del cache para los certificados de Google para acelerar las validaciones de los tokens

![Google XML Manager](../img/Google%20-%20XML%20Manager%20Cache.PNG)

**Paso 6** Probar desarrollo

1. Accedemos desde firefox a este URL `https://ibmair.ibm.com:1087/test`

2. Se nos presentará el formulario de Google para colocar las credenciales de usuario

![Google login](../img/Google%20-%20Test%20Login.PNG)

3. Google solicitará validar el acceso del ambiente a través de un segundo factor de autenticación.

4. Finalmente, el resultado esperado

![Google Resultado final](../img/Google%20-%20Test%20Resultado.PNG)

## Resumen y siguiente laboratorio

* Creamos una configuración de OAuth en Google para registrar a datapower como cliente de OpenID
* Construimos una configuración para política de login social donde configuramos a Google como proveedor de identidades
* Publicamos nuestro servicio en DataPower usando un Multi-protocol Gateway

[Volver a la presentación del Lab](../README.md)
