# 🌐 CONFIGURACIÓN DE VLANs EN ROUTER (Router-on-a-Stick)

<p align="center">
  <img src="https://img.shields.io/badge/Networking-Cisco-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/VLAN-802.1Q-orange?style=for-the-badge">
  <img src="https://img.shields.io/badge/Level-Professional-success?style=for-the-badge">
</p>

---

## 📑 Tabla de Contenido

- 📌 Introducción
- 🧠 Conceptos Clave
- 🏗️ Arquitectura
- 🖥️ Equipos
- ⚙️ Configuración Paso a Paso
- 🧪 Validación
- 🚨 Errores Comunes
- 🎯 Conclusión

---

## 📌 Introducción

Este proyecto muestra la implementación de **segmentación de red mediante VLANs** usando un router y swich, donde se lleva acabo inicialmente con las referencias de Router cisco 8200 y Swich calister 1000 series.

Durante este proceso se a va aprender la configurar ambos elementos desde el emulador de terminal **PuTTY**, que permite a los administradores y programadores gestionar servidores Linux, corregir transferencias de archivos, además, se va a explicar conceptos básicos para el entendimiento de la configuración, funcionamiento de los elementos anteriormente mencionados.

Abordando, en los elementos de trabajo, un router es un dispositivo de red de alto rendimiento diseñado para conectar múltiples redes dirigir el trafico de datos entres ellas y gestionar el acceso a internet. Entre las características y funcionalidades principales son la conectividad de red, enrutamiento inteligente, seguridad, protocolos.

Actualmente en el mercado cisco ofrece varios tipos de router, entre ellos están, los principales (Core), perimetrales (Edge) y de distribución.



**Router perimetral**: Soporta protocolos de enrutamiento tanto estáticos como dinamicos (como RIP, OSPF, EIGRP, BGP).

**Router de distribución**: Recibe datos del borde y los distribuye a la red local.

Dando un acercamiento a redes hay que tener en cuenta que se manejan varios niveles inicial en el modelos OSI (**Open Systems Interconnection**) es un marco conceptual estandarizado por la ISO en 1984, que divide la comunicación de red en siete capas abstractas, donde facilita la interoperabilidad entre distintos sistemas, al definir funciones especificas para la tranasmición de datos desde la conexión física hasta la aplicacion de usuario.



## 🧠 Modelo OSI

![Paso 2](https://github.com/Sergio-116/Configuracion_switch_and_router/blob/c43ed31840975eee00f67be5bf404b3be642a7f1/imagenes/imagen%20(8).jpeg)

El modelo OSI divide la red en 7 capas:

**Capa Física**: define las especificaciones eléctricas y mecánicas de la conexión, como cables, conectores y niveles de voltaje. Transmite los datos como un flujo de bits sin procesar.

**Capa de enlace de datos**: proporciona la transferencia de datos entre dos nodos conectados directamente en la misma red física. Organiza los datos en **Tramas**  y maneja el direccionamiento físico (**MAC**).

**Capa de red**: se encarga del enrutamiento de los datos. Determina la mejor ruta física para que los datos lleguen a su destino a través de diferentes redes (protocolo **IP**)

**Capa de Transporte**: responsable de la transferencia de datos extremos a extremo. Incluye el control de errores y flujo para garantizar que los datos lleguen correctamente (Protocolos **TPC y UDP**).

**Capa de sesión**: Administra el inicio, la gestión y el cierre de las sesiones de comunicación entre aplicaciones. Contola el diálogo entre los dos nodos.

**Capa de presentación**: se encarga de traducir, cifrar y comprimir los datos para que sean comprensibles para la capa de aplicación. Asegura que los dispositivos puedan enternderse aunque usen diferentes formatos de datos.

**Capa de aplicación**: es la única capa que interactúa directamente con los datos del usuario y recibir información del usuario. Proporciona protocolos que permiten a las aplicaciones de software y recibir información (Navegadores web **HTTPS**)

---

## 🧠 Modelo TCP/IP

![Paso 3](https://github.com/Sergio-116/Configuracion_switch_and_router/blob/c43ed31840975eee00f67be5bf404b3be642a7f1/imagenes/imagen%20(9).jpeg)

El modelo TCP/IP es el marco conceptual básico de Internet, desarrollado en los años 70 para permitir la comunicación fiable entre equipos. Se organiza en cuatro capas: Aplicación, Transporte, Internet y Acceso a la Red. Define cómo se formatean, direccionan, transmiten y reciben los datos extremo a extremo.

**3. Capa de Aplicación**

Es el nivel más alto, el que tú ves. Su función es proporcionar la interfaz entre el software (tu navegador, app de correo, etc.) y la red.

- Para qué funciona: Define los protocolos que usan las aplicaciones para intercambiar datos. Por ejemplo, cuando escribes una URL, el protocolo HTTP/HTTPS entra en acción; si envías un correo, usas SMTP.

- Nota : Aquí los datos aún no tienen formato de red, son simplemente la información pura (el texto de un mensaje o el código de una web).

**2. Capa de Transporte** 

Aquí es donde se decide cómo va a viajar la información. Su función principal es la comunicación extremo a extremo y el control de flujo.

- Para qué funciona: Divide los datos de la aplicación en trozos más pequeños llamados segmentos. Utiliza dos protocolos principales:

- **TCP**: Es el "mensajero responsable". Verifica que todos los datos lleguen, en orden y sin errores. Si algo se pierde, lo pide de nuevo.

- **UDP**: Es el "mensajero veloz". Envía los datos sin verificar si llegaron. Se usa para streaming o juegos online donde la velocidad importa más que un error mínimo.

**3. Capa de Internet (o Red)**

Esta capa es el "GPS" del modelo. Se encarga de que los paquetes sepan qué camino tomar para llegar a su destino.

- **Para qué funciona**: Toma los segmentos de la capa de transporte y les añade la **dirección IP** de origen y de destino, convirtiéndolos en **paquetes**. El protocolo principal es el **IP**.

- **Dato clave**: Aquí es donde trabajan los routers. Su trabajo es decidir cuál es la ruta más rápida a través de la enorme red de redes que es Internet.

**4. Capa de Acceso a la Red (o Enlace)**

Es la capa física. Se encarga de cómo los bits (0 y 1) se convierten en señales eléctricas, de radio o luz para viajar por un cable o por el aire.

- **Para qué funciona** : Empaqueta los paquetes de internet en tramas que el hardware puede entender. Gestiona la dirección física de los dispositivos (la dirección MAC).

Ejemplos: Aquí es donde operan el Ethernet (cable), el Wi-Fi y la fibra óptica.


---

## 🏗️ Arquitectura


- VLAN 1 → 192.168.1.0/24  
- VLAN 5 → 192.168.5.0/24  

- Interfaz: `GigabitEthernet0/0/0`

- Subinterfaces:
  - G0/0/0.1 → VLAN 1
  - G0/0/0.5 → VLAN 5

---

## 🖥️ Equipos


![Paso 1](https://github.com/Sergio-116/Configuracion_switch_and_router/blob/864633234fb39ae6a4f66776b361625041f57dae/imagenes/Torre.gif)

---

# ⚙️ CONFIGURACIÓN PASO A PASO

![Paso 4](https://github.com/Sergio-116/Configuracion_switch_and_router/blob/864633234fb39ae6a4f66776b361625041f57dae/imagenes/codigo.gif)


---

## 🔹 1. Configuración del Router

---

### 🟢 Paso 1: Entrar a configuración

Primero se accede al modo privilegiado (enable) y luego al modo de configuración global.
Aquí es donde se pueden hacer cambios en el dispositivo.

enable
configure terminal



### 🟢 Paso 2: Nombre del router

Se cambia el nombre del equipo para identificarlo fácilmente dentro de la red.
Esto es importante en entornos reales donde hay muchos dispositivos.

hostname Raticas


### 🟢 Paso 3:Seleccionar la interfaz 

Se accede a la interfaz física del router que se va a usar para conectar con el switch.
Esta interfaz será la base para crear las subinterfaces.

interface GigabitEthernet0/0/0

interface GigabitEthernet0/0/0.1
encapsulation dot1Q 1
ip address 192.168.1.1 255.255.255.0
no shutdown


### 🟢 Paso 4: Crear subinterfaces

Una subinterfaz es una interfaz virtual dentro de una interfaz física.
Se utiliza para manejar múltiples VLANs en un solo puerto (Router-on-a-Stick).

**VLAN 1**

interface GigabitEthernet0/0/0.1
encapsulation dot1Q 1
ip address 192.168.1.1 255.255.255.0
no shutdown

**VLAN 5**

interface GigabitEthernet0/0/0.5
encapsulation dot1Q 5
ip address 192.168.5.1 255.255.255.0
no shutdown


### 🟢 Paso 5: Activar interfaz

Se indica qué VLAN va a manejar esa subinterfaz.
El protocolo 802.1Q permite etiquetar el tráfico para identificar a qué VLAN pertenece.

interface GigabitEthernet0/0/0
no shutdown

Por defecto, las interfaces están apagadas.
Este comando las activa para que puedan transmitir datos.


### 🟢 Paso 6: Guardar configuración

Se asigna la IP que será la puerta de enlace (gateway) para esa VLAN.
Todos los dispositivos de esa VLAN usarán esta IP para comunicarse con otras redes.


## 2. Configuración del Switch

Se crean las VLANs dentro del switch.
Esto permite separar los dispositivos en diferentes redes lógicas.


###🟢 Crear VLANs

vlan 1
name VLAN_1

vlan 5
name VLAN_5


###🟢 Puertos de acceso

Se define a qué VLAN pertenece cada puerto del switch.
Los dispositivos conectados a ese puerto estarán en esa VLAN.

interface fastEthernet0/1
switchport mode access
switchport access vlan 1
interface fastEthernet0/2
switchport mode access
switchport access vlan 5


###🟢 Configurar TRUNK


El trunk permite que varias VLANs viajen por un solo cable hacia el router.
Es esencial para el Router-on-a-Stick.


interface gigabitEthernet0/1
switchport mode trunk
switchport trunk allowed vlan 1,5
🧪 VALIDACIÓN
- Ver VLANs
show vlans
-  Ping


Permite comprobar que las VLANs están creadas correctamente y activas.

ping ip 192.168.1.1
✔ Resultado
Success rate is 100 percent (5/5)

El ping verifica si hay comunicación entre dispositivos.
Si responde correctamente, significa que la configuración es funcional.

write memory

Guarda todos los cambios realizados.
Si no se guarda, se perderán al reiniciar el equipo.


### 🟢 Varificación de **VLAN**

En el este paso se va realizar verificación de la configuración de la red que se creo manteniendo la conectividad por medio de la **IP**


![Paso 5](https://github.com/Sergio-116/Configuracion_switch_and_router/blob/fb368ce6332ca92d28b2d113dd887ab904f528e6/imagenes/Gif.ConfiguracionRedes.gif)

En este paso colocamos la ip que le nombramos al swicth, la mascara y la puerta de enlace donde esta se van a ver ya que están en su mismo segmento de red, colocamos los DNS de Google y posteriormente realizamos un ping a swicth y al router y nos da ok.
---

###**Colaboradores**

1. David Santiago Prada Briceno
2. Johann Andres Paez Garzón
3. Sergio Esteban Quintana Mesa

