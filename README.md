\# 🌐 Configuración de VLANs en Router (Router-on-a-Stick)



<p align="center">

&#x20; <img src="https://img.shields.io/badge/Networking-Cisco-blue?style=for-the-badge">

&#x20; <img src="https://img.shields.io/badge/VLAN-802.1Q-orange?style=for-the-badge">

&#x20; <img src="https://img.shields.io/badge/Level-Professional-success?style=for-the-badge">

</p>



\---



\## 📑 Tabla de Contenido



\- \[📌 Introducción](#-introducción)

\- \[🧠 Conceptos Clave](#-conceptos-clave)

\- \[🏗️ Arquitectura](#️-arquitectura)

\- \[⚙️ Configuración Paso a Paso](#️-configuración-paso-a-paso)

\- \[🧪 Validación](#-validación)

\- \[🚨 Errores Comunes](#-errores-comunes)

\- \[🎯 Conclusión](#-conclusión)



\---



\## 📌 Introducción



Este proyecto muestra la implementación de \*\*segmentación de red mediante VLANs\*\* usando un router y swich, donde se lleva acabo inicialmente con las referencias de Router cisco 8200 y Swich calister 1000 series.


Durante este proceso se a va aprender la configurar ambos elementos desde el emulador de terminal \*\*PuTTY\*\*, que permite a los administradores y programadores gestionar servidores Linux, corregir transferencias de archivos, además, se va a explicar conceptos básicos para el entendimiento de la configuración, funcionamiento de los elementos anteriormente mencionados.  

Abordando, en los elementos de trabajo, un router es un dispositivo de red de alto rendimiento diseñado para conectar múltiples redes dirigir el trafico de datos entres ellas y gestionar el acceso a internet. Entre las características y funcionalidades principales son la conectividad de red, enrutamiento inteligente, seguridad, protocolos.

Actualmente en el mercado cisco ofrece varios tipos de router, entre ellos están, los principales (Core), perimetrales (Edge) y de distribución.



* \*\*Router principal\*\*: Proporciona el máximos ancho de banda para conectar otros routers o switches.
* \*\*Router perimetral\*\*: Soporta protocolos de enrutamiento tanto estáticos como dinamicos (como RIP, OSPF, EIGRP, BGP).
* \*\*Router de distribución\*\*: Recibe datos del borde y los distribuye a la red local. 


Dando un acercamiento a redes hay que tener en cuenta que se manejan varios niveles inicial en el modelos OSI (\*\*Open Systems Interconnection\*\*) es un marco conceptual estandarizado por la ISO en 1984, que divide la comunicación de red en siete capas abstractas, donde facilita la interoperabilidad entre distintos sistemas, al definir funciones especificas para la tranasmición de datos desde la conexión física hasta la aplicacion de usuario.



\### Modelo OSI

* \*\*Capa Física\*\*: define las especificaciones eléctricas y mecánicas de la conexión, como cables, conectores y niveles de voltaje. Transmite los datos como un flujo de bits sin procesar.
* \*\*Capa de enlace de datos\*\*: proporciona la transferencia de datos entre dos nodos conectados directamente en la misma red física. Organiza los datos en \*\*Tramas\*\*  y maneja el direccionamiento físico (\*\*MAC\*\*).
* \*\*Capa de red\*\*: se encarga del enrutamiento de los datos. Determina la mejor ruta física para que los datos lleguen a su destino a través de diferentes redes (protocolo \*\*IP\*\*)
* \*\*Capa de Transporte\*\*: responsable de la transferencia de datos extremos a extremo. Incluye el control de errores y flujo para garantizar que los datos lleguen correctamente (Protocolos \*\*TPC y UDP\*\*).
* \*\*Capa de sesión\*\*: Administra el inicio, la gestión y el cierre de las sesiones de comunicación entre aplicaciones. Contola el diálogo entre los dos nodos. 
* \*\*Capa de presentación\*\*: se encarga de traducir, cifrar y comprimir los datos para que sean comprensibles para la capa de aplicación. Asegura que los dispositivos puedan enternderse aunque usen diferentes formatos de datos.
* \*\*Capa de aplicación\*\*: es la única capa que interactúa directamente con los datos del usuario y recibir información del usuario. Proporciona protocolos que permiten a las aplicaciones de software y recibir información (Navegadores web \*\*HTTPS\*\*)



\### Modelo TCP/IP


El modelo TCP/IP es el "lenguaje" real de Internet. A diferencia del OSI, que es un marco teórico educativo, el TCP/IP fue diseñado para ser práctico y robusto, permitiendo que computadoras de todo el mundo se conecten sin importar su hardware.



Este modelo se divide en 4 capas principales. Su filosofía es la simplicidad: agrupa funciones para que el procesamiento sea más rápido.



* \*\*Capa de Aplicación\*\*: Combina las capas 5, 6 y 7 del modelo OSI. Aquí residen los protocolos que usamos a diario como \*\*HTTP\*\* (web), \*\*SMTP\*\* (correo) y \*\*FTP\*\* (archivos). Se comunica directamente con los procesos de software.
* \*\*Capa de Transporte\*\*: Similar a la capa 4 de OSI. Se encarga de la comunicación host a host. Sus dos protagonistas son:

  * \*\*TCP\*\*: Fiable, garantiza que los datos lleguen completos.
  * \*\*UDP\*\*: Rápido, pero no garantiza la entrega (ideal para video en vivo).
* \*\*Capa de Internet\*\*: Equivale a la capa de Red de OSI. Su función principal es el direccionamiento IP y el enrutamiento. Aquí es donde se decide qué camino toman los paquetes para llegar a su destino.
* \*\*Capa de Acceso a la Red\*\*: Une las capas 1 y 2 de OSI. Define cómo se envían físicamente los datos a través de los medios (cables, fibra, Wi-Fi).





|\*\*Características\*\* | \*\*modelo OSI (Teórico)\*\*|\*\*Modelo TCP/IP (Práctico)\*\*|

|--------------------|-------------------------|----------------------------|

|Estructura|7 Capas detalladas |4 capas simplificadas|

|Enfoque| Se centra en qué debe hacer cada capa |Se centra en cómo conectar sistemas|




Se utiliza el protocolo \*\*IEEE 802.1Q (dot1Q)\*\* para permitir que múltiples VLANs viajen a través de una sola interfaz física, utilizando \*\*subinterfaces\*\*.



\---



\## 🧠 Conceptos Clave



| Concepto | Descripción |

|----------|------------|

| VLAN | Segmentación lógica de red |

| Subinterfaces | Interfaces virtuales dentro de una física |

| dot1Q | Protocolo de etiquetado VLAN |

| Trunk | Enlace que transporta múltiples VLANs |

| Router-on-a-Stick | Enrutamiento entre VLANs con un solo puerto |



\---



\## 🏗️ Arquitectura



* VLAN 1 → 192.168.1.0/24
* VLAN 5 → 192.168.5.0/24
* Interfaz física: `GigabitEthernet0/0/0`
* Subinterfaces configuradas para cada VLAN



\---



\## ⚙️ Configuración Paso a Paso



\---



\### 🔹 Paso 1 – Guardar configuración



```bash

write memory

