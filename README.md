*Blog Mentalidad de Crecimiento y Comunicación en Entornos Digitales*
# Entrada de Blog: Post-Mortem Constructivo

## 1. Contexto
El proyecto consiste en una aplicación web de comercio electrónico que maneja usuarios simultáneos durante eventos de alto tráfico.

## 2. Problema
Durante un evento de ventas, el sistema presentó latencias superiores a 8 segundos. En términos sencillos: la base de datos se saturó porque recibía demasiadas consultas repetidas a la vez.

## 3. Acciones (Post-Mortem)
* **Análisis:** Identificamos una consulta sin índice optimizado.
* **Solución:** Agregamos un índice en la base de datos e implementamos almacenamiento en caché (Redis).

## 4. Aprendizajes
* Implementar monitoreo proactivo antes de eventos masivos.
* Ver los errores como fallos del sistema y no de las personas.

## 5. Reflexión sobre Feedback Radicalmente Sincero
Al recibir comentarios sobre el uso excesivo de jerga técnica, simplifiqué las explicaciones usando analogías claras para que cualquier miembro del equipo entienda el impacto.
