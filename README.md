# Mapeo de coberturas y usos de la tierra - Imbabura 2019

🚧Instrucciones en construcción 👷‍♀️

## Introducción

El objetivo general de la colaboración entre SERVIR-Amazonia y el GAD (Gobierno Autónomo Descentralizado Provincial) de Imbabura es mejorar las capacidades existentes para medir y monitorear la cobertura y uso del suelo en Ecuador con énfasis en la región amazónica para la gestión y gobernanza forestal, incluyendo el contexto de planificación forestal y de uso del suelo y actividades relacionadas.
Debido a la persistente nubosidad sobre la región, hemos acordado producir un mapa piloto de Cobertura y Uso del Suelo de la provincia de Imbabura para el año 2019, utilizando datos satelitales ópticos y de radar.

## Metodología



### Input data generation

Currently, the model uses three different types of data:
- Optical satellite imagery
  - Sentinel-2
  - Planet NICFI
- SAR satellite imagery
  - Sentinel-1
- Elevation data
  - MAG SIGTIERRAS DTMs locales
  - NASA SRTM

#### Sentinel-1

ESA's Sentinel-1 GRD data from Earth Engine is used. We apply a Terrain Normalization based on Vollrath, et al., 2020 &  Hoekman & Reich, 2015. A median composite was created for 2019 using all available data from this year.

#### Sentinel-2



#### Planet NICFI

Necesitas acceso a la colleción NICFI en GEE. Puedes registrarse siguiendo instrucciones en: https://developers.planet.com/docs/integrations/gee/nicfi/

#### Elevation data
