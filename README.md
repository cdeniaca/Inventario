# FoodLoop

FoodLoop es una herramienta web local-first para registrar compras, mantener stock doméstico, anotar consumos y desperdicio, generar una lista de reposición y conservar histórico.

## Principios de esta versión

- Sin backend.
- Sin cuenta de usuario.
- Sin API keys.
- Sin ChatGPT/IA.
- Sin librerías externas cargadas desde CDN.
- Los datos se guardan en IndexedDB en el navegador que estés utilizando.
- El repositorio contiene código, nunca tus tickets ni tu histórico.
- La copia maestra de los datos es el backup JSON que descargas desde FoodLoop.

## Estructura

```text
Inventario/
├── index.html                 # Redirige a ./foodloop/
├── .nojekyll
├── README.md
├── INTEGRACION-PORTFOLIO.md
└── foodloop/
    ├── index.html
    ├── assets/
    │   └── logo.svg
    ├── css/
    │   └── styles.css
    └── js/
        ├── db.js              # IndexedDB + modelo de datos + hábitos
        ├── export.js          # backup, archivo por periodo y CSV
        ├── xlsx.js            # exportación Excel .xlsx sin dependencias
        └── app.js             # interfaz y flujos de uso
```

## Qué guarda FoodLoop

La base IndexedDB contiene seis colecciones:

- `products`: catálogo de productos y datos como ubicación/unidad/caducidad.
- `tickets`: cabecera de cada compra.
- `purchaseLines`: líneas de producto de cada ticket.
- `movements`: compras, consumos, desperdicios y ajustes.
- `shopping`: lista de compra manual o sugerida.
- `settings`: metadatos locales, como fecha del último backup.

El stock actual no se sobrescribe: se calcula sumando movimientos.

```text
stock = compras - consumos - desperdicio +/- ajustes
```

## Backups y exportaciones

### Backup completo

`FoodLoop → Datos → Descargar backup completo`

Genera un JSON con toda la base. Es la copia maestra y se puede importar en otro navegador/dispositivo.

### Archivo restaurable de un periodo

`FoodLoop → Histórico → elegir fechas → Archivo restaurable del periodo`

El archivo incluye los registros del intervalo y un saldo inicial sintético para que el periodo sea autocontenido. Por ejemplo, puedes archivar el año natural 2026.

### Excel por periodo

`FoodLoop → Histórico → elegir fechas → Excel (.xlsx)`

Genera un libro Excel real con hojas de Resumen, Tickets, Compras, Movimientos y Productos. Se construye localmente en el navegador, sin subir datos a un servidor.

### CSV

`FoodLoop → Histórico → elegir fechas → CSV`

Genera un CSV UTF-8 separado por punto y coma con compras, consumos, desperdicio y ajustes.

## Probar en GitHub Pages desde el repositorio Inventario

1. Sube el contenido de esta carpeta a la raíz del repositorio `Inventario`.
2. En GitHub abre `Settings` → `Pages`.
3. En `Build and deployment`, selecciona `Deploy from a branch`.
4. Selecciona `main` y `/ (root)`.
5. Guarda.

El `index.html` de la raíz redirige automáticamente a `./foodloop/`.

## URL final deseada

El objetivo es:

```text
https://www.cristinadeniacarretero.com/foodloop/
```

Para obtener exactamente esa ruta manteniendo `Inventario` como repositorio separado, la carpeta `foodloop/` deberá incorporarse también a la raíz publicada del repositorio que sirve `cristinadeniacarretero.com`.

Cuando se integre el portfolio, quedará:

```text
portfolio/
├── ...
└── foodloop/
    ├── index.html
    ├── assets/
    ├── css/
    └── js/
```

No hace falta modificar las rutas internas de FoodLoop porque son relativas (`./css/...`, `./js/...`).

## Trasladar del móvil al ordenador

1. En el móvil: `Datos → Descargar backup completo`.
2. Transfiere el `.json` al ordenador por el método que prefieras.
3. Abre FoodLoop en el ordenador.
4. `Datos → Importar / restaurar backup`.
5. El ordenador tendrá la misma fotografía de datos que tenía el móvil al crear el backup.

No existe sincronización automática entre los dos navegadores. Si haces cambios en ambos por separado, tendrás dos copias diferentes.

## Privacidad

FoodLoop no envía los registros a un backend. Aun así, si se publica bajo `/foodloop/` comparte el mismo origen web que el resto de `cristinadeniacarretero.com`; por ello conviene controlar los scripts de terceros que se ejecutan bajo ese dominio.

## Futuras fases

La arquitectura deja preparados los siguientes pasos sin cambiar el modelo base:

- pegar texto de ticket y convertirlo en líneas de compra;
- OCR local de fotografías;
- escaneo de códigos de barras;
- lotes con varias fechas de caducidad para un mismo producto;
- gráficos de evolución de gasto/precios;
- reglas de reposición más sofisticadas.
