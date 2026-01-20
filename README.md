# SITIO WEB PARA UC IDEIAK

Sitio principal para la web, responsive y mobile first

## TECNOLOGÍAS USADAS

Sitio desarrollado con con VITE y TYPESCRIPT utilizando TAILWINDCSS para los script.

Al hacer *build* del sitio, VITE por defecto genera una SPA y hay que realizar algunas modificaciones adicionales para que el proceso de construcción genere todas las páginas (MULTIPAGE).
Se modifica el archivo **vite.config.ts** de la siguiente forma:

```
import { defineConfig } from 'vite'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  base: '/',
  plugins: [
    tailwindcss(),
  ],
  build: {
    rollupOptions: {
      input: {
        main: './index.html',
        login: './login.html',
        contacto: './contacto.html',
        thanks: './thanks.html',
        no_login: './no_login.html',
      }
    }
  }
})
```

## DEPLOY A GITHUB

Para el despliegue de la web de utiliza GITHUB-PAGES utilizando el repositorio de la organización *uc-ideiak.github.io*

En ese repositorio se crean dos ramas

- MAIN con el proyecto principal
- GH-PAGES que contiene la carpeta DIST obtenida al hacer BUILD

De esta forma se mantienen ambas ramas por separado y se simplifica el desarrollo.

El fichero **package.json** después de instalar _npm install gh-pages_

```
{
  "name": "uc-ideiak-site",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "predeploy": "npm run build",
    "deploy": "gh-pages -d dist -b gh-pages"
  },
  "devDependencies": {
    "gh-pages": "^6.3.0",
    "typescript": "~5.9.3",
    "vite": "^7.1.7"
  },
  "dependencies": {
    "@tailwindcss/vite": "^4.1.16",
    "tailwindcss": "^4.1.16"
  }
}
```

Después de desplegar el proyecto de esta forma se utiliza CLOUDFLARE para apuntar el dominio a la rama que contiene la carpeta DIST en el repositorio de GitHub.
