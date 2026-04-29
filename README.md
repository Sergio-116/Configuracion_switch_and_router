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

Este proyecto muestra la implementación de segmentación de red mediante VLANs usando un router y un switch.

Se configura desde cero:
- Nombre del equipo
- Interfaces
- VLANs
- Subinterfaces
- Direccionamiento IP
- Pruebas de conectividad (PING)

---

## 🧠 Modelo OSI

![OSI](imagenes/imagen%20(8).jpeg)

El modelo OSI divide la red en 7 capas:

- Física
- Enlace de datos
- Red
- Transporte
- Sesión
- Presentación
- Aplicación

---

## 🧠 Modelo TCP/IP

![TCP/IP](imagenes/imagen%20(8).jpeg)

Modelo práctico usado en Internet:

- Aplicación
- Transporte
- Internet
- Acceso a red

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

![Rack](Multimedia.jpeg)
![Router](Multimedia%20(2).jpeg)
![Switch](Multimedia%20(3).jpeg)
![Switch frontal](Multimedia%20(4).jpeg)

---

# ⚙️ CONFIGURACIÓN PASO A PASO

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