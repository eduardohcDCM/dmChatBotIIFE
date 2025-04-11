# 📦 Instrucciones para insertar el Chatbot en tu página web

A continuación se muestra el script que puedes usar para integrar el **Chatbot de Pedidos** en **cualquier dominio o sitio web**. Solo necesitas copiar y pegar el siguiente fragmento en tu HTML, idealmente antes del cierre de la etiqueta `<body>`:

```html
<script>
window.dcm_config = {
  dcm_c_intro_message: "Hola, soy el asistente de Pedidos, ¿en qué puedo ayudarte?",
  dcm_c_title: "PedidosBot",
  dcm_key: "token",
  dcm_c_name: "contextName"
};
</script>

<!-- Recurso para inserción directa (inline) en el DOM -->
<script src="http://cdn.dcm.mx/resource/js/chatbot-inline.min.js" async></script>

<!-- Recurso para integración mediante iframe -->
<script src="http://cdn.dcm.mx/resource/js/chatbot-iframe.min.js" async></script>
```

> ⚠️ **Importante**: No debes incluir **ambos scripts** (`chatbot-inline.min.js` y `chatbot-iframe.min.js`) al mismo tiempo.  
> Si lo haces, se dará prioridad al script **inline** (`chatbot-inline.min.js`) y el iframe no se cargará.

---

## 🛠️ Explicación de cada atributo

Los siguientes atributos se configuran dentro del objeto global `window.dcm_config` y permiten personalizar el comportamiento del chatbot:

| Atributo               | Descripción |
|------------------------|-------------|
| `dcm_c_intro_message`  | Mensaje de bienvenida que el chatbot mostrará automáticamente al cargar. Ejemplo: `"Hola, soy el asistente de Pedidos, ¿en qué puedo ayudarte?"` |
| `dcm_c_title`          | Título del componente del chatbot. Se muestra en la cabecera del widget. Ejemplo: `"PedidosBot"` |
| `dcm_key`              | Token de autenticación del contexto. Este valor se debe obtener desde el **Manager de Contextos**. Es único para cada cliente o configuración. |
| `dcm_c_name`           | Nombre del contexto del chatbot. También se obtiene desde el **Manager de Contextos** y está vinculado al tipo de conocimiento o comportamiento del bot. |

---

## 🔄 Diferencias entre modos de integración

### 🟦 1. Integración **Inline** (`chatbot-inline.min.js`)

Este modo **inserta directamente** el componente del chatbot en el DOM de tu página.  
Utiliza internamente una **instancia de Vue 2** para renderizar el widget del chatbot.

> ⚠️ **Consideración técnica importante**:  
> Si tu sitio ya utiliza **Vue.js**, especialmente **Vue 2**, asegúrate de que no haya conflictos de versiones ni problemas con la instancia global de Vue.  
> Este script carga Vue 2 directamente desde CDN si no está presente, lo cual **puede interferir** con otras aplicaciones Vue existentes en la misma página.

**Recomendado para:**
- Sitios estáticos o simples que **no usan Vue.js**
- Integraciones donde se desea una mayor personalización visual o integración directa con el DOM

---

### 🟨 2. Integración mediante **iframe** (`chatbot-iframe.min.js`)

Este modo **encapsula** el chatbot dentro de un iframe, aislándolo completamente del DOM y del entorno JavaScript de tu sitio.

**Ventajas:**
- No hay riesgo de conflicto con otras librerías (incluido Vue.js)
- Mayor seguridad y aislamiento del chatbot

**Recomendado para:**
- Sitios con frameworks modernos (Vue, React, Angular, etc.)
- Casos donde no se quiere modificar el DOM directamente
> ⚠️ **Consideración técnica importante**:  
> Estamos implementando una mejora en el espacio que utiliza el iframe, estaremos infomrado del ajuste en los siguientes dias.

---

## ✅ Buenas prácticas

- Asegúrate de cargar solo **uno** de los scripts (`inline` o `iframe`).
- Obtén los valores de `dcm_key` y `dcm_c_name` exclusivamente desde el **Manager de Contextos**.
- Para ambientes productivos, siempre prueba la integración en un entorno de staging antes de publicar en vivo.
