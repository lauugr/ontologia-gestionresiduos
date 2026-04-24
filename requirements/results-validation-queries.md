# Validación del grafo RDF mediante consultas SPARQL

Se ha realizado la validación del grafo RDF generado a partir de los datasets mediante un conjunto de consultas SPARQL ejecutadas sobre el fichero `output-gestion-residuos.ttl` (ubicado en `/mappings/output`).

El grafo ha sido construido a partir de reglas RML y materializado con Morph-KGC en formato N-Triples. Posteriormente ha sido convertido a Turtle para facilitar su análisis.

Las consultas se han ejecutado utilizando la librería rdflib de Python con el objetivo de comprobar la calidad, consistencia y completitud de los datos.

# Resultados de la validación
```
Grafo cargado

================================================================================
QUERY 1 - Número total de centros de gestión
================================================================================
794

================================================================================
QUERY 2 - Número total de contenedores
================================================================================
44249

================================================================================
QUERY 3 - Número total de puntos limpios por tipo
================================================================================
https://w3id.org/def/medioambiente/residuos#MobileCollectionPoint | 409
https://w3id.org/def/medioambiente/residuos#PermanentCollectionPoint | 58

================================================================================
QUERY 4 - Centros de gestión sin número de registro
================================================================================
Sin resultados

================================================================================
QUERY 5 - Centros de gestión sin dirección
================================================================================
Sin resultados

================================================================================
QUERY 6 - 'order' mal tipado en contenedores
================================================================================
Sin resultados

================================================================================
QUERY 7 - 'isConstructionDemolitionWasteManager' mal tipado en centros de gestión
================================================================================
Sin resultados

================================================================================
QUERY 8 - 'isPubliclyOwned' mal tipado en puntos limpios
================================================================================
Sin resultados

================================================================================
QUERY 9 - Direcciones sin literal de dirección
================================================================================
https://w3id.org/medioambiente/recurso/residuos/address/13G01A1200004545S
https://w3id.org/medioambiente/recurso/residuos/address/13G01A1200005213Q
https://w3id.org/medioambiente/recurso/residuos/address/13G01A1200005682W
https://w3id.org/medioambiente/recurso/residuos/address/13G01A1200006810A
https://w3id.org/medioambiente/recurso/residuos/address/13G01A1200007644D
https://w3id.org/medioambiente/recurso/residuos/address/13G01A1200007648J
https://w3id.org/medioambiente/recurso/residuos/address/13G01A1200007653H
https://w3id.org/medioambiente/recurso/residuos/address/13G01A1200007926S
https://w3id.org/medioambiente/recurso/residuos/address/13G01A1200008186E
https://w3id.org/medioambiente/recurso/residuos/address/13G01A1200009020M
... 784 filas más

================================================================================
QUERY 10 - Municipios sin provincia
================================================================================
Sin resultados

================================================================================
QUERY 11 - Duplicados de número de registro en centros de gestión
================================================================================
Sin resultados

================================================================================
QUERY 12 - Contenedores con 'belongsTo' apuntando a recursos no territoriales esperados
================================================================================
Sin resultados
```

# Interpretación de resultados

Las primeras tres consultas indican que el grafo contiene 794 centros de gestión, 44249 contenedores y un total de 467 puntos limpios, de los cuales 409 son móviles y 58 permanentes.
El resto de consultas, excepto la 9, no devuelve resultados, lo que indica que no se han detectado errores en los aspectos validados.

La consulta relativa a direcciones sin literal `esdir:direccion devuelve resultados debido a que, en el caso de los centros de gestión, la dirección se ha modelado mediante atributos desglosados (como tipo de vía, nombre de la vía o número), en lugar de un único literal completo. Por tanto, este resultado no se considera un error, sino una consecuencia del modelo adoptado.

En consecuencia, el grafo RDF generado presenta un alto nivel de calidad y consistencia.