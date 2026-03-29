# Calificación Automatizada de Leads (Lead Scoring)
Descripción del caso: Este flujo automatiza la recepción, evaluación y asignación de clientes potenciales (leads) para Siigo. El proceso comienza cuando un nuevo lead es recibido a través de un Webhook (inputs-formulario).

Para garantizar la seguridad, el sistema extrae solo información no sensible y la envía a un Agente de IA (Google Gemini). La IA evalúa el lead basándose en criterios específicos (tamaño de empresa, sector, cargo y fuente) y asigna un puntaje de 0 a 100, clasificándolo en categorías HOT, WARM o COLD.

Posteriormente, el flujo consulta una base de datos de asesores en Supabase para encontrar a la persona disponible con menor carga de trabajo que coincida con la prioridad del lead. Finalmente, se envía un correo personalizado de bienvenida al lead y se actualiza una hoja de cálculo en Google Sheets con el estado "Contactado" y el asesor asignado.

* ## Explicación de los Nodos Principales *

Webhook (Recepcion_lead): Actúa como el disparador del flujo al recibir los datos de nuevos prospectos desde formularios externos. Centraliza la entrada de información para iniciar el proceso de calificación de forma inmediata.

Google Sheets (Base_Datos_Sheets): Registra cada lead entrante en una fila de la base de datos con un estado inicial (creado). Permite mantener un historial de auditoría desde el primer momento en que el usuario interactúa con la marca.

Set (Extracción_información_no_sensible): Filtra los datos del webhook para enviar al motor de IA únicamente variables de negocio como industria y cargo. Esta capa asegura que la información personal identificable no sea procesada por modelos externos.

AI Agent (Agente_Scoring): Analiza el perfil del lead utilizando lógica de LangChain y Gemini para determinar su potencial de conversión. Devuelve un puntaje numérico y una categorización basada en reglas de negocio predefinidas.

Formateador_variable_tier (Set): Normaliza y estandariza la etiqueta de prioridad generada por la IA para asegurar la compatibilidad con los filtros subsiguientes.

Google Gemini Chat Model: Provee la inteligencia lingüística y lógica al agente para interpretar datos no estructurados. Su configuración de temperatura balancea la precisión técnica con la flexibilidad del análisis.

Switch (Clasificador_Prioridad): Segmenta el flujo en tres rutas distintas (Hot, Warm, Cold) dependiendo del resultado del scoring. Dirige cada oportunidad hacia el proceso de atención o nutrición que le corresponde.

Supabase (Consulta_BD_Asesores): Consulta en tiempo real la tabla de asesores activos para identificar quiénes están disponibles según su especialidad. Filtra los perfiles que coinciden con el nivel de prioridad del lead asignado.

¿Hay_Asesores_Activos? (Filter): Valida si la consulta a la base de datos retornó algún asesor disponible antes de proceder con la asignación. Actúa como un control de seguridad que desvía el flujo hacia una notificación de alerta si no existen agentes activos en ese momento.

Discord (Notificación_Ausencia_Asesor): Dispara una alerta de contingencia si no se encuentra un asesor disponible para un lead de alta prioridad. Garantiza que el equipo de supervisión pueda intervenir manualmente ante cualquier fallo en la asignación.

Code (Selección_Asesor): Ejecuta un script para comparar la carga de trabajo actual de los asesores disponibles. Selecciona automáticamente al asesor con menos tareas activas para optimizar el tiempo de respuesta.

Datos_Correo_Lead (Set): Consolida la información final del lead, incluyendo su nombre y los datos de contacto, para estructurar el cuerpo del mensaje que se enviará. Prepara las variables necesarias para que el nodo de correo pueda realizar una personalización precisa antes del envío.

Google Translate (Traductor_Ingles): Adapta automáticamente el mensaje comercial al idioma inglés para estandarizar la comunicación internacional. Asegura que la propuesta de valor sea clara y profesional antes de ser enviada al destinatario.

Gmail (Gmail_Confirmación_Recibido): Realiza el envío del correo electrónico personalizado que incluye la invitación a agendar mediante Calendly. Conecta al lead directamente con el asesor asignado para cerrar la brecha de contacto.

Google Sheets (Actualización_Estado_Sheets): Modifica la fila original del lead para marcarlo como "Contactado" e incluir el nombre del asesor responsable. Cierra el ciclo de automatización asegurando la integridad y actualización de la base de datos.
