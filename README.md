# Mapeo de coberturas y usos de la tierra - Imbabura 2019

![](/images/logos.png)

## Introducción

El objetivo general de la colaboración entre SERVIR-Amazonia y el GAD (Gobierno Autónomo Descentralizado Provincial) de Imbabura es mejorar las capacidades existentes para medir y monitorear la cobertura y uso del suelo en Ecuador con énfasis en la región amazónica para la gestión y gobernanza forestal, incluyendo el contexto de planificación forestal y de uso del suelo y actividades relacionadas.

Debido a la persistente nubosidad sobre la región, hemos acordado producir un mapa piloto de Cobertura y Uso del Suelo de la provincia de Imbabura para el año 2019, utilizando datos satelitales ópticos y de radar, con las clases de cubiertas y uso abajo.

![](/images/propuesta.png)

## Google Earth Engine (GEE) set-up

Necesitas una cuenta en [Google Earth Engine](https://earthengine.google.com/). Para agencias de gobierno o instituiciones academicas, accessa a [https://earthengine.google.com/noncommercial/](https://earthengine.google.com/noncommercial/) para más informaciones.

Después de tener su cuenta creada, usuarios pueden, se desean, utilizar GEE sin crear un proyecto en la Cloud: [https://code.earthengine.google.com/register](https://code.earthengine.google.com/register) - opción "Noncommercial users can also use Earth Engine without creating Cloud projects. Click here for the signup form."

## Metodología

El flujo de trabajo está abajo:

![](/images/imbabura-workflow.png)

### Generación de datos de entrada

Actualmente, el modelo utiliza tres tipos de datos diferentes:
- Imágenes satelitales ópticas
  - Sentinel-2
  - Planet NICFI
- Imágenes satelitales de radar (SAR)
  - Sentinel-1
- Datos de elevación
  - MAG SIGTIERRAS DTMs locales
  - NASA SRTM

#### Datos de elevación

Datos locales disponibles de la provincia por el proyecto SIGTIERRAS del MAG es utilizado. Como algunas áreas no tienen información, utilizamos datos del SRTM para complementar.

![](/images/elevacion.png)

#### Planet NICFI

Necesitas acceso a la colleción NICFI en GEE. Puedes registrarse siguiendo instrucciones en: https://developers.planet.com/docs/integrations/gee/nicfi/.
Mosaicos mensuales de 2019 son agregados en una composición mediana.

#### Sentinel-1

Se utilizan los datos Sentinel-1 GRD de Earth Engine de la ESA. Aplicamos una Normalización del Terreno basada en Vollrath, et al., 2020 & Hoekman & Reich, 2015 a través del código disponible en https://github.com/adugnag/gee_s1_ard. El MDE utilizado para la normalización del terreno es la combinación de datos SRTM y datos MDT locales, descritos arriba. Utilizamos datos de las dos direcciones (Ascending y Descending) y la série temporal en datos lineares. Un filtro multitemporal GAMMA MAP con kernel 7x7 es aplicado a cada imagén para remoción del moteado Se crea una mediana compuesta para 2019 utilizando todos los datos disponibles de este año.

#### Sentinel-2

Utilizamos el producto de Google [Cloud Score+](https://developers.google.com/earth-engine/datasets/catalog/GOOGLE_CLOUD_SCORE_PLUS_V1_S2_HARMONIZED), para la generación de una composición mediana de 2019. Utilizamos la banda `cs` con un umbral de 0.4. 

### Modelo de clasificación

Puntos de referencia extraedos de un producto de 2020 del MAG fueron utilizados para entrenar un classifier Random Forest con 100 árboles de decisiones. 7.000 puntos de cada clase de cobierta y uso de la tierra fueron utilizados, totalizando 63.000 puntos.

## Resultados y app

La clasificación final puede ser visualizados en la aplicación [https://servir-amazonia.earthengine.app/view/cob-imbabura](https://servir-amazonia.earthengine.app/view/cob-imbabura).
Una validación del mapa independente va a ser brindada en 2024.

Una aplicación para comparación con otros mapas disponibles (MAATE y MAG) está disponible en [https://servir-amazonia.earthengine.app/view/cob-imbabura-comp](https://servir-amazonia.earthengine.app/view/cob-imbabura-comp). Los diferentes productos deben ser utilizados de manera complementar. 

## Recursos

Diapositivas presentadas durante el enlazamiento del mapa [aquí](https://docs.google.com/presentation/d/1ewmdR0mngd1_x-9k-iCD84fwyrBS9_0h/edit?usp=sharing&ouid=117588040825190888554&rtpof=true&sd=true) y grabación del evento [aquí](https://www.facebook.com/PrefecturaImbabura/videos/882536243471435/).

Estaremos compartindo los scripts en la API Python futuramente....
