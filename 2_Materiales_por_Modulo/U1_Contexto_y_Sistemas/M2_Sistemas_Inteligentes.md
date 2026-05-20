# Módulo 2: Visión General de los Sistemas Inteligentes y Sensores Tácticos

## Información del Módulo
* **Unidad:** U1 - Contexto y Sistemas
* **Duración estimada:** 2.5 horas
* **Modalidad:** Presencial

## Objetivos del Aprendizaje
1. Diferenciar la IA Estrecha de conceptos teóricos y evaluar su rendimiento real en hardware militar TRL 8-9 (Technology Readiness Level).
2. Identificar la topología de red y los componentes físicos de un sistema inteligente táctico (Sensores, TPUs, Actuadores).
3. Comprender el flujo sensórico en el ecosistema de la Brigada (vehículos blindados, UAVs, soldados desembarcados con ATAK).

## Contenido Detallado Técnico

### 1. Hardware y Arquitectura de Inferencia en el Nivel Táctico
Para que un algoritmo de Machine Learning sea operativo en zona de conflicto, debe abandonar los grandes centros de datos refrigerados y ejecutarse en hardware rugerizado (MIL-STD-810G).

* **El "Cerebro" Táctico (TPUs y SoCs):** 
  * Uso de Sistemas en Chip (SoC) como la línea **NVIDIA Jetson AGX Orin**, que proporcionan cientos de TOPS (Tera Operations Per Second) con un consumo eléctrico inferior a 60 W. Estos módulos se integran en ordenadores de misión dentro de blindados (ej. plataformas de Indra o GMV) para procesar inferencias de redes neuronales localmente.
* **Sensores (El "Ojo" y el "Oído"):** 
  * **Electro-Ópticos / Térmicos (EO/IR):** Torres SERT (Sistema de Exploración y Reconocimiento Terrestre). Generan terabytes de video no comprimido.
  * **Radares de Apertura Sintética (SAR):** Que permiten cartografía e identificación de blancos a través de nubes y humo.
  * **UGS (Unattended Ground Sensors):** Nodos sísmicos y acústicos que detectan pisadas o vibraciones de cadenas de tanques.
* **Actuadores (La Acción Física):**
  * Estaciones de Armas Remotamente Controladas (RCWS) como la Guardian 2.0 o la Mini-Samson. La IA puede pre-orientar el arma e incluso realizar el *tracking* (seguimiento del blanco en movimiento), pero la doctrina occidental exige un pulsador manual para el fuego.

### 2. Esquema Funcional: El Motor de Automatic Target Recognition (ATR)

El siguiente diagrama detalla cómo un flujo de video se convierte en una decisión de combate mediante un modelo de visión artificial y telemetría de plataforma.

```mermaid
flowchart TD
    subgraph Capa de Adquisición de Datos
        A1(Cámara IR) -->|Video Bruto| B1{Frame Grabber / FPGA}
        A2(Unidad Inercial IMU) -->|Pitch/Roll/Yaw| B1
        A3(Telémetro Láser) -->|Distancia al pixel| B1
    end
    
    subgraph Capa de IA Edge (Hardware Rugerizado)
        B1 -->|Frames Normalizados| C1[Pre-procesamiento: \nMejora de Contraste]
        C1 --> C2[Inferencia CNN: YOLOv8-Mil \n Detección de Bounding Boxes]
        C2 --> C3[Clasificador Secundario: \n Identificación IFF / Modelo de Vehículo]
        A2 --> C4[Proyección Geoespacial]
        C3 --> C4
    end
    
    subgraph Capa C2 e Interfaz (Human-in-the-Loop)
        C4 -->|Objeto: T-72 \n Coordenadas: 30T 456 432| D1(Interfaz BMS-ET)
        D1 -->|Alarma Visual| D2[Jefe de Vehículo]
        D2 -.->|Aprueba Enganche| D3((Sistema de Armas RCWS))
    end
```

### 3. Del Sensor al Tirador (Sensor-to-Shooter Loop) y Retos
* **Filtros de Kalman y SLAM:** Los sistemas inteligentes no solo reconocen amenazas. En los Vehículos Terrestres No Tripulados (UGV) como el MUTT o el THeMIS, se utiliza *Simultaneous Localization and Mapping* (SLAM) fusionando LIDAR y odometría visual para navegar de forma autónoma en entornos donde el GPS ha sido interferido por guerra electrónica (GNSS Spoofing/Jamming).
* **Sobrecarga Cognitiva (Cognitive Overload):** El riesgo de que la IA genere un exceso de "falsos positivos" (identificar un tractor como un blindado), obligando al operador a silenciar el sistema. La métrica clave en defensa no es solo la "precisión" (Accuracy), sino la minimización de *False Alarm Rates* (FAR).

## Actividades y Evaluación
* **Dimensionamiento de Enjambre (Swarming):** Diseñar sobre plano la arquitectura técnica para un enjambre de 5 micro-UAVs apoyando a un convoy logístico en el Sahel. Los alumnos deberán establecer qué UAV actúa como nodo de cómputo maestro (IA), cómo fusionan sus cámaras térmicas, y cómo transmiten la alerta de IEDs (Artefactos Explosivos Improvisados) al vehículo de cabeza utilizando la red ATAK (Android Tactical Assault Kit).
