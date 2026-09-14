# 01. Fundamentos Teóricos de DWDM y Redes Ópticas

Este documento contiene el marco teórico obligatorio para la validación y autorización del uso presencial del laboratorio y la maqueta **DWDM (Dense Wavelength Division Multiplexing)**.

---

## 1. Definición de DWDM y Funcionamiento Óptico

La **Multiplexación por División de Longitud de Onda Densa (DWDM)** es una tecnología de transmisión de datos que multiplexa múltiples señales portadoras ópticas en una sola fibra portadora, utilizando diferentes longitudes de onda (colores) de la luz láser.

### Funcionamiento de la Multiplexación Óptica
1. **Conversión:** Las señales eléctricas de los clientes (Ethernet, Fibre Channel, etc.) se convierten en señales ópticas con longitudes de onda específicas y estables (transpondedores).
2. **Multiplexación:** Un multiplexor óptico (MUX) combina estas diferentes longitudes de onda en un único hilo de fibra óptica.
3. **Amplificación:** A lo largo del trayecto, la señal combinada se amplifica ópticamente (usando EDFA) sin necesidad de convertirla a señales eléctricas.
4. **Demultiplexación:** En el extremo receptor, un demultiplexor (DEMUX) separa las longitudes de onda individuales y las entrega a sus respectivos receptores.

### Diferencias Clave: DWDM vs. CWDM

| Característica | CWDM (Coarse WDM) | DWDM (Dense WDM) |
| :--- | :--- | :--- |
| **Espaciamiento de canales** | Amplio (20 nm) | Denso (0.8 nm / 0.4 nm o menor) |
| **Capacidad de canales** | Típicamente hasta 18 canales | Hasta 80, 96 o más canales (Flexible Grid) |
| **Distancia de alcance** | Corto alcance (hasta 80 km), sin amplificar | Largo alcance y ultrametropolitano (miles de km) |
| **Bandas de operación** | Espectro expandido (1270 nm a 1610 nm) | Centrado principalmente en la **Banda C** y **Banda L** |
| **Costo y Láseres** | Láseres no refrigerados (más económicos) | Láseres refrigerados de alta precisión (mayor costo) |

---

## 2. Espectro y Longitudes de Onda (ITU-T G.694.1)

El diseño de canales en sistemas DWDM está estandarizado mundialmente para garantizar la interoperabilidad de los componentes ópticos.

* **Recomendación ITU-T G.694.1:** Define las grillas de frecuencias para las aplicaciones WDM. Especifica las frecuencias centrales nominales basadas en un ancla fija a **193.1 THz (1552.52 nm)**.
* **Operación en Banda C:** DWDM opera principalmente en la **Banda Convencional (C-Band)**, que abarca desde los **1530 nm hasta los 1565 nm** Esta región se selecciona porque presenta la menor atenuación física en la fibra óptica de sílice ($\approx 0.2\text{ dB/km}$) y coincide con la ventana de ganancia de los amplificadores EDFA.

### Espaciamiento de Canales
* **Grilla de 100 GHz:** Espaciamiento fijo de $0.8\text{ nm}$. Permite alojar aproximadamente 40 canales en la Banda C.
* **Grilla de 50 GHz:** Espaciamiento fijo de $0.4\text{ nm}$. Duplica la capacidad de la fibra permitiendo hasta 80 canales.
* **Flexible Grid (Grilla Flexible):** Permite asignar porciones de espectro en ranuras (slots) variables, típicamente con granularidad de **12.5 GHz** para el ancho de banda del canal y **6.25 GHz** para la frecuencia central. Es indispensable para transmisiones coherentes de alta velocidad (400G, 800G y superiores) que requieren mayor ancho de banda espectral.

---

## 3. Modulación Óptica y Conversión Electro-Óptica

La modulación óptica codifica la información digital binaria (bits) en las propiedades físicas de la onda de luz (amplitud, fase y polarización).

### Formatos de Modulación
* **NRZ (Non-Return-to-Zero):** Modulación por amplitud simple (OOK - On-Off Keying). El láser se enciende para un '1' y se apaga o atenúa para un '0'. Limitado para altas velocidades debido a efectos cromáticos.
* **PAM4 (Pulse Amplitude Modulation 4):** Utiliza 4 niveles de amplitud de luz para codificar **2 bits por símbolo**. Reduce a la mitad el ancho de banda requerido frente a NRZ, común en conexiones de centros de datos de corto alcance.
* **QPSK (Quadrature Phase Shift Keying):** Modulación por cambio de fase. Utiliza 4 fases distintas de la onda de luz para codificar **2 bits por símbolo**. Ampliamente utilizado en sistemas coherentes de larga distancia por su alta tolerancia al ruido.
* **QAM (Quadrature Amplitude Modulation - ej. 16-QAM, 64-QAM):** Combina variaciones tanto de amplitud como de fase Al transmitir más bits por símbolo (4 bits en 16-QAM), incrementa masivamente la eficiencia espectral, requiriendo sistemas de recepción coherente y procesamiento digital de señales (DSP).

### Conversión Electro-Óptica
Es el proceso donde las señales eléctricas del dominio digital se transforman en fotones. Se puede realizar mediante:
1. **Modulación Directa (DML):** Se varía directamente la corriente de alimentación del diodo láser. Produce fluctuaciones de frecuencia (*chirp*), limitándolo a bajas distancias.
2. **Modulación Externa (EML / Mach-Zehnder):** El láser emite luz constante y un modulador externo (como el interferómetro Mach-Zehnder) interrumpe o desfasa la luz externamente. Evita el *chirp* y es el estándar para enlaces DWDM de larga distancia.

---

## 4. Estándares y Normativas Internacionales

El despliegue de maquetas y sistemas de producción DWDM se rige estrictamente por las siguientes recomendaciones de la Unión Internacional de Telecomunicaciones (ITU):

* **ITU-T G.694.1 (Grilla Espectral):** Define las cuadrículas de frecuencia para los sistemas DWDM fijos y flexibles[cite: 1], garantizando que todos los fabricantes utilicen las mismas frecuencias ópticas exactas.
* **ITU-T G.709 (Red de Transporte Óptico - OTN):** Define la estructura de tramas (vía contenedores digitales como ODUk, OTUk) para el transporte eficiente de múltiples servicios sobre DWDM. Introduce la corrección de errores hacia adelante (**FEC**), que permite recuperar datos degradados por el ruido de la línea sin retransmisión.
* **ITU-T G.652 (Fibra Monomodo Estándar - SMF):** Es la fibra más instalada globalmente. Tiene su punto de dispersión cromática cero cerca de los $1310\text{ nm}$. Al usarla en Banda C ($1550\text{ nm}$), presenta muy baja atenuación pero requiere compensación estricta de dispersión en enlaces largos.
* **ITU-T G.655 (Fibra NZ-DSF - Non-Zero Dispersion-Shifted Fiber):** Diseñada específicamente para sistemas WDM de larga distancia. Desplaza la dispersión cero fuera de la Banda C para mitigar los efectos no lineales dañinos como el Mezclado de Cuatro Ondas (FWM), manteniendo al mismo tiempo una dispersión controlada y baja atenuación.

---

## 5. Anexo Matemático y Físico

Para comprender los valores de espectro y atenuación mencionados anteriormente, es necesario aplicar principios físicos fundamentales de la luz electromagnética.

### Relación entre Frecuencia y Longitud de Onda
La relación matemática universal entre la frecuencia ($f$) y la longitud de onda ($\lambda$) está dada por la velocidad de la luz en el vacío ($c$):

$$c = \lambda \times f$$

Donde:
* **$c$** (Velocidad de la luz) = $299.792.458 \text{ m/s}$ (usualmente redondeado a $3 \times 10^8 \text{ m/s}$).
* **$f$** = Frecuencia medida en Hercios (Hz) o Terahercios (THz).
* **$\lambda$** = Longitud de onda medida en metros (m) o nanómetros (nm).

### ¿Por qué 193.1 THz equivale a 1552.52 nm?
El estándar ITU-T G.694.1 fija el "ancla" de la grilla DWDM en **193.1 THz**[cite: 1]. Si despejamos la longitud de onda ($\lambda = c / f$):
$$ \lambda = \frac{299.792.458 \text{ m/s}}{193.1 \times 10^{12} \text{ Hz}} \approx 1.55252 \times 10^{-6} \text{ metros} $$
Al convertir a nanómetros ($1 \text{ nm} = 10^{-9} \text{ m}$), obtenemos exactamente **1552.52 nm**, el centro de la Banda C.

### ¿De dónde sale que 100 GHz de separación es igual a 0.8 nm?
Aunque en DWDM solemos hablar de separación en "nanómetros" por costumbre, la luz se comporta de manera no lineal respecto a la frecuencia. Para calcular cuánto equivale un salto de **100 GHz** en nanómetros cerca de los 1550 nm, se usa la derivada de la ecuación de la luz:

$$ \Delta\lambda \approx \left( \frac{\lambda^2}{c} \right) \times \Delta f $$

Si reemplazamos $\lambda = 1550 \text{ nm}$, $c = 300.000 \text{ km/s}$ y $\Delta f = 100 \text{ GHz}$:
$$ \Delta\lambda \approx \left( \frac{1550^2}{300.000} \right) \times 100 \approx 0.8 \text{ nm} $$
Por esto, en la grilla de 100 GHz, los canales están separados por **$\sim 0.8 \text{ nm}$**, y en la de 50 GHz, por **$\sim 0.4 \text{ nm}$**.

### El origen de la atenuación de 0.2 dB/km en la Banda C
El valor de $\approx 0.2\text{ dB/km}$ no es un invento, es un límite físico del cristal de sílice (vidrio). Se forma por la intersección de dos fenómenos:
1. **Dispersión de Rayleigh:** Las partículas microscópicas en el vidrio desvían la luz. Este efecto es muy fuerte en longitudes de onda cortas (como 850 nm) pero disminuye drásticamente a medida que la longitud de onda crece.
2. **Absorción Infrarroja:** A partir de los 1600 nm, las propias moléculas químicas del vidrio comienzan a absorber la luz y convertirla en calor.
El "valle" exacto donde la Dispersión de Rayleigh ya bajó y la Absorción Infrarroja aún no sube, se encuentra exactamente entre los **1530 nm y 1565 nm** (La Banda C), permitiendo la pérdida teórica más baja posible en la fibra óptica.
