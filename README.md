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

1. **Test de Accesibilidad.**

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

## Fase 3: Dimensión de Gobernanza y Ética (G)

En esta fase analizo cómo la web trata la información del usuario y si es transparente a la hora de pedir consentimiento o datos personales. Aunque la página funciona correctamente, hay algunos aspectos que podrían mejorarse para que el usuario tenga más control y claridad sobre lo que acepta.

1. Transparencia

El banner de cookies no es demasiado claro. El botón de aceptar está muy destacado, mientras que la opción de rechazar o configurar está más escondida. Esto hace que el usuario tienda a aceptar sin pensar, lo que puede considerarse un pequeño patrón oscuro. Sería mejor que ambas opciones estuvieran igual de visibles para que el usuario pueda decidir de forma más transparente.

2. Datos innecesarios

El formulario pide nombre, correo y teléfono incluso para una consulta sencilla. No queda claro si todos esos datos son realmente necesarios ni para qué se van a usar exactamente. Además, la política de privacidad no está muy visible, lo que dificulta que el usuario pueda revisar cómo se gestionan sus datos antes de enviarlos. Reducir los datos solicitados y hacer más accesible la información legal mejoraría la experiencia y la confianza del usuario.


## Fase 4: Propuesta de Refactorización (Green Coding)


Después de revisar el código de la página de la Taberna del Porvenir, he encontrado varias mejoras que pueden aplicarse para que la web sea más ligera, accesible y sostenible. La página usa UIkit y carga muchas imágenes, módulos y scripts que pueden optimizarse sin cambiar el diseño.


1. Optimización de activos


En el código hay imágenes con atributos rotos, por ejemplo:


html

//<img class="el-image"
src="/media/yootheme/cache/43/logo.png"
alt=" loading="lazy" width="60" height="30">

Ese alt=" loading="lazy" está mal escrito y rompe tanto el alt como el lazy loading.


Corrección:


html
//</img class="el-image"
src="/media/yootheme/cache/43/logo.webp"
loading="lazy"
alt="Logotipo Andalucía se mueve con Europa"
width="60" height="30">


Además, algunas imágenes cargan versiones muy grandes aunque se muestran pequeñas. Aquí se puede reducir el tamaño o eliminar PNG si ya existe WebP o AVIF.


2. Reducción de peticiones


El HTML carga muchos scripts sin defer, lo que bloquea la carga inicial.


Ejemplo actual:


html
//<script src="/js/main.js"></script>


Mejora:


html
//<script src="/js/main.js" defer></script>


También se carga el iframe de la visita virtual aunque el usuario no lo haya abierto:


html
//<iframe src="https://my.matterport.com/show/?m=RvJUeutmoxa&play=1"></iframe>


Esto debería cargarse solo cuando el usuario haga clic en “Visita virtual”.


3. Mejora social (Accesibilidad)


En el HTML hay varios problemas:


Encabezados desordenados (hay un h2 antes del h1).


Iconos SVG sin aria-hidden.


Atributos alt vacíos o rotos.


Botones del menú móvil con aria-expanded que no coincide con el estado real.


Ejemplo de icono sin accesibilidad:


html
//<svg width="20" height="20">...</svg>


Mejora:


html
//<svg width="20" height="20" aria-hidden="true">...</svg>


Ejemplo de encabezado mal ordenado:


html
<h2>Taberna del Porvenir</h2>
<h1>Cardenal Bueno Monreal, 20</h1>


Lo correcto sería que el título principal fuese el h1.


4. Mejora de gobernanza (Ética y privacidad)
Aunque en el fragmento no aparece el banner de cookies, sí se ve que:


Los formularios piden teléfono incluso para cosas simples.


Los enlaces legales no están muy visibles.


Propuesta para el banner de cookies:


html

//<button class="btn-cookies aceptar">Aceptar</button>
//<button class="btn-cookies rechazar">Rechazar</button>


Esto evita patrones oscuros y mejora la transparencia.


5. Reflexión sobre la Paradoja de Jevons


Si la web se optimiza y carga más rápido, puede aumentar el tráfico. Para evitar que eso aumente el consumo total:


Activar caché del navegador.


Servir imágenes desde un CDN.


Evitar añadir módulos UIkit innecesarios.


Mantener la web ligera y sin scripts pesados.
