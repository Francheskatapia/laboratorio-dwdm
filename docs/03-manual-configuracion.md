# 03. Manual de Configuración y Procedimientos Operativos

Este documento establece las normativas de seguridad, los pasos de aprovisionamiento del chasis de transmisión y los procedimientos estandarizados de prueba para operar la maqueta DWDM de forma segura y eficiente.

---

## 1. Medidas de Seguridad Óptica

El trabajo con sistemas de transporte óptico de alta capacidad implica riesgos específicos que deben mitigarse antes de manipular cualquier equipo.

### Protección contra Radiación Láser (Clase 1M / 3R)
Las redes DWDM y los amplificadores ópticos utilizan láseres infrarrojos (en la Banda C) que son invisibles al ojo humano y pueden causar daño ocular irreversible.
* **Regla de ogligatoria:** Nunca mirar directamente al extremo de una fibra óptica, un conector o un puerto activo del equipo.
* Considerar siempre que todas las fibras están "vivas" (transmitiendo luz) hasta que se demuestre lo contrario con un medidor de potencia.
* Utilizar los tapones antipolvo en todos los puertos e interfaces ópticas que no estén en uso.

### Limpieza de Conectores Ópticos
La suciedad (polvo, grasa) es la principal causa de fallas en redes ópticas, ya que genera atenuación y reflexiones que degradan el OSNR.
* Inspeccionar siempre el núcleo del conector con un microscopio óptico antes de conectarlo.
* Limpiar la férula utilizando lápices limpiadores mecánicos tipo  toallitas libres de pelusa con alcohol isopropílico de alta pureza.
* Volver a inspeccionar después de la limpieza. **Nunca tocar la punta del conector con los dedos.**

### Manejo de Conectores APC y UPC
Es crítico identificar y no mezclar los tipos de pulido de las férulas, ya que una conexión cruzada destruirá ambos conectores:
* **UPC (Ultra Physical Contact) - Color Azul:** Pulido plano. Común en puertos de equipos de cliente y transceptores SFP/XFP.
* **APC (Angled Physical Contact) - Color Verde:** Pulido en ángulo de 8 grados. Minimiza drásticamente la pérdida de retorno (reflectancia). Es el estándar para redes DWDM, conexiones de amplificadores y el analizador OSA.

---

## 2. Configuración del Chasis DWDM (HT6000)

El proceso de aprovisionamiento en el chasis HT6000 permite establecer el puente entre la red del cliente y la red de transporte DWDM.

### Pasos para el Aprovisionamiento de Servicios
1. **Acceso al sistema:** Ingresar a la interfaz de gestión (WebGUI o CLI) del HT6000 a través del puerto de administración (Management Port) utilizando las credenciales de administrador.
2. **Verificación de hardware:** Confirmar en el panel de estado que las tarjetas transpondedoras/muxpondedoras y los módulos EDFA estén reconocidos y operando sin alarmas (LEDs en verde).
3. **Configuración de Transceptores:** Activar los puertos de cliente y configurar la tasa de bits y el protocolo esperado.

### Mapeo de Puertos y Asignación de Canales
1. **Mapeo Cliente a Línea (Cross-connection):** Configurar lógicamente el transpondedor para que el tráfico ingresado por el puerto cliente "Tx/Rx 1" sea encapsulado y mapeado hacia la interfaz de línea DWDM "Line 1".
2. **Asignación del Canal (Longitud de Onda):** En las interfaces de línea sintonizables (Tunable XFP/SFP+), seleccionar la longitud de onda específica según la grilla ITU-T G.694.1 (ej. Canal 21, 192.1 THz, 1560.61 nm).
3. **Verificación de Potencia:** Habilitar el láser de línea y verificar que la potencia de transmisión (Tx Power) esté dentro de los rangos óptimos de la tarjeta (típicamente entre -1 dBm y +3 dBm).

---

## 3. Procedimiento de Prueba y Medición

Una vez levantado el enlace DWDM a través de los carretes de fibra, se procede a la validación técnica del transporte.

### 3.1 Inserción del Atenuador Óptico Variable (OVA JW3303)
1. Desconectar temporalmente el enlace de fibra en el punto de recepción (antes del EDFA de preamplificación o del puerto de entrada del transpondedor).
2. Insertar el **OVA JW3303** en serie con el enlace, respetando los puertos de entrada (IN) y salida (OUT).
3. Encender el OVA y configurarlo inicialmente con una atenuación de **0 dB**.
4. Incrementar gradualmente la atenuación (en pasos de 1 dB) para simular atenuación en la línea y evaluar el margen de operación del sistema.

### 3.2 Obtención del Espectro Óptico (OSA RXT4510)
1. Conectar el puerto de entrada del **RXT4510** al puerto de monitoreo del chasis HT6000 o mediante un *splitter* óptico en la línea.
2. Configurar los parámetros de escaneo: Rango de longitud de onda (Banda C: 1530 nm a 1565 nm) y resolución (ej. 0.1 nm).
3. Ejecutar el escaneo. Identificar los picos de señal correspondientes a los canales DWDM configurados.
4. Medir y registrar la **Potencia por Canal (dBm)** y la **Relación Señal a Ruido Óptica (OSNR)** de cada portadora para certificar la viabilidad del enlace.

### 3.3 Medición de Rendimiento y BER (MTX150x)
1. Conectar el puerto de prueba del **MTX150x** al puerto de cliente del Switch CSS610 (o directamente al transpondedor en configuración back-to-back).
2. Configurar la prueba **RFC 2544**: Definir el tamaño de las tramas (ej. 64, 512, 1518 bytes) y el tiempo de prueba.
3. Ejecutar el test de rendimiento para verificar la tasa máxima de transferencia (*Throughput*) y registrar la **Pérdida de Tramas (Frame Loss)**.
4. Configurar y ejecutar una prueba de **Bit Error Rate (BER)** por un periodo prolongado (ej. 15-30 minutos) para certificar que el transporte de la capa física esté libre de errores (BER ideal = 0).
