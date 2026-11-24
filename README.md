# AQUA-T — Frontend React

Interfaz de la tienda AQUA-T (Evaluación 3), desarrollada con React, Vite y Bootstrap. Este repositorio es **independiente** del backend y contiene el código, recursos, pruebas y dependencias necesarias para ejecutar la interfaz.

## Requisitos

- Node.js 22.12 o superior compatible con Vite 8 (o una versión compatible de Node 20, a partir de 20.19).
- npm y Git.
- Para catálogo, inicio de sesión y compras: [AQUA-T-Backend-SpringBoot](https://github.com/JoseLuisCGZ/AQUA-T-Backend-SpringBoot), MySQL y API local en `http://localhost:8080`.

## 1. Clonar e instalar

```powershell
git clone https://github.com/JoseLuisCGZ/AQUA-T-Frontend.git
cd AQUA-T-Frontend
npm ci
```

`npm ci` utiliza el `package-lock.json` versionado.

## 2. Iniciar

Primero levanta **MySQL y Spring Boot** siguiendo el README del backend. Después ejecuta:

```powershell
npm run dev
```

Abre la URL de Vite: normalmente http://localhost:5173.

Los servicios usan `http://localhost:8080` como base de API si no existe `VITE_SPRING_API_URL`. En la instalación local habitual **no necesitas crear `.env.local`**. Si cambias el puerto del backend, crea un archivo `.env.local` en la raíz con:

```env
VITE_SPRING_API_URL=http://localhost:8080
```

Reinicia Vite después de modificar variables. El repositorio incluye el identificador **público** `VITE_GOOGLE_CLIENT_ID`. Para usar Google OAuth, el backend debe configurar el mismo identificador en `GOOGLE_CLIENT_ID` y el origen de React debe estar autorizado en Google Cloud. **El login convencional puede probarse sin Google OAuth.**

## 3. Compilar y ejecutar pruebas

```powershell
npm ci
npm run build
npm test
```

`npm test` utiliza Karma/Jasmine y requiere Google Chrome disponible. La compilación crea la carpeta `dist/`, que está excluida de Git.

## 4. Comprobación funcional

1. Comprueba que http://localhost:8080/api/v1/productos devuelva productos, no `[]`.
2. Abre http://localhost:5173 y revisa el catálogo y las imágenes.
3. Accede con una cuenta Cliente de demostración, añade productos al carrito y completa una compra de prueba.
4. Accede como Administrador y comprueba productos, usuarios y boletas.
5. Accede como Vendedor y verifica que solo pueda consultar las operaciones permitidas.

Las cuentas y contraseñas de demostración se generan en el **backend**, solo si se habilita el seed en una base local vacía.

## 5. Solución de problemas

| Síntoma | Solución |
|---|---|
| No aparecen productos | Revisa MySQL, Spring Boot y la respuesta de `/api/v1/productos` |
| No hay conexión al API | Verifica `VITE_SPRING_API_URL`, puerto `8080` y backend iniciado |
| Error CORS | Usa `http://localhost:5173` o ajusta CORS en Spring Boot |
| No puedes iniciar sesión | Comprueba que se cargaron usuarios demo y conoces la clave configurada localmente |
| Falla Google OAuth | Revisa el Client ID y orígenes de Google Cloud |
| `npm ci` falla | Comprueba `node -v` y `npm -v`; utiliza una versión compatible con Vite 8 |
| `npm test` falla al iniciar Chrome | Asegura que Google Chrome esté instalado |

## Seguridad

No coloques contraseñas de MySQL, secretos JWT ni claves privadas en variables `VITE_*`: cualquier variable `VITE_*` queda expuesta al navegador. No publiques archivos privados de configuración.