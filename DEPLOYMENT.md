# Guía de Despliegue en GitHub Pages

Este documento explica cómo está configurado el despliegue automático de este sitio web en GitHub Pages.

## Configuración Actual

El sitio está configurado para desplegarse automáticamente en **https://michifeli.github.io** mediante GitHub Actions.

### Archivo de Configuración de Astro

En `astro.config.mjs`, el sitio está configurado con:

```javascript
export default defineConfig({
  site: 'https://michifeli.github.io',
  base: "/",
  // ...
});
```

- **site**: La URL donde se alojará el sitio
- **base**: El path base (raíz en este caso)

### Workflow de GitHub Actions

El archivo `.github/workflows/deploy.yml` contiene la configuración para el despliegue automático:

#### Cuándo se Ejecuta

- **Automáticamente**: Cada vez que se hace push a la rama `main`
- **Manualmente**: Se puede ejecutar desde la pestaña "Actions" en GitHub usando "workflow_dispatch"

#### Proceso de Despliegue

1. **Build**: Compila el sitio Astro
   - Instala Node.js 22 y pnpm 10
   - Instala las dependencias con `pnpm install`
   - Construye el sitio con `pnpm run build`
   - Genera los archivos estáticos en el directorio `dist/`

2. **Deploy**: Publica el sitio en GitHub Pages
   - Sube los archivos del directorio `dist/` a GitHub Pages
   - El sitio queda disponible en https://michifeli.github.io

## Cómo Hacer Cambios y Desplegarlos

### Opción 1: Despliegue Automático (Recomendado)

1. Haz tus cambios en el código
2. Commit y push a la rama `main`:
   ```bash
   git add .
   git commit -m "Descripción de tus cambios"
   git push origin main
   ```
3. El workflow se ejecutará automáticamente y tu sitio se actualizará en unos minutos

### Opción 2: Despliegue Manual

1. Ve a la pestaña "Actions" en tu repositorio de GitHub
2. Selecciona "Deploy Astro site to Pages"
3. Haz clic en "Run workflow"
4. Selecciona la rama `main` y confirma

## Verificar el Despliegue

### Ver el Estado del Workflow

1. Ve a la pestaña "Actions" en tu repositorio
2. Verás el historial de ejecuciones del workflow
3. Haz clic en una ejecución para ver los detalles y logs

### Acceder al Sitio

Una vez que el workflow se complete exitosamente:
- Tu sitio estará disponible en: **https://michifeli.github.io**
- Los cambios pueden tardar 1-2 minutos en propagarse

## Solución de Problemas

### El Workflow Falla

1. Revisa los logs en la pestaña "Actions"
2. Verifica que el build local funcione:
   ```bash
   pnpm install
   pnpm run build
   ```
3. Asegúrate de que todos los archivos necesarios estén committeados

### El Sitio No Se Actualiza

1. Verifica que el workflow se haya completado exitosamente
2. Espera unos minutos para la propagación
3. Limpia la caché del navegador (Ctrl+Shift+R o Cmd+Shift+R)
4. Verifica la configuración de GitHub Pages en Settings > Pages

## Configuración de GitHub Pages

Para que el despliegue funcione, asegúrate de que en la configuración del repositorio:

1. Ve a **Settings** > **Pages**
2. En "Build and deployment":
   - **Source**: GitHub Actions
3. El sitio debería estar publicado en https://michifeli.github.io

## Archivos Importantes

- `.github/workflows/deploy.yml` - Configuración del workflow de CI/CD
- `astro.config.mjs` - Configuración de Astro con la URL del sitio
- `.nojekyll` - Indica a GitHub Pages que no use Jekyll
- `dist/` - Directorio de salida del build (no se commitea, ver .gitignore)

## Recursos Adicionales

- [Documentación de Astro sobre despliegue en GitHub Pages](https://docs.astro.build/en/guides/deploy/github/)
- [Documentación de GitHub Actions](https://docs.github.com/en/actions)
- [Documentación de GitHub Pages](https://docs.github.com/en/pages)
