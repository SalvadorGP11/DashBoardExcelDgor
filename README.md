# DgorDashboardExterno

Dashboard estático publicado con GitHub Pages. El Excel no se guarda en el repositorio: se obtiene desde una URL pública externa configurada en `config.js`.

## Archivos

```text
DgorDashboardExterno/
├── index.html
├── config.js
├── .nojekyll
└── README.md
```

## Configuración

Abra `config.js` y reemplace:

```javascript
excelUrl: "PEGA_AQUI_LA_URL_PUBLICA_DIRECTA_DEL_EXCEL"
```

por la URL pública directa de su archivo:

```javascript
excelUrl: "https://pub-xxxxxxxxxxxxxxxx.r2.dev/detalleConcertacion.xlsx"
```

La URL debe:

- descargar directamente un archivo `.xlsx`;
- permitir peticiones `GET`;
- tener CORS habilitado para `https://salvadorgp11.github.io`;
- conservar el mismo nombre o URL cuando se actualice.

## Estructura esperada del Excel

El dashboard utiliza preferentemente alguna de estas hojas:

- `Actividades`
- `Estatus`
- `Accesos`

Si ninguna existe, utiliza la primera hoja.

Campos reconocidos:

- UE o Dirección regional
- CE, Estado o Coordinación
- Folio
- Clave o CVE
- Estatus
- Nombre del acceso o Nombre
- Empleado asignado o Responsable
- Actividad
- Situación
- Detalle
- Observaciones
- Fecha actividad o Fecha

## Publicar en GitHub Pages

1. Cree un repositorio nuevo.
2. Suba `index.html`, `config.js`, `.nojekyll` y `README.md`.
3. Entre a `Settings > Pages`.
4. Seleccione `Deploy from a branch`.
5. Seleccione `main` y `/(root)`.
6. Guarde.

La URL será similar a:

```text
https://salvadorgp11.github.io/NOMBRE_DEL_REPOSITORIO/
```

## Cloudflare R2

Configure CORS en el bucket:

```json
[
  {
    "AllowedOrigins": [
      "https://salvadorgp11.github.io"
    ],
    "AllowedMethods": [
      "GET",
      "HEAD"
    ],
    "AllowedHeaders": [
      "*"
    ],
    "ExposeHeaders": [
      "ETag",
      "Content-Length",
      "Content-Type"
    ],
    "MaxAgeSeconds": 3600
  }
]
```

Después haga público el objeto `detalleConcertacion.xlsx`, copie su URL pública y colóquela en `config.js`.

## Actualización

Para actualizar los datos, reemplace el Excel en el almacenamiento externo conservando la misma URL. El dashboard obtendrá la versión reciente al recargar o al pulsar **Actualizar datos**.
