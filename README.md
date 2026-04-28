# Resolución de Reto Técnico: Optimización de Rutas en Redes Financieras

Este repositorio contiene la solución técnica desarrollada para el proceso de selección de **Data Analytics & Scientist Jr.** El proyecto implementa un algoritmo de ruta mínima sobre un grafo dirigido ponderado, integrando la restricción de paso obligatorio por una conexión específica.

## 1. Caso de Negocio
Esta solución se enfoca en el **Análisis de Redes Financieras** para la detección de flujos sospechosos y auditoría de capital. Se utiliza la **Teoría de Grafos** para modelar las conexiones entre entidades donde cada arista representa una transacción con un costo/riesgo asociado.

El núcleo de la solución es el **Algoritmo de Dijkstra**, aplicado de forma segmentada para garantizar el paso por la arista crítica $(u, v)$:
* **Lógica:** Se calcula la ruta mínima $Origen \to u$ y la ruta $v \to Destino$. La unión de estas con la arista $(u, v)$ garantiza la ruta óptima bajo la restricción impuesta por el negocio.

## 2. Cómo Generar los Datos y Correr la Solución
El proyecto es autocontenido y reproducible:
1.  **Generación:** Al ejecutar la celda "3. Generación de Dataset Sintético" en el Notebook, se crea automáticamente un grafo con escenarios de éxito y error.
2.  **Ejecución:**
    * Abrir `Examen_Data_Analytics_Scientist_Jr_Francisco_Caballero.ipynb` en Google Colab o Jupyter.
    * Ejecutar todas las celdas (`Ctrl + F9` en Colab).
    * La última celda mostrará el resultado gráfico y la validación técnica.

## 3. Formato de Entradas y Salidas
* **Entradas:**
    * `Grafo (G)`: Objeto NetworkX o CSV con columnas `[Origen, Destino, Costo]`.
    * `Parámetros`: Nodo origen ($o$), nodo destino ($d$) y arista obligatoria ($u, v$).
* **Salidas:**
    * `Ruta`: Lista secuencial de nodos (ej. `['O', 'A', 'U', 'V', 'D']`).
    * `Costo Total`: Suma ponderada de los pesos de la ruta.
    * `Evidencia`: Validación booleana del cumplimiento de la restricción.

## 4. Log de Decisiones (Alternativas Consideradas)
* **Alternativa A: Algoritmo de Bruta Fuerza.** Descartado por su complejidad exponencial $O(N!)$, inviable para redes bancarias reales.
* **Alternativa B: Algoritmo de Bellman-Ford.** Se consideró por su capacidad de manejar pesos negativos, pero se eligió **Dijkstra** por su superioridad en tiempo de ejecución ($O(E + V \log V)$) dado que los riesgos financieros suelen ser positivos.
* **Decisión Final:** Se optó por una implementación modular en Python (NetworkX) por su balance entre legibilidad para auditoría y eficiencia computacional.

## 5. Supuestos y Limitaciones
* **Pesos:** Se asumen valores no negativos (comisiones, riesgo o tiempo).
* **Escalabilidad:** Para miles de millones de registros, se sugiere migrar a **Apache Spark (GraphFrames)**.
* **Fragilidad:** El modelo es sensible a cambios en los pesos en tiempo real si no se cuenta con un pipeline de datos dinámico.

## 6. Casos de Prueba Incluidos
* **Escenario Normal:** Existe una ruta válida que pasa por la arista.
* **Caso Borde (Sin Solución):** El punto de riesgo es inalcanzable desde el origen.
* **Caso Borde (Validación):** Una ruta global más corta existe pero no pasa por la arista; el algoritmo la ignora para cumplir la restricción.

---
**Candidato:** Francisco Javier Caballero Garcia  
**Perfil:** Data Analytics & Scientist | Especialista en Procesos de Datos
