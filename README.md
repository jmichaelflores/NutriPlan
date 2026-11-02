# NutriPlan 2.0

Aplicación web estática para planificar comidas para dos adultos, sin pescado ni mariscos. Compatible con GitHub Pages en `/NutriPlan/`. No requiere API, cuentas ni servidor.

## Uso y publicación

Sube **todos los archivos y carpetas** a la raíz de la rama `main` de `jmichaelflores/NutriPlan`. En GitHub Pages selecciona `main` y `/ (root)`. Abre `https://jmichaelflores.github.io/NutriPlan/` y, desde Android, usa la opción de instalar/agregar a pantalla principal si el navegador lo permite.

Para pruebas locales, desde esta carpeta ejecuta `python3 -m http.server 8000` y abre `http://localhost:8000`. Para las pruebas de lógica ejecuta `node --test tests/core.test.js` (Node 18+). Un servidor HTTP es necesario para comprobar el service worker.

## Arquitectura

- `index.html`: estructura accesible y vistas.
- `styles.css`: interfaz responsive y modo oscuro.
- `core.js`: catálogo, estimaciones nutricionales, motor de planificación, compras, validación y migración; también funciona en Node para pruebas.
- `app.js`: interfaz, interacciones, persistencia y exportaciones.
- `sw.js` / `manifest.webmanifest` / `icons/`: PWA y cache offline.
- `tests/core.test.js`: pruebas automatizadas sin dependencias.

## Datos y privacidad

Los datos se guardan en `localStorage` (`nutriplan-v2`) del dispositivo. El primer uso intenta migrar el formato previo `nutriplan` sin borrarlo. Exporta el respaldo JSON antes de sustituir la versión anterior. No hay sincronización entre dispositivos. Importar un respaldo reemplaza el estado actual tras confirmación.

## Alcance y limitaciones

**Los valores por 100 g son estimaciones ilustrativas, NO datos clínicos verificados.** Deben revisarse y reemplazarse por una base de composición nutricional confiable, con identificación de fuente y preparación específica. Las recetas incluyen gramajes de referencia, pero no ajustes por merma, absorción de aceite, rendimiento de cocción o cambios de peso. Las metas energéticas son orientativas y no prescriben dietas. La fórmula de gasto basal es Mifflin-St Jeor, usando sexo registrado; el gasto total multiplica por un factor de actividad estimado.

El costo solo se calcula con precios ingresados manualmente. Las unidades de compra son aproximadas; no se validan precios actuales. La lista de compras considera comidas **aceptadas** durante los siete días visibles y descuenta inventario sin modificarlo. Marcar una comida como consumida **no** descuenta automáticamente inventario. La PWA usa icono SVG, cuya instalación puede variar entre navegadores; iconos PNG y pruebas en dispositivos reales quedan pendientes.

**Limitaciones conocidas**: no existe editor individual de ingredientes dentro de una receta; se pueden ajustar las porciones. El inventario no maneja todavía caducidad. No se han ejecutado pruebas visuales ni E2E en Android; únicamente pruebas unitarias de lógica. La navegación offline necesita una primera visita online y un navegador compatible.