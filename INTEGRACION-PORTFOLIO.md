# Integración de FoodLoop en CristinaDeniaCarretero.com

## Objetivo

FoodLoop aparecerá como un proyecto dentro de la sección de Proyectos del portfolio. La tarjeta enlazará a:

```text
/foodloop/
```

La aplicación se abrirá como página independiente, no dentro de un iframe.

## Estructura final del sitio

```text
sitio-principal/
├── index.html                  # portfolio actual
├── ...
└── foodloop/                   # copiar desde el repo Inventario
    ├── index.html
    ├── assets/logo.svg
    ├── css/styles.css
    └── js/
        ├── db.js
        ├── export.js
        └── app.js
```

## Tarjeta genérica de proyecto

Este fragmento es solo una referencia. Cuando se reciba el HTML/CSS real del portfolio debe adaptarse a los componentes y clases existentes, en lugar de pegarse sin más.

```html
<a href="/foodloop/" class="project-card">
  <div class="project-card__tag">Local-first · Data</div>
  <h3>FoodLoop</h3>
  <p>Inventario doméstico, histórico de compras y reposición basada en hábitos.</p>
  <span>Abrir FoodLoop →</span>
</a>
```

## Importante sobre el repositorio `Inventario`

GitHub Pages publica los sitios de proyecto usando el nombre del repositorio como parte de la ruta. Por tanto, mientras `Inventario` sea un proyecto independiente, su URL de proyecto contendrá `Inventario`.

La ruta exacta `/foodloop/` se consigue de una de estas dos formas:

1. **Recomendada para este caso:** mantener `Inventario` como repositorio de desarrollo y copiar la carpeta `foodloop/` al repositorio que publica el portfolio.
2. Renombrar el repositorio de proyecto a `foodloop`, si se quiere que el propio project site utilice ese nombre de ruta.

No se puede asignar un dominio personalizado de GitHub Pages a una ruta arbitraria como `dominio.com/foodloop`; los dominios personalizados operan a nivel de dominio/subdominio.

## Siguiente integración

Cuando se proporcione el archivo/repo actual del portfolio:

1. localizar la sección `Proyectos`;
2. replicar exactamente el diseño de sus tarjetas;
3. añadir FoodLoop como nuevo proyecto;
4. copiar la carpeta `foodloop/` al sitio publicado;
5. verificar rutas relativas y responsive;
6. probar `https://.../foodloop/` directamente y desde la tarjeta.
