# Módulo 5: Datos y su Valor Estratégico en el ET

## Información del Módulo
* **Unidad:** U3 - Gestión de Datos y RAG
* **Duración estimada:** 2.5 horas
* **Modalidad:** Presencial (Taller práctico)

## Objetivos del Aprendizaje
1. Identificar la estructura y origen de los datos dentro de los Sistemas de Información de las FAS (ej. SIMACET, SIGLE).
2. Comprender la arquitectura de ingesta de datos ETL (Extract, Transform, Load) en un entorno de combate caracterizado por la pérdida de paquetes.
3. Operar herramientas técnicas de consolidación de datos para prepararlos para su consumo algorítmico y análisis en Puestos de Mando.

## Contenido Detallado Técnico

### 1. El Dato como Activo de Armas (Data Fabric Militar)
El volumen de información generado por una Brigada Mecanizada moderna supera la capacidad humana de análisis. La estrategia del "Data Fabric" consiste en federar y hacer interoperables todos los silos de información.
* **Mando y Control (C2):** Bases de datos relacionales y NoSQL provenientes del SIMACET (Sistema de Mando y Control del Ejército de Tierra) y del BMS (Battlefield Management System). Trazas de Blue Force Tracking (BFT), posiciones enemigas reportadas, planes de fuego y órdenes de operaciones (OPORD).
* **Logística y Mantenimiento:** Archivos procedentes del SIGLE (Sistema Integrado de Gestión Logística del Ejército). Registros de horas de funcionamiento, niveles de municionamiento por pieza, consumo de combustible diario y gestión de recambios.
* **Inteligencia (ISR):** Fuentes no estructuradas: Videos KLV de drones, interceptaciones de radio transcritas (SIGINT), reportes de patrullas (HUMINT) e imágenes satelitales multiespectrales (IMINT).

### 2. Pipeline de Datos en Operaciones (ETL Táctico)

La recolección de datos en la empresa civil asume conexiones estables. En Defensa, el Pipeline debe tolerar anchos de banda de Kilobits por segundo y alta latencia.

```mermaid
graph LR
    subgraph Edge (Nodos Tácticos Avanzados)
        A1[(BBDD Logística de Base)] 
        A2[Vehículo Dragón (BMS BFT)]
        A3[Reportes SITREP/HUMINT]
    end

    subgraph Data Pipeline (CECOM - Puesto de Mando)
        B1((Extracción y Descompresión Protobuf))
        B2[Limpieza y Normalización \n Deduplicación de Trazas Radar]
        B3((Carga en Data Lake))
        
        A1 -.->|Conexión Intermitente SATCOM| B1
        A2 -->|Radio VHF PR4G| B1
        A3 -->|Enlace Microondas HCLOS| B1
        B1 --> B2
        B2 --> B3
    end

    subgraph Consumo Algorítmico (CESADAR)
        C1[(Data Lake Unificado)]
        C2[Dashboard de Mando COP]
        C3[IA Predictiva (Mantenimiento/Bajas)]
        
        B3 --> C1
        C1 --> C2
        C1 --> C3
    end
```

### 3. Técnicas de Calidad del Dato (Data Quality) en Defensa
* **Protocol Buffers (Protobuf):** Uso de formatos de serialización binaria (como Protobuf o FlatBuffers) en lugar de JSON o XML para reducir el tamaño del payload de los datos que viajan por las radios tácticas en un 80%, evitando cuellos de botella.
* **Gobernanza y Ontologías (MIP):** El Multilateral Interoperability Programme (MIP) define un modelo de datos lógico compartido por la OTAN. Para que el dato sea útil a la IA, la etiqueta "Carro de Combate" debe estar mapeada a una ontología exacta compartida con los aliados, unificando formatos de fecha (Zulu Time) y coordenadas (MGRS).
* **Gestión del Ruido:** En operaciones de combate, un vehículo destruido puede seguir enviando su última posición conocida por la red, o un sensor sometido a *jamming* (interferencia electrónica) puede generar trazas "fantasma". Los algoritmos de limpieza deben identificar y purgar estos falsos positivos antes de que envenenen el COP.

## Actividades y Evaluación
* **Taller Práctico de Data Wrangling:** Mediante Python (Librerías Pandas y NumPy), los alumnos recibirán un volcado tabular de averías de la flota VAMTAC ST5 proveniente de tres bases distintas con graves errores de formato (fechas europeas mezcladas con americanas, descripciones en texto libre, coordenadas geodésicas mezcladas con UTM, campos nulos). Deberán programar un script robusto que limpie, consolide e ingeste esos datos en un formato estándar consumible por un algoritmo predictivo.
