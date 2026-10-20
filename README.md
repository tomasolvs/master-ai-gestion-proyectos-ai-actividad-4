# Actividad 4 — Comparación de modelos de sentimiento

* Nombre: Tomás Olivares
* Nombre del curso: Gestión de proyectos de inteligencia artificial
* Nombre del profesor: Luis Ariel Vázquez Piña
* Módulo: 2 - Semana: 5
* Fecha:  19/10/2026
* Actividad 4: Prototipo de clasificación de reseñas por medio de NLP

## Caso de uso
Prototipo para clasificar reseñas de restaurantes en español como positivas (POS), neutrales (NEU) o negativas (NEG), comparando tres modelos preentrenados de Hugging Face.

## Estructura
- `notebooks/Actividad4_Comparacion_Modelos_Sentimiento.ipynb`: notebook para Google Colab.
- `data/resenas_restaurante.csv`: dataset de 90 reseñas sintéticas balanceadas.
- `src/generar_dataset.py`: script reproducible que genera el CSV.
- `results/`: carpeta destinada a los resultados exportados al ejecutar el notebook.
- `docs/analisis_comparativo.docx`: reporte técnico.
- `requirements.txt`: dependencias.

## Dataset y limitaciones
Los 90 ejemplos fueron redactados para esta actividad y son sintéticos; no proceden de reseñas reales ni contienen datos personales. El conjunto está balanceado (30 por clase) para comprobar el flujo de evaluación. No debe interpretarse como benchmark de producción ni como evidencia de generalización. Para una decisión real se necesita una muestra más amplia y representativa, con etiquetas verificadas por personas.

Campos:
- `id`: identificador secuencial.
- `texto`: reseña en español.
- `etiqueta`: POS, NEU o NEG.
- `etiqueta_nombre`: etiqueta legible en español.

## Modelos evaluados
1. `pysentimiento/robertuito-sentiment-analysis`
2. `lxyuan/distilbert-base-multilingual-cased-sentiments-student`
3. `cardiffnlp/twitter-xlm-roberta-base-sentiment`

Las métricas (accuracy, precision macro, recall macro, F1 macro) y latencias se calculan al ejecutar el notebook. No se reportan cifras previas inventadas. Las licencias y condiciones deben confirmarse en cada model card antes de redistribuir o usar comercialmente.

## Ejecutar en Google Colab
1. Abrir el notebook en Colab.
2. Seleccionar `Entorno de ejecución > Cambiar tipo de entorno de ejecución > GPU`.
3. Subir `data/resenas_restaurante.csv` cuando lo solicite la celda de carga, o colocar el CSV en el directorio de trabajo.
4. Ejecutar las celdas en orden.
5. (Opcional) añadir `HF_TOKEN` en Colab Secrets. Los modelos públicos suelen descargarse sin token.
6. Revisar tablas, matrices de confusión y conclusiones generadas.

## Reproducir el dataset
Desde la raíz del proyecto:
```bash
python src/generar_dataset.py
```

## Umbrales propuestos
Como objetivos iniciales de prototipo, se proponen F1 macro >= 0.80 y latencia media <= 250 ms/reseña en el hardware documentado. Son umbrales de diseño, no resultados observados. Si no se cumplen, no se debe presentar un modelo como listo para producción.

## Conclusiones
La selección debe equilibrar desempeño por clase, latencia, costo de recursos, dominio de entrenamiento y licencia. Una recomendación para producción requiere validar con reseñas reales y representativas, revisar errores y documentar el entorno exacto.
