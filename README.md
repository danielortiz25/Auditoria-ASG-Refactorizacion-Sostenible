# Auditoria-ASG-Refactorizacion-Sostenible

## INTRODUCCIÓN 

Refactorización del código de la página web 

[https://www.arengalia.es/tabernas/taberna-porvenir](https://www.arengalia.es/tabernas/taberna-porvenir)

## Fase 1: Inventario y Dimensión Ambiental (A)

1. **Medición inicial**. 

Para medir la huella de carbono he usado esta pagina: [https://www.websitecarbon.com/](https://www.websitecarbon.com/)

Y como podemos ver la pagina esta bastante mal:

![Texto descriptivo](/img/Captura%20de%20pantalla%202026-05-13%20133206.png)

2. **Identificación de *Bloatware***. 

Como podemos ver en la imagen la página está bastante “sucia”

![Texto descriptivo](/img/Captura%20de%20pantalla%202026-05-13%20134404.png)

Los principales recursos mas pesados son .jpg (imagenes).

3. **Análisis**. ¿Crees que la web sufre de "inflación de software"? Justifica tu respuesta.

Sí. La web presenta inflación de software porque:

- Carga imágenes muy pesadas sin compresión moderna.

- Descarga scripts externos innecesarios en el primer render.

- No usa lazy loading, lo que dispara el consumo energético.

- El peso total supera 1 MB, límite recomendado para webs sostenibles.

## Fase 2: Dimensión Social y Equidad (S)