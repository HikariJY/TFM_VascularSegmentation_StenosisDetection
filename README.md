# **TFM_VascularSegmentation_StenosisDetection**
**TFM VIU Catagua Cobos Josseph Yaakob**


## **DATASETS**

### ARCADE

Recuperado en [KAGGLE - ARCADE](https://www.kaggle.com/datasets/gongiahmed/arcade-x-ray-angiography-images) con imágenes de angiografía y sus respectivas anotaciones al estilo COCO para la segmentación vascular y detección de estenosis.

<table>
  <tr>
    <td align="center">
      <img src="readme_resources/ARCADE_stenosis.png" alt="Imagen 1" width="250">
      <br>
      Imagen 1. ARCADE-Estenosis
    </td>
    <td align="center">
      <img src="readme_resources/ARCADE_syntax.png" alt="Imagen 2" width="250">
      <br>
      Imagen 2. ARCADE-Sintaxis
    </td>
  </tr>
</table>

```plaintext
📂 **ARCADE**
│── 📂 **stenosis**
│   ├── 📄 data.yaml
│   ├── 📂 **test**
│   │   ├── 📄 labels.cache
│   │   ├── 📂 annotations (1) → test.json
│   │   ├── 📂 images (300) → _Ejemplos_: 1.png, 10.png, 100.png...
│   │   └── 📂 labels (300) → _Ejemplos_: 1.txt, 10.txt, 100.txt...
│   ├── 📂 **train**
│   │   ├── 📄 labels.cache
│   │   ├── 📂 annotations (1) → train.json
│   │   ├── 📂 images (1000) → _Ejemplos_: 1.png, 10.png, 100.png...
│   │   └── 📂 labels (997) → _Ejemplos_: 1.txt, 10.txt, 100.txt...
│   └── 📂 **val**
│       ├── 📄 labels.cache
│       ├── 📂 annotations (1) → val.json
│       ├── 📂 images (200) → _Ejemplos_: 1.png, 10.png, 100.png...
│       └── 📂 labels (200) → _Ejemplos_: 1.txt, 10.txt, 100.txt...
│
│── 📂 **syntax**
    ├── 📄 data.yaml
    ├── 📂 **test**
    │   ├── 📄 labels.cache
    │   ├── 📂 annotations (1) → test.json
    │   ├── 📂 images (300) → _Ejemplos_: 1.png, 10.png, 100.png...
    │   └── 📂 labels (300) → _Ejemplos_: 1.txt, 10.txt, 100.txt...
    ├── 📂 **train**
    │   ├── 📄 labels.cache
    │   ├── 📂 annotations (1) → train.json
    │   ├── 📂 images (1000) → _Ejemplos_: 1.png, 10.png, 100.png...
    │   └── 📂 labels (1000) → _Ejemplos_: 1.txt, 10.txt, 100.txt...
    └── 📂 **val**
        ├── 📄 labels.cache
        ├── 📂 annotations (1) → val.json
        ├── 📂 images (200) → _Ejemplos_: 1.png, 10.png, 100.png...
        └── 📂 labels (200) → _Ejemplos_: 1.txt, 10.txt, 100.txt...
```

### Database X-ray Coronary Angiograms

Recuperado en [KAGGLE - DCA1](https://www.kaggle.com/datasets/bard2024/database-x-ray-coronary-angiograms-dca1?select=Database_134_Angiograms) con imágenes de angiografía y sus respectivas máscaras de segmentación.

<table>
  <tr>
    <td align="center">
      <img src="readme_resources/DCA1_angiography.png" alt="Imagen 3" width="250">
      <br>
      Imagen 3. DCA1-Angiografía
    </td>
    <td align="center">
      <img src="readme_resources/DCA1_mask.png" alt="Imagen 4" width="250">
      <br>
      Imagen 4. DCA1-Máscara
    </td>
  </tr>
</table>

```plaintext
📂 **DCA1**
└── Archivos (268): _Ejemplos_: 1.pgm, 10.pgm, 100.pgm, 100_gt.pgm, 101.pgm
```

## **GENERACIÓN DE DATOS**

Se usaron las anotaciones del dataset ARCADE para generar las máscaras de segmentación:

<table>
  <tr>
    <td align="center">
      <img src="readme_resources/ARCADE_stenosis_masks.png" alt="Imagen 5" width="250">
      <br>
      Imagen 5. ARCADE-Stenosis-Generación de máscaras
    </td>
    <td align="center">
      <img src="readme_resources/ARCADE_syntax_masks.png" alt="Imagen 6" width="250">
      <br>
      Imagen 6. ARCADE-Syntax-Generación de máscaras
    </td>
  </tr>
</table>

## **ESTUDIO DE PREPROCESAMIENTO**

Se aplicaron varios filtros de imagen, para observar cuál influye más en la segmentación vascular y la detección de estenosis:

<table>
  <tr>
    <td align="center">
      <img src="readme_resources/ARCADE_segmentation_filters.png" alt="Imagen 7" height="75">
      <br>
      Imagen 7. ARCADE-Segmentación-Filtros aplicados
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="readme_resources/ARCADE_detection_filters.png" alt="Imagen 8" height="75">
      <br>
      Imagen 8. ARCADE-Detección-Filtros aplicados
    </td>
  </tr>
</table>

Luego se aplicó un estudio por matriz de correlación con un umbral de 0.9 o 90% máximo de correlación entre filtros:

<table>
  <tr>
    <td align="center">
        Matriz de correlación
    </td>
    <td align="center">
        Filtros descartados
    </td>
    <td align="center">
        Filtros no descartados
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="readme_resources/ARCADE_segmentation_matrix.png" alt="Imagen 9" weight="250">
      <br>
      Imagen 9. ARCADE-Segmentación-Matriz de correlación entre filtros
    </td>
    <td align="left">
        - CLAHE <br>
        - Desenfoque de mediana <br>
        - Ecualización por histograma <br>
        - Realce de bordes <br>
        - Sobel <br>
        - Unsharp Masking <br>
    </td>
    <td align="left">
        - Bilateral <br>
        - Desenfoque Gaussiano <br>
        - Estandarización Z-Score <br>
        - Normalización <br>
        - Promedio <br>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="readme_resources/ARCADE_detection_matrix.png" alt="Imagen 10" weight="250">
      <br>
      Imagen 10. ARCADE-Detección-Matriz de correlación entre filtros
    </td>
    <td align="left">
        - CLAHE <br>
        - Desenfoque de mediana <br>
        - Ecualización por histograma <br>
        - Realce de bordes <br>
        - Sobel <br>
        - Unsharp Masking <br>
    </td>
    <td align="left">
        - Bilateral <br>
        - Desenfoque Gaussiano <br>
        - Estandarización Z-Score <br>
        - Normalización <br>
        - Promedio <br>
    </td>
  </tr>
</table>

Por último se aplicó un estudio de caja y bigote por relación entre clase y filtro con un umbral de 0.05, aunque ninguno fue descartado, ayudó a verificar que pueden dar información suficiente para clasificarlo entre región con interés y fondo.

<table>
  <tr>
    <td align="center">
      <img src="readme_resources/ARCADE_segmentation_boxplot.png" alt="Imagen 11" weight="250">
      <br>
      Imagen 11. ARCADE-Segmentación-Caja y bigotes
    </td>
    <td align="center">
      <img src="readme_resources/ARCADE_detection_boxplot.png" alt="Imagen 12" weight="250">
      <br>
      Imagen 12. ARCADE-Detección-Caja y bigotes
    </td>
  </tr>
</table>

## **SEGMENTACIÓN VASCULAR**

