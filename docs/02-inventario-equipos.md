# 02. Inventario y Rol Técnico de los Componentes de la Maqueta

Este documento detalla el inventario de hardware de la maqueta **DWDM** disponible en el laboratorio, especificando la función, el tipo de interfaces físicas y el rol técnico asignado a cada uno de los 7 componentes principales dentro del rack de telecomunicaciones.

---

## 1. Vista General del Layout del Rack (Esquema Visual)

El rack del laboratorio organiza los componentes de transmisión, agregación, simulación y medición de la siguiente manera:
*(Nota: Aquí puedes incrustar una imagen del layout físico si cuentas con ella en la carpeta `diagramas/imagenes/`)*

## 2. Descripción Detallada de los Componentes

### Instrumentación y Medición

* **1. Analizador Ethernet (MTX150x)**
  * **Función:** Generación, inyección y análisis de tráfico de datos en Capa 2 (L2) y Capa 3 (L3). Es el encargado de estresar el sistema y validar el rendimiento extremo a extremo de la red de transporte mediante los estándares internacionales **RFC 2544** (Rendimiento, Latencia, Pérdida de paquetes, Back-to-back) e **Y.1564** (Validación de Niveles de Servicio o SLA)[cite: 1].
  * **Tipo de Interfaz:** Puertos eléctricos RJ-45 (10/100/1000 Base-T) y puertos ópticos SFP/SFP+ (1G/10G Ethernet).
  * **Rol Técnico:** Actúa como el cliente de datos activo de la red. Genera la carga útil de tráfico que entra por el Switch de agregación para medir la calidad del transporte óptico.

* **2. Analizador de Espectro Óptico - OSA (RXT4510)**
  * **Función:** Escaneo y análisis del dominio de la frecuencia y longitud de onda en la fibra óptica. Permite la visualización de los canales activos en la Banda C, la medición precisa de la potencia óptica individual por canal óptico (**dBm**) y el cálculo de la relación señal a ruido óptica (**OSNR**)[cite: 1].
  * **Tipo de Interfaz:** Puerto de entrada óptica monomodo universal (normalmente con conectores FC/APC o SC/APC de alta precisión para evitar reflexiones).
  * **Rol Técnico:** Instrumento de diagnóstico crítico en la línea de transmisión. Se conecta a los puertos de monitoreo (*MON*) de los chasis DWDM o amplificadores para evaluar la salud espectral de las señales combinadas sin interrumpir el tráfico.

---

### Agregación y Enrutamiento Físico

* **3. Switch Ethernet (CSS610)**
  * **Función:** Agregación de tráfico de múltiples clientes y conmutación de datos a velocidad de línea en el borde de la red[cite: 1].
  * **Tipo de Interfaz:** 8 puertos Gigabit Ethernet (RJ-45) y 2 puertos 10G SFP+.
  * **Rol Técnico:** Concentrador de acceso. Recibe los servicios Ethernet de baja velocidad o del analizador de tráfico y los consolida en enlaces de alta velocidad (uplinks ópticos) hacia las tarjetas transpondedoras de los chasis DWDM.

* **4. ODF (Optical Distribution Frame)**
  * **Función:** Panel de distribución óptica que centraliza, organiza, protege y termina mecánicamente los hilos de fibra del rack, facilitando el parcheo seguro entre equipos activos y la planta externa simulada[cite: 1].
  * **Tipo de Interfaz:** Pasamuros/Acopladores ópticos, típicamente de tipo **LC/UPC** (azul) o **SC/APC** (verde).
  * **Rol Técnico:** Punto de interconexión y flexibilidad física. Toda la conectividad entre los multiplexores ópticos, carretes de fibra e instrumentos pasa por el ODF para evitar el desgaste directo de los puertos internos de los equipos DWDM.

---

### Sistema de Transporte DWDM

* **5. Chasis DWDM 1 y DWDM 2 (HT6000)**
  * **Función:** Plataforma modular activa de transporte óptico. Aloja y gestiona las tarjetas encargadas de la conversión electro-óptica (Transpondedores/Muxpondedores), las tarjetas de filtros multiplexores/demultiplexores (MUX/DEMUX) y los módulos de gestión y control remoto de la red de transporte[cite: 1].
  * **Tipo de Interfaz:** Puertos de gestión RJ-45 (Consola/Ethernet), bahías modulares para tarjetas de línea DWDM, y puertos ópticos SFP+/XFP/QSFP28 en los módulos transpondedores.
  * **Rol Técnico:** Núcleo de la tecnología DWDM de la maqueta. El Chasis 1 opera como el Nodo Local (Transmisor/Edfas de emisión) y el Chasis 2 opera como el Nodo Remoto (Receptor/Edfas de recepción), permitiendo el transporte masivo multicanal sobre la red óptica.

---

### Medio de Transmisión y Simulación

* **6. Carretes de Fibra Óptica (AB - 25 KM y BA - 25 KM)**
  * **Función:** Bobinas de prueba cerradas que contienen fibra óptica monomodo real para emular el comportamiento físico de un enlace de transmisión interurbano o metropolitano de larga distancia[cite: 1].
  * **Tipo de Interfaz:** Conectores ópticos macho SC/APC o FC/APC de baja pérdida en los extremos de la caja contenedora.
  * **Rol Técnico:** Medio de transmisión física (Planta Externa). Simulan un vano óptico real de 25 km en sentido de ida (A a B) y 25 km en sentido de retorno (B a A), introduciendo al sistema atenuación geométrica, dispersión cromática y retardo de propagación reales.

* **7. Atenuador Óptico Variable - OVA (JW3303)**
  * **Función:** Introducción controlada, precisa y ajustable de pérdidas de potencia óptica (**dB**) en el trayecto de la luz sin alterar las características espectrales de la señal[cite: 1].
  * **Tipo de Interfaz:** Puertos ópticos de entrada y salida Monomodo (SM), típicamente con conectores FC o SC.
  * **Rol Técnico:** Simulador de degradación de enlace y margen de seguridad. Se coloca en serie con los carretes de fibra para simular un envejecimiento de la fibra, cortes reparados (atenuación por fusión) o fallas físicas en la ruta, permitiendo evaluar el límite operacional y el umbral de recepción de los transceptores ópticos.
