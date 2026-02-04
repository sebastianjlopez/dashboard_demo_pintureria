# Dashboard Chatbot 24/7 – Especificación de métricas

Este documento describe **todas las características y métricas** que el dashboard consume. El equipo de chatbots debe habilitar las interacciones y eventos necesarios para alimentar estos datos (por sesión, conversación, lead o venta).

---

## 1. KPIs de Negocio

| Métrica | Descripción | Qué debe habilitar el chatbot |
|--------|-------------|-------------------------------|
| **Ventas generadas por el Bot (ARS)** | Monto total en pesos atribuible a conversaciones/acciones del bot en el período. | Registrar cada venta o cita cerrada originada en el chat (ID de conversación, monto en ARS, fecha). Opcional: atribución por último mensaje antes del cierre. |
| **Leads calificados** | Cantidad de usuarios que completaron datos para contacto (nombre, teléfono/email, etc.). | Evento “lead_captured” cuando el usuario envía todos los campos requeridos del formulario o flujo de captación (ej. después de “Quiero que me contacten” con datos completos). |
| **Horas hombre ahorradas** | Horas equivalentes de atención manual que el bot reemplazó. | Estimar por: (consultas resueltas sin humano × tiempo promedio de resolución manual). Necesario: marcar conversaciones como “resuelta por bot” vs “escalada a humano” y tiempo medio de resolución manual (ej. 15–25 min). |

---

## 2. Resumen operativo

| Métrica | Descripción | Qué debe habilitar el chatbot |
|--------|-------------|-------------------------------|
| **Disponibilidad** | % de tiempo en que el bot estuvo operativo (uptime). | Healthchecks o logs de disponibilidad del servicio del bot; agregar por período (semana/mes/trimestre). |
| **Respuesta promedio** | Tiempo medio (ej. segundos) desde el mensaje del usuario hasta la primera respuesta del bot. | Timestamp de cada mensaje entrante y de la primera respuesta del bot por turno; promediar por período. |
| **Total interacciones** | Número total de intercambios o mensajes en el período. | Contar mensajes de usuario (o “turnos” de conversación) por período. |
| **Ahorro mensual (ARS)** | Ahorro en costos operativos por uso del bot. | Calcular a partir de horas ahorradas × costo por hora, o fórmula acordada con negocio (ej. equivalente a X empleados). |

---

## 3. Análisis de sentimiento

| Métrica | Descripción | Qué debe habilitar el chatbot |
|--------|-------------|-------------------------------|
| **Humor de los usuarios** | Distribución %: Positivo / Neutro / Enojado (o Negativo). | Por conversación o por mensaje: clasificación de sentimiento (modelo propio, API o reglas). Enviar etiqueta: `positive`, `neutral`, `negative` (o equivalente) y opcionalmente score. Agregar a diario/semanal/mensual para el dashboard. |

---

## 4. Métricas de eficiencia

| Métrica | Descripción | Qué debe habilitar el chatbot |
|--------|-------------|-------------------------------|
| **Tasa de automatización (Automation Rate)** | % de conversaciones resueltas solo por el bot vs. % que requirieron humano. | Por conversación: flag o estado final `resuelta_por_bot` vs `escalada_a_agente`. Calcular % sobre el total de conversaciones cerradas en el período. |
| **Tiempo de respuesta: Antes vs. Ahora** | Comparativa “Antes (manual)” en minutos vs “Ahora (bot)” en segundos. | “Ahora”: ya se obtiene del “Respuesta promedio” del resumen operativo. “Antes”: valor de referencia histórica o de negocio (ej. 25 min manual); puede ser fijo o por campaña. |

---

## 5. Inteligencia de mercado

| Métrica | Descripción | Qué debe habilitar el chatbot |
|--------|-------------|-------------------------------|
| **Motivos de contacto** | Distribución % de por qué escribe el usuario. Categorías del dashboard: **Precios**, **Soporte técnico**, **Horarios**, **Reclamos**. | Clasificar cada conversación (o primer mensaje) en una de estas 4 categorías. Puede ser: intención detectada (NLU), menú elegido, o keyword; enviar categoría al cerrar o al detectar intención. |
| **Horarios pico** | Cantidad de mensajes o sesiones por hora del día (0h–23h). | Timestamp (fecha y hora) de cada mensaje entrante o de cada “sesión iniciada”; agregar conteos por hora para el período seleccionado. |

---

## 6. Embudo de conversión

El dashboard muestra 4 etapas en orden. Cada una debe ser un **conteo por período** (semana/mes/trimestre).

| Etapa | Descripción | Qué debe habilitar el chatbot |
|-------|-------------|-------------------------------|
| **Sesiones iniciadas** | Usuarios que abrieron o iniciaron una conversación. | Evento “sesión_iniciada” (por canal y usuario único por período, si aplica). |
| **Interacción con menú** | Usuarios que eligieron al menos una opción del menú o flujo principal. | Evento cuando el usuario responde a un menú (botones, quick replies, opciones numeradas) o completa el primer paso del flujo. |
| **Leads capturados** | Usuarios que dejaron datos de contacto (mismo criterio que “Leads calificados”). | Mismo evento “lead_captured” que para el KPI de leads; contar por período. |
| **Ventas / Citas cerradas** | Ventas o citas concretadas atribuibles al bot. | Mismo criterio que “Ventas generadas por el Bot”: evento de cierre (venta o cita) vinculado a la conversación/canal. |

---

## 7. Rendimiento del Chatbot

### 7.1 Tarjetas de métricas

| Métrica | Descripción | Qué debe habilitar el chatbot |
|--------|-------------|-------------------------------|
| **Total consultas** | Número de consultas o conversaciones en el período. | Contar conversaciones únicas (o “consultas” según definición: por sesión, por tema, etc.) y enviar total por período. |
| **Tasa de resolución** | % de consultas que se cerraron como “resueltas” (por bot o agente). | Por conversación: estado de cierre `resuelta` vs `abandonada`/`sin_resolver`; calcular % sobre total de conversaciones cerradas. |
| **Tiempo promedio** | Duración media de una conversación (ej. en minutos). | Timestamp de inicio y cierre de conversación; calcular diferencia y promediar por período. |
| **Satisfacción** | Puntuación media (ej. 1–5) de satisfacción del usuario. | Encuesta post-chat o valor inferido; enviar score por conversación y promediar (ej. 4.6/5). |

### 7.2 Gráficos

| Gráfico | Datos necesarios |
|---------|------------------|
| **Conversaciones por día** | Conteo de conversaciones (o mensajes) por día en el período (ej. 15 días). |
| **Distribución por hora del día** | Conteo por franja horaria (ej. 00h, 03h, 06h, …, 21h). Mismo dato base que “Horarios pico” pero agregado en 8 franjas si se desea. |
| **Tipos de consultas** | Conteo por categoría de consulta. Categorías del dashboard: **Colores y combinaciones**, **Rendimiento y cantidad**, **Precios**, **Aplicación y técnicas**, **Productos específicos**. Clasificar cada conversación en una de estas 5. |
| **Canales de comunicación** | Conteo por canal. Canales del dashboard: **WhatsApp**, **Web Chat**, **Facebook**, **Instagram**. Enviar `channel_id` o nombre en cada evento de mensaje/sesión. |
| **Calificaciones del servicio** | Conteo de conversaciones (o respuestas de encuesta) por puntuación: 1 a 5 estrellas. Enviar la puntuación dada por el usuario. |

---

## 8. Logística y gestión de pedidos

### 8.1 Tarjetas de métricas

| Métrica | Descripción | Qué debe habilitar el chatbot |
|--------|-------------|-------------------------------|
| **Pedidos gestionados** | Cantidad de pedidos creados o gestionados vía bot en el período. | Evento “pedido_creado” o “pedido_gestionado” (ej. confirmación, cambio, consulta de estado) vinculado al chat. |
| **Tiempo promedio de entrega** | Promedio de días desde pedido hasta entrega. | Fecha de pedido y fecha de entrega (o estado “entregado”) por pedido; calcular días y promediar. Puede venir de CRM/ERP y cruzarse con “origen = chatbot”. |
| **Pedidos demorados** | Cantidad de pedidos que superaron el tiempo de entrega acordado. | Comparar “fecha entrega real” vs “fecha prometida”; marcar como demorado y contar por período. |
| **Tasa de cumplimiento** | % de pedidos entregados a tiempo. | (Pedidos a tiempo / Total pedidos con entrega) × 100 en el período. |

### 8.2 Gráficos

| Gráfico | Datos necesarios |
|---------|------------------|
| **Estado de pedidos** | Conteo por estado. Estados del dashboard: **Entregados**, **En tránsito**, **Preparando**, **Demorados**, **Cancelados**. Sincronizar estados con CRM/ERP y filtrar por pedidos originados en chatbot si aplica. |
| **Distribución de tiempos de entrega** | Conteo de pedidos por rango de días de entrega: **1 día**, **2 días**, **3 días**, **4 días**, **5+ días**. Calcular días por pedido y agrupar. |
| **Pedidos y demoras por semana** | Para cada semana del período: total de pedidos y cantidad de pedidos demorados (dos series). |
| **Pedidos por zona** | Conteo por zona geográfica. Zonas del dashboard: **Centro**, **Zona Norte**, **Zona Sur**, **Zona Oeste**, **Zona Este**. Incluir zona (o dirección/CP) al registrar el pedido. |
| **Motivos de demoras** | Conteo por motivo cuando el pedido está demorado. Motivos del dashboard: **Stock insuficiente**, **Problemas de tráfico**, **Dirección incorrecta**, **Cliente ausente**, **Otros**. Registrar motivo al marcar demora o al cerrar incidencia. |

---

## 9. Resumen para el equipo de chatbots

Para que el dashboard se alimente correctamente, el equipo de chatbots debe implementar o exponer:

1. **Eventos mínimos**
   - `sesión_iniciada` (con timestamp, canal, user_id).
   - `interacción_menú` (usuario eligió opción de menú).
   - `lead_captured` (datos completos de contacto).
   - `venta_o_cita_cerrada` (con monto ARS si aplica).
   - `conversación_cerrada` (con estado: resuelta_por_bot / escalada / resuelta_por_agente / abandonada).
   - `mensaje_recibido` / `mensaje_enviado` (con timestamp para respuesta promedio y conteo por hora).

2. **Clasificaciones por conversación**
   - Motivo de contacto: Precios | Soporte técnico | Horarios | Reclamos.
   - Tipo de consulta: Colores y combinaciones | Rendimiento y cantidad | Precios | Aplicación y técnicas | Productos específicos.
   - Sentimiento: Positivo | Neutro | Negativo.

3. **Datos de canal**
   - Identificador de canal en cada evento: WhatsApp | Web Chat | Facebook | Instagram.

4. **Integración con pedidos**
   - Eventos o API que permitan contar pedidos por estado, zona, tiempo de entrega y motivo de demora (para pedidos originados o gestionados por el bot).

5. **Métricas calculadas**
   - Disponibilidad (uptime), respuesta promedio, total interacciones, horas ahorradas y ahorro en ARS según fórmula de negocio.

Con estos eventos y clasificaciones habilitados, el dashboard puede mostrar todas las métricas descritas en este documento.

---

*Dashboard por [Savante](https://www.savante.dev/). Repositorio: [dashboard_demo_pintureria](https://github.com/sebastianjlopez/dashboard_demo_pintureria).*
