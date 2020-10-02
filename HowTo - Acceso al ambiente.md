![Logos](img/Logo-IBM-INCO.PNG)
# Implementando OpenId y SSO en Datapower

---

## ¿Qué es Skytap?

*IBM Cloud for Skytap Solutions* (ICSS) es un proveedor de nube pública que acelera la innovación empresarial mediante la modernización de las aplicaciones tradicionales. Los entornos ICSS Cloud facilitan el desarrollo y la ejecución de aplicaciones híbridas mediante la migración rápida de cargas de trabajo tradicionales a la nube, lo que permite prácticas modernas de ciclo de vida de desarrollo de software (SDLC) e integra nuevas arquitecturas y servicios nativos de la nube.

Skytap es la solución de ambientes en la nube que IBM utiliza para realizar Demostraciones, Pruebas de tecnologías (PoT), Pruebas de concepto (PoC) y talleres *hands-on* para conocer de primera mano la experiencia de utilizar las capacidades de los productos de ibm

Mas información sobre Skytap en https://www.ibm.com/ar-es/cloud/skytap

## ¿Cómo accedo al ambiente del taller?

Al hacer una reservación, recibirás un correo de dte@us.ibm.com con la información de accesos al ambiente. Al acceder al enlace en la sección "Desktop Access Information" se nos presentará la siguiente ventana

![Skytap - Acceso a ambientes](img/Skytap%20-%20Acceso%20a%20ambiente.PNG)

Colocaremos el password que viene en la misma sección. Al presionar el botón "Submit" se nos presentará la consola de gestión de las vms que conforman el taller. En este caso, se presentará de esta información

![Skytap - VMs del ambiente](img/Skytap%20-%20VMs%20del%20ambiente.PNG)

Las máquinas que constituyen nuestro laboratorio son:

* __Boot/Master - Ubuntu__: Esta máquina es donde realizaremos todos los pasos del taller. Es un desktop Ubuntu que tiene acceso a la instancia de Datapower
* __Datapower_V7.7.1.3__: Esta vm aloja la instancia virtual de datapower

Si las vms se presentan como la pantalla, debemos encenderlas. Para ello, presionamos el botón "Play" en la barra de opciones

Esperaremos a que las vms enciendan, el estado final debe lucir como la siguiente imágen

![Skytap - VMs encendidas](img/Skytap%20-%20VMs%20del%20ambiente%20encendidas.PNG)

Toma aproximadamente unos 5 minutos que todos los componentes estén arriba y funcionando.

Ahora accederemos a nuestro desktop de trabajo, presionamos el botón [RDP] arriba de la vm *Boot/Master - Ubuntu*

![Skytap - Acceso RDP](img/Skytap%20-%20RDP%20vm%20de%20trabajo.PNG)

Listos para trabajar!!! Accede al paso a paso del [primer laboratorio acá](Lab%201%20-%20OIDC%20proveedor%20Interno/README.md)
