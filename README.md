# Auditoria-ASG-Refactorizacion-Sostenible

## INTRODUCCIÓN 

Refactorización del código de la página web 

[https://www.arengalia.es/tabernas/taberna-porvenir](https://www.arengalia.es/tabernas/taberna-porvenir)

## Fase 1: Inventario y Dimensión Ambiental (A)

1. **Medición inicial**. 

Para medir la huella de carbono he usado esta pagina: [https://www.websitecarbon.com/](https://www.websitecarbon.com/)

Y como podemos ver la pagina esta bastante mal:

![](/img/cap1.png)

2. **Identificación de *Bloatware***. 

Como podemos ver en la imagen la página está bastante “sucia”

![](/img/cap2.png)

Los principales recursos mas pesados son .jpg (imagenes).

3. **Análisis**. 

Sí. La web presenta inflación de software porque:

- Carga imágenes muy pesadas sin compresión moderna.

- Descarga scripts externos innecesarios en el primer render.

- No usa lazy loading, lo que dispara el consumo energético.

- El peso total supera 1 MB, límite recomendado para webs sostenibles.

## Fase 2: Dimensión Social y Equidad (S)

1.**Test de Accesibilidad.**

Se ha realizado un análisis de accesibilidad sobre la página [https://www.arengalia.es/tabernas/taberna-porvenir](https://www.arengalia.es/tabernas/taberna-porvenir) utilizando la herramienta WAVE Web Accessibility Evaluation Tool.

El resultado general refleja una accesibilidad moderada, con margen de mejora en aspectos visuales y estructurales.

| Métrica | Resultado | Interpretación |
| ----- | ----- | ----- |
| Errores | 9 | Elementos que incumplen directamente las pautas WCAG 2.2 (atributos ALT ausentes, etiquetas incorrectas, etc.). |
| Errores de contraste | 2 | Problemas de visibilidad entre texto y fondo, especialmente en botones o títulos sobre imágenes. |
| Alertas | 6 | Aspectos que podrían generar confusión o dificultar la navegación (uso excesivo de ARIA, estructura no semántica). |
| Características detectadas | 77 | Elementos correctamente implementados (roles, etiquetas, landmarks). |
| Estructura | 25 | Se detecta una jerarquía básica, aunque con encabezados desordenados. |
| Elementos ARIA | 222 | Uso elevado de atributos ARIA, algunos redundantes o innecesarios. |
| AIM Score | 7.4 / 10 | Nivel de accesibilidad aceptable, pero no óptimo para cumplir WCAG 2.2 AA. |

![](/img/cap3.png)

2. **Identificación de barreras**

El análisis realizado con WAVE revela varias barreras que afectan a la accesibilidad de la página. La primera es la ausencia de atributos ALT en imágenes importantes, lo que impide que los lectores de pantalla describan el contenido visual a usuarios con discapacidad visual. También se detectan problemas de contraste en algunos textos y botones, especialmente cuando aparecen sobre fondos claros, dificultando la lectura para personas con baja visión.