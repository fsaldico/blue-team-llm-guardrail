# Filtro de seguridad para modelos de lenguaje con Python

Este laboratorio práctico fue desarrollado en el marco de la Licenciatura en Ciberdefensa. El objetivo es crear un script inicial de control (guardrail) para evaluar los mensajes de los usuarios antes de que lleguen a una interfaz de IA, mitigando el riesgo de inyección de prompts (vulnerabilidad clasificada como LLM01 por OWASP).

## Lógica del filtro y controles aplicados

Normalización del texto: El script convierte los mensajes entrantes a minúsculas mediante la función lower() para evitar que un atacante intente evadir los controles alternando caracteres en mayúsculas.

Separación de términos peligrosos: Se definieron listas independientes para comandos de ataque explícitos (como "olvida las reglas" o "bypass") y palabras sensibles del negocio (como "contraseña").

Control de falsos positivos: Si el sistema detecta una palabra sensible, analiza el contexto de la oración. Si el usuario incluye términos como "cómo", "ayuda" o "necesito", el script interpreta que es una consulta legítima de soporte técnico y permite el paso. Si la palabra viene aislada o de forma sospechosa, se ejecuta el bloqueo.

Historial de logs: Los mensajes bloqueados se guardan en una lista estructurada llamada registro_de_auditoria que almacena el ID del usuario, el tipo de evento y el texto exacto del ataque para posteriores auditorías de seguridad.

Pruebas unitarias: Se integró la librería estándar unittest de Python para automatizar el testeo del filtro. Esto permite verificar de forma constante que la lógica responda correctamente ante intentos de ataque y consultas legítimas.

## Archivos del proyecto

El código fuente, los comentarios didácticos y el banco de pruebas automatizadas están unificados en el siguiente cuaderno interactivo:

* blue_team_guardrail_tests.ipynb
