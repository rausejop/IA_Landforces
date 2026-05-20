# Módulo 1: Introducción a la IA y Contexto Estratégico (Ejército de Tierra)

## Información del Módulo
* **Unidad:** U1 - Contexto y Sistemas
* **Duración estimada:** 2.5 horas
* **Modalidad:** Presencial

## Objetivos del Aprendizaje
1. Comprender la evolución técnica de la IA y su encaje en la doctrina del Ejército de Tierra y la Alianza Atlántica (Fuerza 35, JADC2).
2. Identificar la transformación del Sistema de Mando y Control (C2) terrestre hacia un modelo de Operaciones Multi-Dominio (MDO).
3. Evaluar de forma crítica el impacto de la IA en programas de adquisición reales como el VCR 8x8 Dragón, el Sistema TALOS y plataformas ISR (Intelligence, Surveillance, and Reconnaissance).

## Contenido Detallado Técnico

### 1. La IA en el Horizonte Estratégico: Fuerza 2035 y MDO
El Plan de Experimentación "Fuerza 35" del Ejército de Tierra español plantea un escenario operativo caracterizado por la letalidad, la hiperconectividad y la saturación de información. En este contexto, la superioridad en el enfrentamiento no se basa únicamente en el calibre del arma, sino en la velocidad de la red C2.

* **Del Dato a la Decisión (Project Maven a BMS-ET):** El punto de inflexión moderno de la IA militar fue el Proyecto Maven (EE.UU.), que automatizó el análisis de horas de video de drones utilizando redes neuronales. En el Ejército de Tierra, el objetivo equivalente es la integración algorítmica en el **BMS-ET (Battlefield Management System)**, pasando de un sistema que simplemente posiciona iconos en un mapa (Blue Force Tracking) a un motor de recomendación táctica.
* **JADC2 (Joint All-Domain Command and Control):** Doctrina aliada que busca conectar "cada sensor con cada tirador". La IA es el único habilitador tecnológico capaz de fusionar datos estructurados (coordenadas radar) y no estructurados (reportes de HUMINT) en tiempo real, priorizando blancos para la Artillería de Campaña o el Apoyo Aéreo Cercano (CAS).

### 2. Arquitectura de Transformación C2 (Diagrama de Red Táctica)

El siguiente esquema ilustra la transición de un ciclo de reporte basado en la transmisión de voz (altamente susceptible al error humano y a la latencia) hacia un ciclo algorítmico federado.

```mermaid
graph TD
    subgraph "Doctrina Tradicional (C2 Estático y Jerárquico)"
        A1[Observador Avanzado OAV] -- "Malla Radio Voz (VHF)" --> B1[Centro de Dirección de Fuegos FDC]
        B1 -- "Cálculo Manual/Balístico" --> C1[Batería de Artillería]
        C1 -- "Disparo" --> D1[Impacto con Latencia Alta]
    end

    subgraph "Doctrina Aumentada por IA (Fuerza 35 / JADC2)"
        A2[Micro UAV Raven / Fulmar] -- "Video Digital + Metadatos KLV" --> B2(Nodo Edge AI en VCR Dragón)
        C2[Radar ARTHUR] -- "Trazas Digitales JREAP" --> B2
        B2 -- "Inferencia: Reconocimiento Automático de Blancos (ATR)" --> D2{Motor IA de Priorización}
        D2 -- "Asignación Óptima de Efector (SISTAC/TALOS)" --> E2[Pieza ATP M109A5 o HIMARS]
        D2 -- "Actualización COP" --> F2[Puesto de Mando (PC Desplegable)]
        E2 -- "Fuego Inmediato" --> G2[Impacto con Latencia Mínima]
    end
    
    style B2 fill:#2c3e50,stroke:#e74c3c,stroke-width:2px,color:#fff
    style D2 fill:#8e44ad,stroke:#9b59b6,stroke-width:2px,color:#fff
```

### 3. Ejemplos Reales de Aplicación en el Ejército de Tierra
1. **Inteligencia, Reconocimiento y Adquisición de Objetivos (ISTAR):**
   * **Visión Artificial (Computer Vision):** Despliegue de modelos CNN (Convolutional Neural Networks) como YOLOv8 u Object-DETR sobre flujos de video EO/IR (Electro-Óptico / Infrarrojo). El sistema es capaz de distinguir un Carro de Combate T-90 de un BMP-3 camuflado bajo redes térmicas, calculando sus coordenadas absolutas cruzando la orientación del PTZ de la cámara con el telémetro láser.
2. **Logística Predictiva en el PCMASA (Parque y Centro de Mantenimiento):**
   * Transición del mantenimiento correctivo (reparar cuando se rompe) al **predictivo**. Sensores del bus CAN (Controller Area Network) de la flota Leopardo 2E y VCR 8x8 envían telemetría continua (temperatura de aceite, vibración del tren de rodaje). Modelos de regresión de series temporales (ej. LSTM - Long Short-Term Memory) predicen el fallo de un componente con semanas de antelación, optimizando el *Supply Chain* en la zona de operaciones.
3. **Soporte de Fuego (Sistema TALOS):**
   * Integración de algoritmos heurísticos para la asignación "Sensor-Shooter". Si se detectan 50 blancos simultáneos, la IA evalúa cuál es la amenaza más crítica basándose en la distancia, el tipo de unidad y el vector de movimiento, recomendando a qué batería de artillería asignar el fuego basándose en la disponibilidad de munición y estado de las piezas.

## Actividades y Evaluación
* **Análisis de Sistema Táctico (Estudio de Caso VCR):** Los alumnos diseccionarán un escenario donde el Sistema de Combate del VCR 8x8 Dragón detecta un equipo contracarro (ATGM) enemigo en zona boscosa. Deberán definir qué procesos de ese ciclo (Detección térmica, Extracción de Coordenadas, Clasificación de Amenaza) son ejecutados por la IA Edge y en qué punto exacto interviene el Jefe de Vehículo para autorizar la acción letal (*Human-in-the-loop*).
