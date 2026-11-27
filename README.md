# Predicción de la terminación anticipada de estudios clínicos registrados en ClinicalTrials.gov: replicación y mejora de un modelo de referencia

Proyecto final de **Minería de Datos**, Licenciatura en Ciencia de Datos

**Autores:**

- Cruz Gutiérrez Edgar Omar
- Martínez Muñoz Alan Magno
- Munive Ramírez Ibrahim

---

## Resumen

Un estudio clínico que termina antes de lo previsto puede exponer a sus participantes a intervenciones sin alcanzar el tamaño de muestra necesario, y consume recursos de patrocinadores, centros de investigación y comités de ética. Este proyecto replica el modelo de Elkin y Zhu (2021) sobre datos de ClinicalTrials.gov y busca superar su desempeño, además de predecir la terminación por bajo reclutamiento.

## Preguntas de minería de datos

**Pregunta principal:** ¿con qué desempeño puede predecirse, a partir de la información registrada en ClinicalTrials.gov, que un estudio clínico terminará anticipadamente, y en qué medida supera ese desempeño al reportado por Elkin y Zhu (2021)?

**Pregunta específica:** ¿con qué desempeño puede predecirse la terminación anticipada por bajo reclutamiento?

Se trata de un problema de aprendizaje supervisado de clasificación binaria, con tres análisis:

1. **Análisis 1 (comparación directa):** reproducción del método de referencia (M0) frente al modelo propuesto (M1) sobre la misma cohorte y las mismas particiones.
2. **Análisis 2:** la etiqueta de terminación se sustituye por la terminación debida a bajo reclutamiento.
3. **Análisis 3:** evaluación con partición temporal y un conjunto de variables libre de fuga de información.

## Fuente de datos

La fuente principal es **AACT (Aggregate Analysis of ClinicalTrials.gov)**, una base de datos relacional en PostgreSQL que mantiene la Clinical Trials Transformation Initiative (CTTI). Contiene la totalidad de los registros de ClinicalTrials.gov, se actualiza diariamente y es de acceso gratuito con una cuenta de usuario.

## Flujo de trabajo

El proyecto sigue las seis fases de CRISP-DM.

1. **Comprensión del negocio:** objetivos, criterio de éxito (lift $\geq 2.0$ en el $20 \%$ superior) y plan del proyecto.
2. **Comprensión de los datos:** extracción de AACT a una capa bronce en Parquet, descripción de tablas, exploración con cubo OLAP y verificación de calidad.

3. **Preparación de los datos:** selección de la cohorte de replicación, limpieza, construcción de las variables, integración y etiquetado del motivo de terminación.

4. **Modelado:** reproducción de M0 (red neuronal, bosque aleatorio, XGBoost y regresión logística con submuestreo) y construcción de M1 (XGBoost con aprendizaje sensible al costo y representaciones de texto con PubMedBERT).

5. **Evaluación:** validación cruzada estratificada 5 $\times$ 5, prueba t corregida de Nadeau y Bengio, intervalos bootstrap en el Análisis 3 e interpretación con SHAP.

6. **Despliegue:** repositorio público, bitácora de calidad de datos, módulo de predicción y artículo con exposición.

Q.E.D.