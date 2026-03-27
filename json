{
  "name": "Sistem Lead Scoring✅",
  "nodes": [
    {
      "parameters": {
        "options": {
          "temperature": 0.4
        }
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGoogleGemini",
      "typeVersion": 1,
      "position": [
        -2560,
        1120
      ],
      "id": "5a339aa0-f213-4c25-a5af-c6e3babeb3ce",
      "name": "Google Gemini Chat Model",
      "credentials": {
        "googlePalmApi": {
          "id": "8jLaEVULqwm4LpAw",
          "name": "Google Gemini(PaLM) Api account"
        }
      }
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "={{ $json.body }}",
        "options": {
          "systemMessage": "Eres un agente especializado en calificación de leads B2B para Siigo, empresa de software contable colombiana que atiende PyMEs, medianas empresas y contadores independientes en Latinoamérica.\n\nTu única función es evaluar leads entrantes y asignarles un score de 0 a 100 basado en su potencial de conversión. \n\nNo tienes memoria entre llamadas. \n\nCada evaluación es independiente.\n\n<CRITERIOS DE SCORING> \n\nEvalúa exactamente 4 señales. Cada señal tiene un peso fijo. La suma siempre debe ser 100.\n\n<Señal 1>\nSeñal 1: Tamaño de empresa (peso: 25 puntos)\nUsa el campo employee_count. \n\nEmpleados\nPuntos\n> 200=25\n101 – 200 =20\n21 – 100 = 15\n5 – 20 = 8\n< 5 o desconocido =3\n</Señal 1>\n\n<Señal 2>\nSeñal 2: Sector de la empresa (peso: 25 puntos)\nEvalúa qué tan alineado está el sector con el mercado objetivo de Siigo.\nSector\nPuntos\nSoftware, Tecnología, Finanzas, Contabilidad=25\nRetail, Comercio, Distribución =22\nSalud, Educación, Servicios profesionales=18\nManufactura, Construcción, Agro= 13\nGobierno, ONG, Otro o desconocido=7\n</Señal 2>\n\n<Señal 3>\nSeñal 3: Cargo del contacto (peso: 25 puntos)\nEvalúa el nivel de decisión del contacto dentro de su empresa.\nCargo\nPuntos\nCEO, Gerente General, Director, Dueño, Propietario= 25\nCFO, Director Financiero, Contador General, Controller=23\nGerente Administrativo, Gerente Financiero, Jefe de Contable.=18\nCoordinador, Analista, Asistente Contable = 10\nDesconocido o no relacionado con finanzas/decisión= 4\n</Señal 3>\n\n<Señal 4>\nSeñal 4: Fuente del lead (peso: 25 puntos)\nEvalúa la intención de compra implícita según cómo llegó el lead.\nFuente\nPuntos\nlead activo = 25\nprograma referidos= 24\nformulario_web= 20\ngoogle_ads= 18\nlinkedin= 14\nferias (eventos y ferias)= 10\ndesconocido= 5\nSin contexto de origen= 0\n</Señal 4>\n\n</CRITERIOS DE SCORING> \n\n<CLASIFICACIÓN EN TIERS> \nDespués de calcular el score total, clasifica el lead en uno de estos tres tiers:\nHOT: score >= 71.  Alta probabilidad de conversión.\nWARM: score entre 40 y 70 inclusive. Potencial con nurturing.\nCOLD: score <= 39.Bajo potencial inmediato.\n</CLASIFICACIÓN EN TIERS> \n\n<MANEJO DE DATOS FALTANTES> \nNunca inventes datos. Si un campo está vacío, null o es \"desconocido\":\nUsa la puntuación mínima de ese criterio según la tabla.\nIndica en el campo \"datos_faltantes\" qué campos no estaban disponibles.\nEl score puede ser bajo por datos incompletos. Eso es correcto y esperado.\nSi el nombre de la empresa o el contacto están completamente vacíos, devuelve score 0 y tier COLD con razon \"datos_insuficientes_para_evaluar\".\n</MANEJO DE DATOS FALTANTES> \n\n<FORMATO DE RESPUESTA> \nResponde ÚNICAMENTE con un objeto JSON válido. Sin texto antes ni después. Sin bloques de código. Sin explicaciones adicionales. El JSON debe tener exactamente esta estructura:\n{ \"score\": <número entero entre 0 y 100>, \"tier\": \"<HOT | WARM | COLD>\", \"breakdown\": { \"tamano_empresa\": <número entero entre 0 y 25>, \"sector\": <número entero entre 0 y 25>, \"cargo_contacto\": <número entero entre 0 y 25>, \"fuente\": <número entero entre 0 y 25> }, \"razon\": \"<explicación breve en español de máximo 2 oraciones justificando el score>\", \"datos_faltantes\": [\"<campo1>\", \"<campo2>\"], \"confianza\": \"<ALTA | MEDIA | BAJA>\" }\nReglas del JSON:\nLa suma de breakdown.tamano_empresa + breakdown.sector + breakdown.cargo_contacto + breakdown.fuente debe ser exactamente igual a score.\ndatos_faltantes es un array vacío [] si todos los campos estaban disponibles.\nconfianza es ALTA si todos los campos estaban disponibles, MEDIA si faltaba uno, BAJA si faltaban dos o más.\nrazon debe estar en español, ser concisa y mencionar el factor más determinante del score.\nNunca uses comillas simples en el JSON. Siempre comillas dobles.\nNunca incluyas comas finales en arrays u objetos. \n</FORMATO DE RESPUESTA> \n\n"
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 3.1,
      "position": [
        -2560,
        944
      ],
      "id": "910d6009-de54-4d53-8655-3e01342471ce",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "content": "## Calificación Inteligente de Leads\n\n**Función:**\nAnalizar el perfil de los prospectos entrantes para determinar su nivel de madurez y probabilidad de conversión, asignando un puntaje numérico de 0 a 100.\n\n**Criterios:**\nEl puntaje se calcula mediante el análisis de cuatro variables clave (señales), cada una con un peso del 25% sobre el total:\n\n- Señal 1: Tamaño de empresa\n- Señal 2: Sector de la empresa\n- Señal 3: Cargo del contacto\n- Señal 4: Fuente del lead\n\n\n**Clasificación en Tiers:**\n\n- Una vez obtenido el score final, el sistema clasifica el lead en uno de los siguientes niveles de prioridad:\n\nHOT: score >= 71.  Alta probabilidad de conversión.\nWARM: score entre 40 y 70 inclusive. Potencial con nurturing.\nCOLD: score <= 39.Bajo potencial inmediato.",
        "height": 1248,
        "width": 576,
        "color": 7
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        -2624,
        208
      ],
      "typeVersion": 1,
      "id": "98371ab7-ea6c-4715-a376-2716ada0bae7",
      "name": "Sticky Note"
    },
    {
      "parameters": {
        "content": "## Input\n{\n  \"name\": \"Matt Murphy\",\n  \"email\": \"jmoreno@empresa.com\",\n  \"phone\": \"+13124445566\",\n  \"cargo\": \"Commercial leader\",\n  \"company\": \"Investments SA\",\n  \"city\": \"Miami\",\n  \"source\": \"linkedin\",\n  \"industry\": \"manufacture\",\n  \"employee_count\": \"100-150\"\n}",
        "height": 1248,
        "color": 7
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        -3200,
        208
      ],
      "typeVersion": 1,
      "id": "78e45ac5-a212-40a0-a18a-4eeef3d15ced",
      "name": "Sticky Note1"
    },
    {
      "parameters": {
        "content": "## Seguridad y Privacidad de Datos\nSe transfieren al Agente de IA únicamente los atributos necesarios para la categorización (cargo, industria, tamaño de empresa). Se omiten deliberadamente datos de carácter personal como nombre, teléfono y correo electrónico para garantizar el cumplimiento de políticas de privacidad.",
        "height": 1248,
        "color": 7
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        -2912,
        208
      ],
      "typeVersion": 1,
      "id": "da5c8f69-336e-4db0-b13c-33ab71669e1c",
      "name": "Sticky Note2"
    },
    {
      "parameters": {
        "content": "## Asignación Dinámica de Asesores\n\nGarantizar que cada lead sea gestionado por el asesor más idóneo, optimizando los tiempos de respuesta y equilibrando la carga de trabajo del equipo comercial.\n\n1. El sistema consulta la base de datos de asesores en Supabase para identificar perfiles cuyo enfoque coincida con el tipo de Tier que fue asignado el Lead.\n\n2. Mediante un nodo de Código (JavaScript), se analizan los asesores disponibles y se calcula su saturación actual. El sistema selecciona automáticamente al asesor que tenga el menor número de chats/leads activos, evitando cuellos de botella y garantizando una distribución equitativa.\n\n3. En caso de que no se identifique ningún asesor activo o disponible para el perfil del lead, el flujo activa una alerta inmediata vía Discord.\n\n",
        "height": 1248,
        "width": 1392,
        "color": 7
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        -2000,
        208
      ],
      "typeVersion": 1,
      "id": "2bf1e33f-cd05-4e2e-8963-8708b422cec5",
      "name": "Sticky Note3"
    },
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "Formulario-lead",
        "options": {}
      },
      "id": "42088924-9652-4adc-bcb0-3a05c20a9c3f",
      "name": "Recepción_lead",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1,
      "position": [
        -3152,
        656
      ],
      "webhookId": "4cc7e281-e1ef-4c77-bc8a-49e0117cf512",
      "retryOnFail": true
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "423ff50d-4b69-48dd-bcdb-dff700e4c316",
              "name": "body.cargo",
              "value": "={{ $json.cargo }}",
              "type": "string"
            },
            {
              "id": "bb46bffb-d509-4c00-a4d0-90461d20dcae",
              "name": "body.company",
              "value": "={{ $json.empresa }}",
              "type": "string"
            },
            {
              "id": "dc056e87-c240-4b38-9503-1d7136645b15",
              "name": "body.city",
              "value": "={{ $json.ciudad }}",
              "type": "string"
            },
            {
              "id": "9eeaad7e-e309-4c8d-8a45-48b99bd8325e",
              "name": "body.source",
              "value": "={{ $json.fuente }}",
              "type": "string"
            },
            {
              "id": "4ab3b945-cb81-4679-94e8-1652246112f6",
              "name": "body.industry",
              "value": "={{ $('Recepción_lead').item.json.body.industry }}",
              "type": "string"
            },
            {
              "id": "383beb96-515f-4f9c-b8f5-fc90ff2ccc25",
              "name": "body.employee_count",
              "value": "={{ $('Recepción_lead').item.json.body.employee_count }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -2832,
        944
      ],
      "id": "38e1e66b-fe4f-4a16-8b57-2939d519c971",
      "name": "Extracción_información_no_sensible"
    },
    {
      "parameters": {
        "jsCode": "const raw = $input.first().json.output;\nconst cleaned = raw.replace(/```json/g, '').replace(/```/g, '').trim();\nconst parsed = JSON.parse(cleaned);\n\nreturn [{\n  json: {\n    score: parsed.score,\n    tier: parsed.tier,\n    tamano_empresa: parsed.breakdown.tamano_empresa,\n    sector: parsed.breakdown.sector,\n    cargo_contacto: parsed.breakdown.cargo_contacto,\n    fuente: parsed.breakdown.fuente,\n    razon: parsed.razon,\n    datos_faltantes: parsed.datos_faltantes,\n    confianza: parsed.confianza\n  }\n}];"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        -2208,
        944
      ],
      "id": "0762dff7-e39b-47ae-ad0e-18504f21eb55",
      "name": "Formateador_variable_tier"
    },
    {
      "parameters": {
        "rules": {
          "values": [
            {
              "conditions": {
                "options": {
                  "caseSensitive": true,
                  "leftValue": "",
                  "typeValidation": "strict",
                  "version": 3
                },
                "conditions": [
                  {
                    "id": "5491f577-5e26-410e-959c-d6631e34952c",
                    "leftValue": "={{ $json.tier }}",
                    "rightValue": "HOT",
                    "operator": {
                      "type": "string",
                      "operation": "equals",
                      "name": "filter.operator.equals"
                    }
                  }
                ],
                "combinator": "and"
              },
              "renameOutput": true,
              "outputKey": "HOT"
            },
            {
              "conditions": {
                "options": {
                  "caseSensitive": true,
                  "leftValue": "",
                  "typeValidation": "strict",
                  "version": 3
                },
                "conditions": [
                  {
                    "leftValue": "={{ $json.tier }}",
                    "rightValue": "WARM",
                    "operator": {
                      "type": "string",
                      "operation": "equals"
                    },
                    "id": "d55b749f-60c7-4c12-bc16-e3202acf2666"
                  }
                ],
                "combinator": "and"
              },
              "renameOutput": true,
              "outputKey": "WARM"
            },
            {
              "conditions": {
                "options": {
                  "caseSensitive": true,
                  "leftValue": "",
                  "typeValidation": "strict",
                  "version": 3
                },
                "conditions": [
                  {
                    "id": "b64fa438-93e6-4a2a-a2ba-03e48eb9fdb0",
                    "leftValue": "={{ $json.tier }}",
                    "rightValue": "COLD",
                    "operator": {
                      "type": "string",
                      "operation": "equals"
                    }
                  }
                ],
                "combinator": "and"
              },
              "renameOutput": true,
              "outputKey": "COLD"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.switch",
      "typeVersion": 3.4,
      "position": [
        -1856,
        752
      ],
      "id": "3c0ca3aa-27a6-4548-9b41-1686038a3838",
      "name": "Clasificador_Prioridad"
    },
    {
      "parameters": {
        "operation": "getAll",
        "tableId": "asesores",
        "matchType": "allFilters",
        "filters": {
          "conditions": [
            {
              "keyName": "Score",
              "condition": "eq",
              "keyValue": "={{ $json.tier }}"
            },
            {
              "keyName": "activo",
              "condition": "eq",
              "keyValue": "TRUE"
            }
          ]
        }
      },
      "type": "n8n-nodes-base.supabase",
      "typeVersion": 1,
      "position": [
        -1568,
        544
      ],
      "id": "cf391543-371e-4559-bfd5-a05dc5fcbba1",
      "name": "Consulta_BD_Asesores_Activos",
      "alwaysOutputData": true,
      "credentials": {
        "supabaseApi": {
          "id": "RrBNPtYsFdFIja99",
          "name": "Supabase inventario"
        }
      }
    },
    {
      "parameters": {
        "operation": "getAll",
        "tableId": "asesores",
        "matchType": "allFilters",
        "filters": {
          "conditions": [
            {
              "keyName": "Score",
              "condition": "eq",
              "keyValue": "={{ $json.tier }}"
            },
            {
              "keyName": "activo",
              "condition": "eq",
              "keyValue": "TRUE"
            }
          ]
        }
      },
      "type": "n8n-nodes-base.supabase",
      "typeVersion": 1,
      "position": [
        -1568,
        768
      ],
      "id": "c2dcb75c-d4e6-49e1-b70f-e0193650a235",
      "name": "Consulta_BD_Asesores_Activos1",
      "alwaysOutputData": true,
      "credentials": {
        "supabaseApi": {
          "id": "RrBNPtYsFdFIja99",
          "name": "Supabase inventario"
        }
      }
    },
    {
      "parameters": {
        "operation": "getAll",
        "tableId": "asesores",
        "filters": {
          "conditions": [
            {
              "keyName": "Score",
              "condition": "eq",
              "keyValue": "={{ $json.tier }}"
            },
            {
              "keyName": "activo",
              "condition": "eq",
              "keyValue": "TRUE"
            }
          ]
        }
      },
      "type": "n8n-nodes-base.supabase",
      "typeVersion": 1,
      "position": [
        -1568,
        992
      ],
      "id": "b041cb18-83fd-43db-8606-0bacb369d9fd",
      "name": "Consulta_BD_Asesores_Activos2",
      "alwaysOutputData": true,
      "credentials": {
        "supabaseApi": {
          "id": "RrBNPtYsFdFIja99",
          "name": "Supabase inventario"
        }
      }
    },
    {
      "parameters": {
        "conditions": {
          "options": {
            "caseSensitive": true,
            "leftValue": "",
            "typeValidation": "strict",
            "version": 3
          },
          "conditions": [
            {
              "id": "d26efe96-18a7-4ad7-93ea-382201ece05a",
              "leftValue": "={{ $json.asesor_id }}",
              "rightValue": "",
              "operator": {
                "type": "string",
                "operation": "exists",
                "singleValue": true
              }
            }
          ],
          "combinator": "and"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.if",
      "typeVersion": 2.3,
      "position": [
        -1328,
        544
      ],
      "id": "78b82497-bce8-4efa-b519-b33a891f9b72",
      "name": "¿Hay_Asesores_Activos?"
    },
    {
      "parameters": {
        "conditions": {
          "options": {
            "caseSensitive": true,
            "leftValue": "",
            "typeValidation": "strict",
            "version": 3
          },
          "conditions": [
            {
              "id": "9b0df80d-e619-40d7-836d-dac455a590b9",
              "leftValue": "={{ $json.asesor_id }}",
              "rightValue": "NULL",
              "operator": {
                "type": "string",
                "operation": "exists",
                "singleValue": true
              }
            }
          ],
          "combinator": "and"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.if",
      "typeVersion": 2.3,
      "position": [
        -1328,
        768
      ],
      "id": "7c8e87a0-9f00-468f-b06c-a4dc7bf7e57a",
      "name": "¿Hay_Asesores_Activos?1"
    },
    {
      "parameters": {
        "conditions": {
          "options": {
            "caseSensitive": true,
            "leftValue": "",
            "typeValidation": "strict",
            "version": 3
          },
          "conditions": [
            {
              "id": "8e92f47a-cebe-4bde-8969-ee62856b3f76",
              "leftValue": "={{ $json.asesor_id }}",
              "rightValue": "",
              "operator": {
                "type": "string",
                "operation": "exists",
                "singleValue": true
              }
            }
          ],
          "combinator": "and"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.if",
      "typeVersion": 2.3,
      "position": [
        -1328,
        992
      ],
      "id": "5b294ecc-2556-4ead-b0ba-e49b0159daca",
      "name": "¿Hay_Asesores_Activos?2"
    },
    {
      "parameters": {
        "authentication": "webhook",
        "content": "=:sos: Urgente :sos:\nNo tienes ningun asesor activo para recibir el lead HOT.\n\nLos datos del lead son:\n{{ $('Recepción_lead').item.json.body.name }}\n{{ $('Recepción_lead').item.json.body.phone }}\n{{ $('Recepción_lead').item.json.body.company }}",
        "options": {}
      },
      "type": "n8n-nodes-base.discord",
      "typeVersion": 2,
      "position": [
        -1088,
        640
      ],
      "id": "088af299-8a0c-4f5e-97be-3cadaac15368",
      "name": "Notificación_Ausencia_Asesor",
      "webhookId": "6dcdb4ee-bcf7-4326-8324-92e12fd27197",
      "credentials": {
        "discordWebhookApi": {
          "id": "WF2f6F4kkTsMfhRc",
          "name": "Discord Webhook account"
        }
      }
    },
    {
      "parameters": {
        "authentication": "webhook",
        "content": "=:eyes: Importante\nNo tienes ningun asesor activo para recibir el lead WARM.\n\nLos datos del lead son:\n{{ $('Recepción_lead').item.json.body.name }}\n{{ $('Recepción_lead').item.json.body.phone }}\n{{ $('Recepción_lead').item.json.body.company }}",
        "options": {}
      },
      "type": "n8n-nodes-base.discord",
      "typeVersion": 2,
      "position": [
        -1088,
        864
      ],
      "id": "19ec111f-dbce-4451-95fd-9ac9218f6349",
      "name": "Notificación_Ausencia_Asesor1",
      "webhookId": "3ead5f7a-abad-490e-840e-fe036bc64418",
      "credentials": {
        "discordWebhookApi": {
          "id": "WF2f6F4kkTsMfhRc",
          "name": "Discord Webhook account"
        }
      }
    },
    {
      "parameters": {
        "authentication": "webhook",
        "content": "=Urgente, no tienes ningun asesor activo para recibir el lead WARM.\n\nLos datos del lead son:\n{{ $('Recepción_lead').item.json.body.name }}\n{{ $('Recepción_lead').item.json.body.phone }}\n{{ $('Recepción_lead').item.json.body.company }}",
        "options": {}
      },
      "type": "n8n-nodes-base.discord",
      "typeVersion": 2,
      "position": [
        -1088,
        1088
      ],
      "id": "78377fe0-ff99-4f97-ab12-9e3dc2ab11df",
      "name": "Notificación_Ausencia_Asesor2",
      "webhookId": "af8b2c6f-3e29-4ab9-b795-002ea5a3fcc3",
      "credentials": {
        "discordWebhookApi": {
          "id": "WF2f6F4kkTsMfhRc",
          "name": "Discord Webhook account"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "// Obtener todos los asesores del output anterior\nconst asesores = $input.all().map(item => item.json);\n\n// 1. Filtrar solo asesores activos\nconst activos = asesores.filter(a => a.activo === true);\n\n// 2. Calcular carga: leads_activos / capacidad_maxima_leads\n// El que tenga menor ratio = más disponible\nconst conCarga = activos.map(a => ({\n  ...a,\n  carga: a.leads_activos / a.capacidad_maxima_leads\n}));\n\n// 3. Seleccionar el de menor carga\nconst seleccionado = conCarga.reduce((min, a) => \n  a.carga < min.carga ? a : min\n);\n\nreturn [{\n  json: {\n    nombre: seleccionado.nombre_completo,\n    celular: seleccionado.telefono,\n    asesor_id: seleccionado.asesor_id,\n    leads_activos: seleccionado.leads_activos,\n    capacidad_maxima_leads: seleccionado.capacidad_maxima_leads,\n    carga_porcentaje: Math.round(seleccionado.carga * 100) + \"%\"\n  }\n}];"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        -800,
        752
      ],
      "id": "09c6fb9a-ab67-48ca-8c4c-e8bcb03f7cbe",
      "name": "Selección_Asesor"
    },
    {
      "parameters": {
        "jsCode": "// Obtener todos los asesores del output anterior\nconst asesores = $input.all().map(item => item.json);\n\n// 1. Filtrar solo asesores activos\nconst activos = asesores.filter(a => a.activo === true);\n\n// 2. Calcular carga: leads_activos / capacidad_maxima_leads\n// El que tenga menor ratio = más disponible\nconst conCarga = activos.map(a => ({\n  ...a,\n  carga: a.leads_activos / a.capacidad_maxima_leads\n}));\n\n// 3. Seleccionar el de menor carga\nconst seleccionado = conCarga.reduce((min, a) => \n  a.carga < min.carga ? a : min\n);\n\nreturn [{\n  json: {\n    nombre: seleccionado.nombre_completo,\n    celular: seleccionado.telefono,\n    asesor_id: seleccionado.asesor_id,\n    leads_activos: seleccionado.leads_activos,\n    capacidad_maxima_leads: seleccionado.capacidad_maxima_leads,\n    carga_porcentaje: Math.round(seleccionado.carga * 100) + \"%\"\n  }\n}];"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        -800,
        976
      ],
      "id": "3094d3e2-509c-49bb-879b-a17447e8d429",
      "name": "Selección_Asesor1"
    },
    {
      "parameters": {
        "jsCode": "// Obtener todos los asesores del output anterior\nconst asesores = $input.all().map(item => item.json);\n\n// 1. Filtrar solo asesores activos\nconst activos = asesores.filter(a => a.activo === true);\n\n// 2. Calcular carga: leads_activos / capacidad_maxima_leads\n// El que tenga menor ratio = más disponible\nconst conCarga = activos.map(a => ({\n  ...a,\n  carga: a.leads_activos / a.capacidad_maxima_leads\n}));\n\n// 3. Seleccionar el de menor carga\nconst seleccionado = conCarga.reduce((min, a) => \n  a.carga < min.carga ? a : min\n);\n\nreturn [{\n  json: {\n    nombre: seleccionado.nombre_completo,\n    celular: seleccionado.telefono,\n    asesor_id: seleccionado.asesor_id,\n    leads_activos: seleccionado.leads_activos,\n    capacidad_maxima_leads: seleccionado.capacidad_maxima_leads,\n    carga_porcentaje: Math.round(seleccionado.carga * 100) + \"%\"\n  }\n}];"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        -800,
        528
      ],
      "id": "e142c1d1-defb-4f85-8df2-b184615ca7e0",
      "name": "Selección_Asesor2"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "b8087d6e-fc18-4513-a063-01e4d3426a9b",
              "name": "body.name",
              "value": "={{ $('Recepción_lead').first().json.body.name }}",
              "type": "string"
            },
            {
              "id": "a95e8fb7-82b4-43e9-a157-0697c594013d",
              "name": "body.email",
              "value": "={{ $('Recepción_lead').first().json.body.email }}",
              "type": "string"
            },
            {
              "id": "6064e446-b6af-4748-9a56-8185c2f9436d",
              "name": "body.company",
              "value": "={{ $('Recepción_lead').first().json.body.company }}",
              "type": "string"
            },
            {
              "id": "488ea1f4-786e-4254-a487-468fe7d71ba8",
              "name": "nombre.asesor",
              "value": "={{ $json.nombre }}",
              "type": "string"
            },
            {
              "id": "48786785-e7da-4aec-b5be-b60e5ece722e",
              "name": "celular.asesor",
              "value": "={{ $json.celular }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -352,
        464
      ],
      "id": "3c836e97-b439-4bbd-90d6-40d628aa1e7c",
      "name": "Datos_Correo_Lead1"
    },
    {
      "parameters": {
        "sendTo": "={{ $('Datos_Correo_Lead1').item.json.body.email }}",
        "subject": "Siigo - 🛡️ Accounting and administrative automation",
        "message": "=<div style=\"font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; line-height: 1.6; color: #333333; max-width: 600px; margin: auto; border: 1px solid #e0e0e0; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 10px rgba(0,0,0,0.05);\">\n  \n  <div style=\"background-color: #0047AB; color: white; padding: 30px; text-align: center;\">\n    <h2 style=\"margin: 0; font-size: 24px; letter-spacing: 0.5px;\">Soluciones Estratégicas B2B</h2>\n    <p style=\"margin: 5px 0 0 0; opacity: 0.9; font-size: 14px;\">Impulsando el crecimiento de tu empresa</p>\n  </div>\n\n  <div style=\"padding: 30px; background-color: #ffffff;\">\n    \n    <div style=\"white-space: pre-wrap; font-size: 15px; color: #444444;\">\n{{ $json.output }}\n    </div>\n\n    <div style=\"margin-top: 30px; text-align: center;\">\n      <a href=\"https://calendly.com/amalia-backup4/demo-siigo\" \n         style=\"background-color: #0047AB; color: white; padding: 12px 25px; text-decoration: none; border-radius: 5px; font-weight: bold; display: inline-block;\">\n         Agendar Demo en Calendly\n      </a>\n    </div>\n  </div>\n\n  <div style=\"background-color: #f4f7fa; color: #777777; padding: 20px; text-align: center; font-size: 12px; border-top: 1px solid #eeeeee;\">\n    <p style=\"margin: 0;\">© 2026 Siigo SAS. Todos los derechos reservados.</p>\n    <p style=\"margin: 5px 0 0 0;\">Este es un mensaje de acercamiento comercial personalizado.</p>\n  </div>\n</div>",
        "options": {}
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.2,
      "position": [
        256,
        464
      ],
      "id": "e7efeb51-0e65-4c51-92de-ca5605cbad36",
      "name": "Gmail_Confirmación_Recibido1",
      "webhookId": "d5fac561-5f61-4674-8c26-860ad81041b6",
      "credentials": {
        "gmailOAuth2": {
          "id": "nOuqCnbBSPV0Jeqq",
          "name": "Gmail account"
        }
      }
    },
    {
      "parameters": {
        "operation": "append",
        "documentId": {
          "__rl": true,
          "value": "1atURXTNZsoC8rgBylTK5aw5-LK8C14PmddcpemJLZ_o",
          "mode": "list",
          "cachedResultName": "Lead scoring",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1atURXTNZsoC8rgBylTK5aw5-LK8C14PmddcpemJLZ_o/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Leads",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1atURXTNZsoC8rgBylTK5aw5-LK8C14PmddcpemJLZ_o/edit#gid=0"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Nombre": "={{ $json.body.name }}",
            "email": "={{ $json.body.email }}",
            "empresa": "={{ $json.body.company }}",
            "cargo": "={{ $json.body.cargo }}",
            "ciudad": "={{ $json.body.city }}",
            "telefono": "={{ $json.body.phone }}",
            "fuente": "={{ $json.body.source }}",
            "fecha_creacion": "={{ $now }}",
            "estado": "Creado"
          },
          "matchingColumns": [
            "id"
          ],
          "schema": [
            {
              "id": "Nombre",
              "displayName": "Nombre",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "empresa",
              "displayName": "empresa",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "cargo",
              "displayName": "cargo",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "email",
              "displayName": "email",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "telefono",
              "displayName": "telefono",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "ciudad",
              "displayName": "ciudad",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "pais",
              "displayName": "pais",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "fuente",
              "displayName": "fuente",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "fecha_creacion",
              "displayName": "fecha_creacion",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "fecha_actualización",
              "displayName": "fecha_actualización",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "estado",
              "displayName": "estado",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "asesor_asignado",
              "displayName": "asesor_asignado",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "score_inicial",
              "displayName": "score_inicial",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "notas",
              "displayName": "notas",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        -3120,
        944
      ],
      "id": "8d37019f-83dd-4ac7-9dae-c3dfa92c1c84",
      "name": "Base_Datos_Sheets",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "4s639T2GmUGuTGTv",
          "name": "Google Sheets account"
        }
      }
    },
    {
      "parameters": {
        "content": "## Comunicación Personalizada en ingles y Cierre de Ciclo\n\n-Gestionar la respuesta automática hacia el prospecto y asegurar que toda la gestión quede debidamente documentada en los sistemas de registro.\n",
        "height": 1248,
        "width": 1392,
        "color": 7
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        -560,
        208
      ],
      "typeVersion": 1,
      "id": "bd94589d-d54e-40d3-b8ec-91cf4ffb4341",
      "name": "Sticky Note4"
    },
    {
      "parameters": {
        "operation": "update",
        "documentId": {
          "__rl": true,
          "value": "1atURXTNZsoC8rgBylTK5aw5-LK8C14PmddcpemJLZ_o",
          "mode": "list",
          "cachedResultName": "Lead scoring",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1atURXTNZsoC8rgBylTK5aw5-LK8C14PmddcpemJLZ_o/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Leads",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1atURXTNZsoC8rgBylTK5aw5-LK8C14PmddcpemJLZ_o/edit#gid=0"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Nombre": "={{ $('Datos_Correo_Lead3').item.json.body.name }}",
            "estado": "Contactado",
            "asesor_asignado": "={{ $('Datos_Correo_Lead3').item.json.nombre.asesor }}",
            "notas": "={{ $('Clasificador_Prioridad').first().json.razon }}\n",
            "score_inicial": "={{ $('Clasificador_Prioridad').first().json.razon }}",
            "fecha_actualización": "={{ $now }}",
            "row_number": 0
          },
          "matchingColumns": [
            "Nombre"
          ],
          "schema": [
            {
              "id": "Nombre",
              "displayName": "Nombre",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "empresa",
              "displayName": "empresa",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "cargo",
              "displayName": "cargo",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "email",
              "displayName": "email",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "telefono",
              "displayName": "telefono",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "ciudad",
              "displayName": "ciudad",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "pais",
              "displayName": "pais",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "fuente",
              "displayName": "fuente",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "fecha_creacion",
              "displayName": "fecha_creacion",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "fecha_actualización",
              "displayName": "fecha_actualización",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "estado",
              "displayName": "estado",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "asesor_asignado",
              "displayName": "asesor_asignado",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "score_inicial",
              "displayName": "score_inicial",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "notas",
              "displayName": "notas",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "row_number",
              "displayName": "row_number",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "number",
              "canBeUsedToMatch": true,
              "readOnly": true,
              "removed": false
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        512,
        1136
      ],
      "id": "4a8c3b25-e207-428f-bf92-b10b6af9aa8e",
      "name": "Actualización_Estado_Sheets3",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "4s639T2GmUGuTGTv",
          "name": "Google Sheets account"
        }
      }
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "b8087d6e-fc18-4513-a063-01e4d3426a9b",
              "name": "body.name",
              "value": "={{ $('Recepción_lead').first().json.body.name }}",
              "type": "string"
            },
            {
              "id": "a95e8fb7-82b4-43e9-a157-0697c594013d",
              "name": "body.email",
              "value": "={{ $('Recepción_lead').first().json.body.email }}",
              "type": "string"
            },
            {
              "id": "6064e446-b6af-4748-9a56-8185c2f9436d",
              "name": "body.company",
              "value": "={{ $('Recepción_lead').first().json.body.company }}",
              "type": "string"
            },
            {
              "id": "488ea1f4-786e-4254-a487-468fe7d71ba8",
              "name": "nombre.asesor",
              "value": "={{ $json.nombre }}",
              "type": "string"
            },
            {
              "id": "48786785-e7da-4aec-b5be-b60e5ece722e",
              "name": "celular.asesor",
              "value": "={{ $json.celular }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -352,
        1136
      ],
      "id": "63697a3e-8fa9-403f-ae10-5733355aecd2",
      "name": "Datos_Correo_Lead3"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "b8087d6e-fc18-4513-a063-01e4d3426a9b",
              "name": "body.name",
              "value": "={{ $('Recepción_lead').first().json.body.name }}",
              "type": "string"
            },
            {
              "id": "a95e8fb7-82b4-43e9-a157-0697c594013d",
              "name": "body.email",
              "value": "={{ $('Recepción_lead').first().json.body.email }}",
              "type": "string"
            },
            {
              "id": "6064e446-b6af-4748-9a56-8185c2f9436d",
              "name": "body.company",
              "value": "={{ $('Recepción_lead').first().json.body.company }}",
              "type": "string"
            },
            {
              "id": "488ea1f4-786e-4254-a487-468fe7d71ba8",
              "name": "nombre.asesor",
              "value": "={{ $json.nombre }}",
              "type": "string"
            },
            {
              "id": "48786785-e7da-4aec-b5be-b60e5ece722e",
              "name": "celular.asesor",
              "value": "={{ $json.celular }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -352,
        816
      ],
      "id": "6201cae7-21ca-474c-a713-a7c3c68a9e6a",
      "name": "Datos_Correo_Lead2"
    },
    {
      "parameters": {
        "sendTo": "={{ $('Datos_Correo_Lead3').item.json.body.email }}",
        "subject": "Siigo - 🛡️ Accounting and administrative automation",
        "message": "=<div style=\"font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; line-height: 1.6; color: #333333; max-width: 600px; margin: auto; border: 1px solid #e0e0e0; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 10px rgba(0,0,0,0.05);\">\n  \n  <div style=\"background-color: #0047AB; color: white; padding: 30px; text-align: center;\">\n    <h2 style=\"margin: 0; font-size: 24px; letter-spacing: 0.5px;\">Soluciones Estratégicas B2B</h2>\n    <p style=\"margin: 5px 0 0 0; opacity: 0.9; font-size: 14px;\">Impulsando el crecimiento de tu empresa</p>\n  </div>\n\n  <div style=\"padding: 30px; background-color: #ffffff;\">\n    \n    <div style=\"white-space: pre-wrap; font-size: 15px; color: #444444;\">\n{{ $json.output }}\n    </div>\n\n    <div style=\"margin-top: 30px; text-align: center;\">\n      <a href=\"https://calendly.com/amalia-backup4/demo-siigo\" \n         style=\"background-color: #0047AB; color: white; padding: 12px 25px; text-decoration: none; border-radius: 5px; font-weight: bold; display: inline-block;\">\n         Agendar Demo en Calendly\n      </a>\n    </div>\n  </div>\n\n  <div style=\"background-color: #f4f7fa; color: #777777; padding: 20px; text-align: center; font-size: 12px; border-top: 1px solid #eeeeee;\">\n    <p style=\"margin: 0;\">© 2026 Siigo SAS. Todos los derechos reservados.</p>\n    <p style=\"margin: 5px 0 0 0;\">Este es un mensaje de acercamiento comercial personalizado.</p>\n  </div>\n</div>",
        "options": {}
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.2,
      "position": [
        256,
        1136
      ],
      "id": "4af55add-0919-4092-bb9e-ccc2570cc15f",
      "name": "Gmail_Confirmación_Recibido3",
      "webhookId": "de0ef5ac-f309-46d1-a21d-be1e071b215a",
      "credentials": {
        "gmailOAuth2": {
          "id": "nOuqCnbBSPV0Jeqq",
          "name": "Gmail account"
        }
      }
    },
    {
      "parameters": {
        "operation": "update",
        "documentId": {
          "__rl": true,
          "value": "1atURXTNZsoC8rgBylTK5aw5-LK8C14PmddcpemJLZ_o",
          "mode": "list",
          "cachedResultName": "Lead scoring",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1atURXTNZsoC8rgBylTK5aw5-LK8C14PmddcpemJLZ_o/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Leads",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1atURXTNZsoC8rgBylTK5aw5-LK8C14PmddcpemJLZ_o/edit#gid=0"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Nombre": "={{ $('Datos_Correo_Lead1').item.json.body.name }}",
            "estado": "Contactado",
            "asesor_asignado": "={{ $('Datos_Correo_Lead1').item.json.nombre.asesor }}",
            "notas": "={{ $('Clasificador_Prioridad').first().json.razon }}\n",
            "score_inicial": "={{ $('Clasificador_Prioridad').first().json.razon }}",
            "fecha_actualización": "={{ $now }}",
            "row_number": 0
          },
          "matchingColumns": [
            "Nombre"
          ],
          "schema": [
            {
              "id": "Nombre",
              "displayName": "Nombre",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "empresa",
              "displayName": "empresa",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "cargo",
              "displayName": "cargo",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "email",
              "displayName": "email",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "telefono",
              "displayName": "telefono",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "ciudad",
              "displayName": "ciudad",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "pais",
              "displayName": "pais",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "fuente",
              "displayName": "fuente",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "fecha_creacion",
              "displayName": "fecha_creacion",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "fecha_actualización",
              "displayName": "fecha_actualización",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "estado",
              "displayName": "estado",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "asesor_asignado",
              "displayName": "asesor_asignado",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "score_inicial",
              "displayName": "score_inicial",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "notas",
              "displayName": "notas",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "row_number",
              "displayName": "row_number",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "number",
              "canBeUsedToMatch": true,
              "readOnly": true,
              "removed": false
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        512,
        464
      ],
      "id": "83fbde36-851f-4cf7-84f7-3e6705b63a5c",
      "name": "Actualización_Estado_Sheets1",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "4s639T2GmUGuTGTv",
          "name": "Google Sheets account"
        }
      }
    },
    {
      "parameters": {
        "sendTo": "={{ $('Datos_Correo_Lead2').item.json.body.email }}",
        "subject": "Siigo - 🛡️ Accounting and administrative automation",
        "message": "=<div style=\"font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; line-height: 1.6; color: #333333; max-width: 600px; margin: auto; border: 1px solid #e0e0e0; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 10px rgba(0,0,0,0.05);\">\n  \n  <div style=\"background-color: #0047AB; color: white; padding: 30px; text-align: center;\">\n    <h2 style=\"margin: 0; font-size: 24px; letter-spacing: 0.5px;\">Soluciones Estratégicas B2B</h2>\n    <p style=\"margin: 5px 0 0 0; opacity: 0.9; font-size: 14px;\">Impulsando el crecimiento de tu empresa</p>\n  </div>\n\n  <div style=\"padding: 30px; background-color: #ffffff;\">\n    \n    <div style=\"white-space: pre-wrap; font-size: 15px; color: #444444;\">\n{{ $json.output }}\n    </div>\n\n    <div style=\"margin-top: 30px; text-align: center;\">\n      <a href=\"https://calendly.com/amalia-backup4/demo-siigo\" \n         style=\"background-color: #0047AB; color: white; padding: 12px 25px; text-decoration: none; border-radius: 5px; font-weight: bold; display: inline-block;\">\n         Agendar Demo en Calendly\n      </a>\n    </div>\n  </div>\n\n  <div style=\"background-color: #f4f7fa; color: #777777; padding: 20px; text-align: center; font-size: 12px; border-top: 1px solid #eeeeee;\">\n    <p style=\"margin: 0;\">© 2026 Siigo SAS. Todos los derechos reservados.</p>\n    <p style=\"margin: 5px 0 0 0;\">Este es un mensaje de acercamiento comercial personalizado.</p>\n  </div>\n</div>",
        "options": {}
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.2,
      "position": [
        256,
        816
      ],
      "id": "72949d9c-42af-473f-9cab-0c319f3f2c6b",
      "name": "Gmail_Confirmación_Recibido2",
      "webhookId": "46e9d43f-7fa3-427c-8ed1-5638b2946655",
      "credentials": {
        "gmailOAuth2": {
          "id": "nOuqCnbBSPV0Jeqq",
          "name": "Gmail account"
        }
      }
    },
    {
      "parameters": {
        "operation": "update",
        "documentId": {
          "__rl": true,
          "value": "1atURXTNZsoC8rgBylTK5aw5-LK8C14PmddcpemJLZ_o",
          "mode": "list",
          "cachedResultName": "Lead scoring",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1atURXTNZsoC8rgBylTK5aw5-LK8C14PmddcpemJLZ_o/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Leads",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1atURXTNZsoC8rgBylTK5aw5-LK8C14PmddcpemJLZ_o/edit#gid=0"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Nombre": "={{ $('Datos_Correo_Lead2').item.json.body.name }}",
            "estado": "Contactado",
            "asesor_asignado": "={{ $('Datos_Correo_Lead2').item.json.nombre.asesor }}",
            "notas": "={{ $('Clasificador_Prioridad').first().json.razon }}\n",
            "score_inicial": "={{ $('Clasificador_Prioridad').first().json.razon }}",
            "fecha_actualización": "={{ $now }}",
            "row_number": 0
          },
          "matchingColumns": [
            "Nombre"
          ],
          "schema": [
            {
              "id": "Nombre",
              "displayName": "Nombre",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "empresa",
              "displayName": "empresa",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "cargo",
              "displayName": "cargo",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "email",
              "displayName": "email",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "telefono",
              "displayName": "telefono",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "ciudad",
              "displayName": "ciudad",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "pais",
              "displayName": "pais",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "fuente",
              "displayName": "fuente",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "fecha_creacion",
              "displayName": "fecha_creacion",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "fecha_actualización",
              "displayName": "fecha_actualización",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "estado",
              "displayName": "estado",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "asesor_asignado",
              "displayName": "asesor_asignado",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "score_inicial",
              "displayName": "score_inicial",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "notas",
              "displayName": "notas",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "row_number",
              "displayName": "row_number",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "number",
              "canBeUsedToMatch": true,
              "readOnly": true,
              "removed": false
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        512,
        816
      ],
      "id": "1922379c-3632-4eda-9269-38f3ee292f60",
      "name": "Actualización_Estado_Sheets2",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "4s639T2GmUGuTGTv",
          "name": "Google Sheets account"
        }
      }
    },
    {
      "parameters": {
        "modelId": {
          "__rl": true,
          "value": "models/gemini-2.5-flash",
          "mode": "list",
          "cachedResultName": "models/gemini-2.5-flash"
        },
        "messages": {
          "values": [
            {
              "content": "=Eres un asesor especializado B2B para Siigo, empresa de software contable colombiana que atiende PyMEs, medianas empresas y contadores independientes en Latinoamérica.\n\n\nTu única función traducir a ingles el texto de un correo comercial.\n\n\nCorreo: \n\n\nEstimada {{ $json.body.name }}\n\n\n\nTe escribo porque sé que gestionar una empresa en crecimiento implica retos constantes, especialmente cuando se trata de mantener la contabilidad al día y cumplir con las normativas locales sin perder la agilidad.\n\n\n\nEn Siigo, hemos ayudado a miles de empresarios en la región a centralizar su facturación, inventarios y nómina en la nube, reduciendo hasta en un 40% el tiempo dedicado a tareas administrativas manuales.\n\n\n\nMe gustaría invitarte a una demo personalizada de 15 minutos para mostrarte cómo nuestra plataforma puede adaptarse específicamente a los procesos de {{ $json.body.company }}\n\n\n\nAgenda por favor por medio del siguiente link https://calendly.com/amalia-backup4/demo-siigo\n\n\n\nQuedo atento/a a tu respuesta.\n{{ $json.nombre.asesor }}\n{{ $json.celular.asesor }}\n\n"
            }
          ]
        },
        "builtInTools": {},
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.googleGemini",
      "typeVersion": 1.1,
      "position": [
        -96,
        1136
      ],
      "id": "5c74f39a-11c4-469a-9b80-e65d20723b49",
      "name": "Traductor_Ingles3",
      "credentials": {
        "googlePalmApi": {
          "id": "8jLaEVULqwm4LpAw",
          "name": "Google Gemini(PaLM) Api account"
        }
      }
    },
    {
      "parameters": {
        "modelId": {
          "__rl": true,
          "value": "models/gemini-2.5-flash",
          "mode": "list",
          "cachedResultName": "models/gemini-2.5-flash"
        },
        "messages": {
          "values": [
            {
              "content": "=Eres un asesor especializado B2B para Siigo, empresa de software contable colombiana que atiende PyMEs, medianas empresas y contadores independientes en Latinoamérica.\n\n\nTu única función traducir a ingles el texto de un correo comercial.\n\n\nCorreo: \n\n\nEstimada {{ $json.body.name }}\n\n\n\nTe escribo porque sé que gestionar una empresa en crecimiento implica retos constantes, especialmente cuando se trata de mantener la contabilidad al día y cumplir con las normativas locales sin perder la agilidad.\n\n\n\nEn Siigo, hemos ayudado a miles de empresarios en la región a centralizar su facturación, inventarios y nómina en la nube, reduciendo hasta en un 40% el tiempo dedicado a tareas administrativas manuales.\n\n\n\nMe gustaría invitarte a una demo personalizada de 15 minutos para mostrarte cómo nuestra plataforma puede adaptarse específicamente a los procesos de {{ $json.body.company }}\n\n\n\nAgenda por favor por medio del siguiente link https://calendly.com/amalia-backup4/demo-siigo\n\n\n\nQuedo atento/a a tu respuesta.\n{{ $json.nombre.asesor }}\n{{ $json.celular.asesor }}\n\n"
            }
          ]
        },
        "builtInTools": {},
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.googleGemini",
      "typeVersion": 1.1,
      "position": [
        -96,
        816
      ],
      "id": "786e44be-2639-4cb9-962e-8055aee64f29",
      "name": "Traductor_Ingles2",
      "credentials": {
        "googlePalmApi": {
          "id": "8jLaEVULqwm4LpAw",
          "name": "Google Gemini(PaLM) Api account"
        }
      }
    },
    {
      "parameters": {
        "modelId": {
          "__rl": true,
          "value": "models/gemini-2.5-flash",
          "mode": "list",
          "cachedResultName": "models/gemini-2.5-flash"
        },
        "messages": {
          "values": [
            {
              "content": "=Eres un asesor especializado B2B para Siigo, empresa de software contable colombiana que atiende PyMEs, medianas empresas y contadores independientes en Latinoamérica.\n\n\nTu única función traducir a ingles el texto de un correo comercial.\n\n\nCorreo: \n\n\nEstimada {{ $json.body.name }}\n\n\n\nTe escribo porque sé que gestionar una empresa en crecimiento implica retos constantes, especialmente cuando se trata de mantener la contabilidad al día y cumplir con las normativas locales sin perder la agilidad.\n\n\n\nEn Siigo, hemos ayudado a miles de empresarios en la región a centralizar su facturación, inventarios y nómina en la nube, reduciendo hasta en un 40% el tiempo dedicado a tareas administrativas manuales.\n\n\n\nMe gustaría invitarte a una demo personalizada de 15 minutos para mostrarte cómo nuestra plataforma puede adaptarse específicamente a los procesos de {{ $json.body.company }}\n\n\n\nAgenda por favor por medio del siguiente link https://calendly.com/amalia-backup4/demo-siigo\n\n\n\nQuedo atento/a a tu respuesta.\n{{ $json.nombre.asesor }}\n{{ $json.celular.asesor }}\n\n"
            }
          ]
        },
        "builtInTools": {},
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.googleGemini",
      "typeVersion": 1.1,
      "position": [
        -96,
        464
      ],
      "id": "12c8d701-673a-44ce-96ca-c29cd2b59f46",
      "name": "Traductor_Ingles1",
      "credentials": {
        "googlePalmApi": {
          "id": "8jLaEVULqwm4LpAw",
          "name": "Google Gemini(PaLM) Api account"
        }
      }
    }
  ],
  "pinData": {},
  "connections": {
    "Google Gemini Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "AI Agent": {
      "main": [
        [
          {
            "node": "Formateador_variable_tier",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Recepción_lead": {
      "main": [
        [
          {
            "node": "Base_Datos_Sheets",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Extracción_información_no_sensible": {
      "main": [
        [
          {
            "node": "AI Agent",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Formateador_variable_tier": {
      "main": [
        [
          {
            "node": "Clasificador_Prioridad",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Clasificador_Prioridad": {
      "main": [
        [
          {
            "node": "Consulta_BD_Asesores_Activos",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Consulta_BD_Asesores_Activos1",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Consulta_BD_Asesores_Activos2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Consulta_BD_Asesores_Activos": {
      "main": [
        [
          {
            "node": "¿Hay_Asesores_Activos?",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Consulta_BD_Asesores_Activos1": {
      "main": [
        [
          {
            "node": "¿Hay_Asesores_Activos?1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Consulta_BD_Asesores_Activos2": {
      "main": [
        [
          {
            "node": "¿Hay_Asesores_Activos?2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "¿Hay_Asesores_Activos?": {
      "main": [
        [
          {
            "node": "Selección_Asesor2",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Notificación_Ausencia_Asesor",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "¿Hay_Asesores_Activos?1": {
      "main": [
        [
          {
            "node": "Selección_Asesor",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Notificación_Ausencia_Asesor1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "¿Hay_Asesores_Activos?2": {
      "main": [
        [
          {
            "node": "Selección_Asesor1",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Notificación_Ausencia_Asesor2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Selección_Asesor": {
      "main": [
        [
          {
            "node": "Datos_Correo_Lead2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Selección_Asesor1": {
      "main": [
        [
          {
            "node": "Datos_Correo_Lead3",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Selección_Asesor2": {
      "main": [
        [
          {
            "node": "Datos_Correo_Lead1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Datos_Correo_Lead1": {
      "main": [
        [
          {
            "node": "Traductor_Ingles1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Gmail_Confirmación_Recibido1": {
      "main": [
        [
          {
            "node": "Actualización_Estado_Sheets1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Datos_Correo_Lead3": {
      "main": [
        [
          {
            "node": "Traductor_Ingles3",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Datos_Correo_Lead2": {
      "main": [
        [
          {
            "node": "Traductor_Ingles2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Gmail_Confirmación_Recibido3": {
      "main": [
        [
          {
            "node": "Actualización_Estado_Sheets3",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Gmail_Confirmación_Recibido2": {
      "main": [
        [
          {
            "node": "Actualización_Estado_Sheets2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Base_Datos_Sheets": {
      "main": [
        [
          {
            "node": "Extracción_información_no_sensible",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Traductor_Ingles3": {
      "main": [
        [
          {
            "node": "Gmail_Confirmación_Recibido3",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Traductor_Ingles2": {
      "main": [
        [
          {
            "node": "Gmail_Confirmación_Recibido2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Traductor_Ingles1": {
      "main": [
        [
          {
            "node": "Gmail_Confirmación_Recibido1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1",
    "binaryMode": "separate",
    "availableInMCP": false
  },
  "versionId": "e5be4d3d-1998-4bc1-8573-1baf4a3c73ad",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "f7763aa856622e03143b7ebd9baaf875b6813d90e775fad979b5c5dabb0d5f43"
  },
  "id": "hz8GsKlw8agkB4bP",
  "tags": []
}
