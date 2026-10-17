# Applications of AI for Anomaly Detection (NVIDIA DLI)

Repositorio de estudio del taller **Applications of AI for Anomaly Detection** del NVIDIA Deep
Learning Institute, que completé en octubre de 2026.

**Certificado:** Certificate of Competency, emitido el 1 de octubre de 2026.
Verificación pública: <https://learn.nvidia.com/certificates?id=v3swaJAnQFCW2ZW2OgkQJQ>
(copia en [`certificado/`](certificado/)).

---

## De qué trata el taller

El problema de fondo es detectar comportamiento anómalo en tráfico de red, usando el dataset de
intrusiones **KDD Cup 99**: unos 18 millones de registros, con 22 variables numéricas y 9
categóricas. El taller recorre tres situaciones distintas según lo que uno sabe de los datos:

| Laboratorio | Situación | Técnica | Idea central |
|---|---|---|---|
| 1 | Hay etiquetas | **XGBoost acelerado por GPU** (RAPIDS) | Árboles de gradiente que se construyen uno tras otro, cada uno corrigiendo los errores del anterior. Clasificación binaria y luego multiclase. |
| 2 | No hay etiquetas | **Autoencoder** | Se entrena solo para reconstruir datos normales; un registro que se reconstruye mal (error alto) es sospechoso. Las variables categóricas entran con embeddings en vez de one-hot. |
| 3 | No se sabe cómo se ven las anomalías, o los datos no son gaussianos | **GAN** | El generador aprende a imitar los datos normales y el discriminador termina sirviendo como detector: asigna baja probabilidad a lo que no se parece a lo normal. |
| Evaluación | Dataset nuevo | Una de las tres técnicas | Aplicar el método y elegir el umbral de decisión. |

Las tres se comparan con la **curva ROC y el AUC**, y con la elección del umbral según el
porcentaje de anomalías que se espera encontrar.

## Lo que me llevo

- **El tipo de etiqueta decide el método.** Con etiquetas, un modelo supervisado como XGBoost suele
  ganar. Sin ellas, el autoencoder convierte el problema en medir qué tan "normal" es cada registro.
- **El umbral es una decisión de negocio**, no un detalle técnico. Moverlo cambia el balance entre
  falsos positivos y anomalías que se escapan, y eso se ve directo en la curva ROC.
- **Acelerar en GPU cambia la forma de trabajar.** Con RAPIDS y XGBoost en GPU se pueden probar
  muchas más configuraciones en el mismo tiempo, que es lo que más pesa en la etapa de ajuste.
- **Las variables categóricas importan.** Pasar de one-hot a embeddings cambia lo que el modelo
  puede aprender de ellas.

Este taller conecta con lo que hago en validación de modelos (AUC, umbrales, calibración) y con mi
interés en el cómputo de alto rendimiento aplicado a la IA.

## Contenido del repositorio

| Ruta | Qué es |
|---|---|
| `Lab1-...XGBoost.ipynb` | Laboratorio 1: XGBoost acelerado por GPU |
| `Lab2-...Autoencoders.ipynb` | Laboratorio 2: autoencoders |
| `Lab3-...GANS.ipynb` | Laboratorio 3: GANs |
| `Assessment.ipynb` | Evaluación final del taller |
| `Lab*-preprocess_data.py` | Preprocesamiento del KDD Cup 99 |
| `Lab*-Presentation.pptx`, `Assessment-Presentation.pptx` | Presentaciones del curso |
| `materiales_taller_2026/` | Versión de la presentación del laboratorio 1 que se usó en mi edición del taller (44 diapositivas) |
| `certificado/` | Mi certificado en PDF |
| `data.tar.gz` | Datos del taller |
| `images/` | Figuras usadas en los notebooks |
| `docs/README_original_HROlive.md` | README del repositorio de origen |

> Los notebooks ejecutados provienen del repositorio de origen (ver Créditos). Los laboratorios del
> DLI corren en la plataforma de NVIDIA, así que mi propia ejecución quedó allí y no está aquí.

## Créditos y uso

- El material del curso (notebooks, presentaciones, datos preparados e imágenes) es del **NVIDIA
  Deep Learning Institute**.
- La base de este repositorio es
  [HROlive/Applications-of-AI-for-Anomaly-Detection](https://github.com/HROlive/Applications-of-AI-for-Anomaly-Detection),
  cuyo historial se conserva aquí.
- Por eso este repositorio es **privado** y de uso personal de estudio. Lo propio es el
  certificado, la presentación de mi edición y este README.

---

Natalia Remolina · [github.com/NatoRemolina](https://github.com/NatoRemolina)
