# Agente con OpenRouter y Stitch MCP

Toda la lógica está en **`agente.js`**: prompts, configuración, conexión MCP y bucle autónomo.

## Instalación y configuración

Requisitos: Node.js 22 o posterior, claves de OpenRouter y Stitch, y conexión a Internet.

Desde esta carpeta:

```powershell
npm ci
```

Crear `.env` a partir de `.env.example` si no existe y completar las claves privadas. Se usa `minimax/minimax-m3.1-flash:free`. El agente verifica su gratuidad y fija el precio máximo en cero; no utiliza modelos de pago.

## Ejecución

```powershell
node agente.js
```

La consola muestra la conexión, la creación del proyecto, la generación de la pantalla y su verificación. Después descarga automáticamente estos archivos en `resultado/`, junto a `agente.js`:

- `login.html`: interfaz que se puede abrir en el navegador.
- `login.png`: captura del diseño.
- `resultado.json`: identificadores del proyecto y la pantalla.

La consola confirma la carpeta de destino. Una descarga completa actualiza los archivos del resultado anterior. Cada ejecución crea un proyecto nuevo en Stitch.

Para comprobar la configuración sin crear un diseño:

```powershell
node agente.js --check
```

## Modificar la tarea

Editar `SYSTEM_PROMPT` y `USER_PROMPT` al principio de `agente.js`. El primero contiene las instrucciones del agente; el segundo, la interfaz solicitada.

## Archivos

| Archivo | Uso |
| --- | --- |
| `agente.js` | Código completo del agente y del proxy local de Stitch. |
| `.env` | Claves privadas y modelo; excluido de Git. |
| `.env.example` | Ejemplo genérico de configuración. |
| `package.json` y `package-lock.json` | Dependencias de Node.js y sus versiones. |
| `node_modules/` | Librerías instaladas por npm. |
| `resultado/` | HTML, captura e identificadores de la última descarga. |

La interfaz es un prototipo sin backend de autenticación. Cambiar `USER_PROMPT` afecta a las próximas generaciones. El HTML puede requerir Internet para cargar fuentes y estilos externos. Ante una pérdida de conexión durante una creación o generación, revisar Stitch antes de repetir para evitar duplicados. Si falla la descarga, el diseño permanece en Stitch y la consola muestra el error.

El PDF propone ejecutar `@google/stitch-sdk` mediante `npx`, pero el paquete no incluye un ejecutable. Este archivo inicia el proxy oficial con el argumento interno `--mcp` y conserva la comunicación stdio del ejercicio.
