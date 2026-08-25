# Meta MCP oficial (Meta for Developers)

Meta publica dos servidores MCP oficiales en su centro de desarrolladores
(https://developers.facebook.com/documentation/mcp). Ambos son remotos, hablan
**Streamable HTTP** y se autentican por **OAuth** con tu cuenta de desarrollador
de Meta: no hace falta poner App ID, App Secret ni tokens en ningun archivo.

| Servidor | URL | Para que sirve |
|---|---|---|
| Developer Tools MCP | `https://mcp.facebook.com/devtools` | Buscar en la documentacion de Meta, inspeccionar la configuracion y la seguridad de tu app, ver estado de App Review y compliance, uso y limites de la API, y listar / suscribir / probar webhooks. |
| Ads MCP | `https://mcp.facebook.com/ads` | Gestionar campanas, ad sets y anuncios, reporting de rendimiento, catalogos de producto y audiencias. |

Este repositorio ya los declara en `.mcp.json` (ambito de proyecto), asi que
cualquiera que abra el repo con Claude Code los ve disponibles.

## Activarlos en Claude Code

1. Abre el proyecto con Claude Code. Al detectar `.mcp.json` te va a pedir
   aprobar los servidores MCP del proyecto: acepta.
2. Ejecuta `/mcp`, elige `meta-devtools` y lanza **Authenticate**. Se abre el
   navegador con el login de Facebook / Meta; autoriza el acceso.
3. Repite el paso 2 para `meta-ads` si lo vas a usar.
4. Verifica con `/mcp`: los servidores deben aparecer como `connected`.

Alternativa sin `.mcp.json` (ambito local, solo para tu maquina):

```bash
claude mcp add --transport http meta-devtools https://mcp.facebook.com/devtools
claude mcp add --transport http meta-ads     https://mcp.facebook.com/ads
```

## Claude Desktop

Settings -> Connectors -> Add custom connector, y pega la URL del servidor
(`https://mcp.facebook.com/devtools` o `https://mcp.facebook.com/ads`). El
OAuth se resuelve en el navegador igual que en Claude Code.

## Notas

- **Si no queres el MCP de Ads**, borra la entrada `meta-ads` de `.mcp.json`;
  `meta-devtools` funciona por su cuenta.
- El Ads MCP esta en despliegue por fases. Si ves `is_ads_mcp_enabled: false`,
  no es un problema de permisos: tu cuenta todavia no esta habilitada.
- El Developer Tools MCP esta en beta; es de solo lectura salvo una operacion
  de escritura acotada sobre la configuracion de la app.
- Los dos servidores requieren salida a `mcp.facebook.com`. En entornos con
  proxy de egreso restringido (por ejemplo sesiones remotas de Claude Code) la
  conexion se rechaza con 403 y hay que usarlos desde tu maquina local.
