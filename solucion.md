# GUÍA TÉCNICA — IPFire Proxy + Filtrado Web

***

# FASE 0 — Verificación base de red

## Objetivo

Confirmar que el tráfico pasa por IPFire.

## Paso 0.1 — Gateway

En el cliente:

```
ip route
```

Resultado esperado:

```
default via 192.168.10.254
```

***

## Paso 0.2 — Conectividad

```
ping 8.8.8.8
```

Debe responder.

***

## Paso 0.3 — Navegación

Abrir:

```
http://example.com
```

Debe cargar correctamente.

***

## Validación

* Cliente con salida a Internet
* Gateway correcto
* Navegación funcional

***

# FASE 1 — Activación del proxy

## Objetivo

Forzar el paso del tráfico por IPFire.

## Configuración

Ruta:

```
Servicios → Proxy web
```

<img src="IMG/2.png" alt="2" width="600" height="auto">


Activar:

* Habilitar proxy
* Modo transparente
* Puerto 800

Guardar cambios.

***

## Validación

```
Sistema → Estado
```

Debe aparecer:

```
Proxy encendido
```

***

# FASE 2 — Activación del filtro

## Objetivo

Habilitar el filtrado de contenido.

## Configuración

Ruta:

```
Servicios → Proxy web
```

Activar:

* Filtro de URL


<img src="IMG/5.png" alt="2" width="600" height="auto">


Guardar.

***

## Validación

* Proxy activo
* Sin errores en configuración

***

# FASE 3 — Bloqueo por dominio

## Objetivo

Bloquear páginas específicas.

## Configuración

Ruta:

```
Servicios → Filtro de URL
```

Sección: Lista negra personalizada

Añadir:

```
elnacional.cat
tecnocampus.cat
```

<img src="IMG/7.png" alt="2" width="600" height="auto">


Activar lista negra.

Guardar cambios.

***

## Validación

Probar:

```
https://elnacional.cat
https://tecnocampus.cat
```

Resultado esperado:

<img src="IMG/12.png" alt="2" width="600" height="auto">

<img src="IMG/13.png" alt="2" width="600" height="auto">


* Acceso bloqueado

***

# FASE 4 — Bloqueo por categorías

## Objetivo

Bloquear tipos de contenido.

## Configuración

Ruta:

```
Servicios → Filtro de URL
```

Buscar categorías y bloquear:

* banking / finance
* radio

<img src="IMG/11.png" alt="2" width="600" height="auto">


Guardar cambios.

***

## Validación

Probar:

```
https://www.ing.es
https://www.ah.fm
```

Resultado esperado:

* Sitios bloqueados

***

# FASE 5 — Bloqueo de URL específica

## Objetivo

Control granular dentro de un dominio.

## Configuración

Ruta:

```
Filtro de URL → URLs bloqueadas
```

Añadir:

```
example.com/test

```
o tambien intentaremos bloquear una URL especifica de YouTube como lo es un canal de YT.

<img src="IMG/15.png" alt="2" width="600" height="auto">


<img src="IMG/7.png" alt="2" width="600" height="auto">

Guardar.

***

## Validación

Pruebas:

```
http://youtube.com/@Fernanfloo   → bloqueado
```

<img src="IMG/18.png" alt="2" width="600" height="auto">

<img src="IMG/19.png" alt="2" width="600" height="auto">

```
http://youtube.com        → permitido
```

***

# FASE 6 — Filtrado por palabra clave

## Objetivo

Bloquear contenido dinámico por coincidencia.

## Configuración

Ruta:

```
Filtro de URL → Expresiones / Keywords
```

Añadir:

```
anime
```

<img src="IMG/20.png" alt="2" width="600" height="auto">

***

## Excepción

Ruta:

```
Filtro de URL → Lista blanca
```

Añadir:

```
animenewsnetwork.com
```

<img src="IMG/21.png" alt="2" width="600" height="auto">

Guardar cambios.

***

## Validación

Pruebas:

```
animeflv.net              → bloqueado
```

<img src="IMG/22.png" alt="2" width="600" height="auto">

<img src="IMG/23.png" alt="2" width="600" height="auto">

```
animenewsnetwork.com      → permitido
```

***

# FASE 7 — Restricción por horario

## Objetivo

Control de acceso temporal.

## Configuración

Ruta:

```
Filtro de URL → Control de acceso / Time rules
```

Crear regla:

* Hora inicio
* Hora fin
* Acción: bloquear categoría o dominio

<img src="IMG/26.png" alt="2" width="600" height="auto">

Guardar cambios.

***

## Validación

* Dentro del horario → acceso bloqueado

<img src="IMG/28.png" alt="2" width="600" height="auto">

* Fuera del horario → acceso permitido

<img src="IMG/27.png" alt="2" width="600" height="auto">

