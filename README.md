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



Este proyecto muestra la implementación de \*\*segmentación de red mediante VLANs\*\* usando un router con la técnica \*\*Router-on-a-Stick\*\*.



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



\- VLAN 1 → 192.168.1.0/24

\- VLAN 5 → 192.168.5.0/24

\- Interfaz física: `GigabitEthernet0/0/0`

\- Subinterfaces configuradas para cada VLAN



\---



\## ⚙️ Configuración Paso a Paso



\---



\### 🔹 Paso 1 – Guardar configuración



```bash

write memory

