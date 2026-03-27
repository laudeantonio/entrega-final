# Calificación Automatizada de Leads (Lead Scoring)
Descripción del caso: Este flujo automatiza la recepción, evaluación y asignación de clientes potenciales (leads) para Siigo. El proceso comienza cuando un nuevo lead es recibido a través de un Webhook (por ejemplo, desde un formulario web)

Para garantizar la seguridad, el sistema extrae solo información no sensible (cargo, empresa, sector, etc.) y la envía a un Agente de IA (Google Gemini). La IA evalúa el lead basándose en criterios específicos (tamaño de empresa, sector, cargo y fuente) y asigna un puntaje de 0 a 100, clasificándolo en categorías HOT, WARM o COLD.

Posteriormente, el flujo consulta una base de datos de asesores en Supabase para encontrar a la persona disponible con menor carga de trabajo que coincida con la prioridad del lead. Finalmente, se envía un correo personalizado de bienvenida al lead y se actualiza una hoja de cálculo en Google Sheets con el estado "Contactado" y el asesor asignado.

* ## Explicación de los Nodos Principales*

**A. Recepción y Preparación de Datos**
Nodo: Recepción_lead (Webhook): Actúa como el trigger del flujo. Recibe las solicitudes POST con los datos del formulario de contacto.

Nodo: Extracción_información_no_sensible (Set): Filtra y organiza los datos necesarios para la IA (cargo, empresa, ciudad, fuente, industria y número de empleados), omitiendo intencionalmente datos personales como nombres o teléfonos por seguridad.

Nodo: Base_Datos_Sheets (Google Sheets):Registra inicialmente el lead en una hoja de cálculo con el estado "Creado".


**B. Inteligencia Artificial y Scoring**
Nodo: AI Agent (LangChain): Procesa la información del lead utilizando el modelo Google Gemini Chat.

Parámetros: Temperatura 0.4 para mantener respuestas consistentes y precisas.

Prompt (System Message): El agente tiene instrucciones estrictas para evaluar 4 señales (25 puntos c/u):

Tamaño de empresa: Basado en el número de empleados.

Sector: Alineación con el mercado objetivo de Siigo.

Cargo: Nivel de decisión del contacto.

Fuente: Intención de compra según el origen del lead.

*Formato de Salida: Devuelve un JSON con el score, el tier (HOT, WARM, COLD), un desglose (breakdown) y la razón del puntaje.*


**C. Clasificación y Asignación**
Nodo: Clasificador_Prioridad (Switch): Divide el flujo en tres ramas según el tier (HOT, WARM o COLD) para dar un tratamiento diferenciado a cada lead.

Nodos: Consulta_BD_Asesores_Activos (Supabase): Busca en la tabla asesores a aquellos que estén marcados como activos y cuya especialidad coincida con el tier del lead.

Nodo: Selección_Asesor (Code): Ejecuta un script en JavaScript que calcula la carga de trabajo de los asesores disponibles (leads_activos / capacidad_maxima). Selecciona automáticamente al asesor con menor porcentaje de carga para equilibrar el trabajo.


**D. Notificación y Cierre**
Nodos: Notificación_Ausencia_Asesor (Discord): Si no se encuentra ningún asesor activo para el tier correspondiente, envía una alerta urgente a Discord con los datos del lead para que un supervisor intervenga.

Nodo: Traductor_Ingles / Gmail_Confirmación: Genera un mensaje comercial personalizado y lo envía al lead vía Gmail. El correo incluye un botón para agendar una demo directamente en Calendly.

Nodo: Actualización_Estado_Sheets (Google Sheets): Actualiza la fila del lead con el nombre del asesor asignado, la razón del scoring y cambia el estado a "Contactado".
