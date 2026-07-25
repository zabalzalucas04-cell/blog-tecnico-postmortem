# 🛠️ Post-Mortem de Operaciones: Rediseño del Sistema de Trazabilidad y Marcado de Números de Serie para Escalabilidad Industrial

**Autor:** Lucas Zabalza
**Rol:** Responsable de Ingeniería de Procesos / Calidad  
**Área:** Planta de Producción  
**Fecha:** 25 de Julio de 2026  
**Repositorio de Documentación:** https://github.com/zabalzalucas04-cell/blog-tecnico-postmortem

---

## 1. Contexto

Nuestra empresa (PyME dedicada a la fabricación de componentes electromecánicos) se encuentra en la etapa final de lanzamiento de una nueva línea de productos: la serie **"Alpha-Control"**. Hasta el momento, la planta operaba con volúmenes reducidos y utilizaba esquemas de identificación tradicionales basados en registros manuales y etiquetas adhesivas con correlativos simples (ej. `0001`, `0002`).

Con la llegada de esta nueva línea, la capacidad proyectada de producción aumentó un **300%**, diversificando el catálogo en 5 variantes de productos con distintas especificaciones técnicas y mercados de destino. 

Para sostener este crecimiento, se volvió prioritario diseñar un **sistema de marcado físico y un esquema de numeración de serie** que garantizara trazabilidad punta a punta (desde ensamblaje hasta garantías), evitando el colapso del sistema por duplicación o falta de información clave.

---

## 2. Problema

Durante las pruebas piloto de la línea "Alpha-Control", el equipo de calidad y producción identificó que el sistema de identificación actual presentaba graves limitaciones operativas y riesgos de obsolescencia:

### 2.1 Limitaciones del Sistema Heredado (*Legacy*)
* **Obsolescencia de Numeración:** El esquema correlativo simple no permitía diferenciar modelo, año de fabricación, lote de componentes ni país de destino.
* **Degradación del Marcado:** Las etiquetas impresas por transferencia térmica en el área de acabado se deterioraban con los solventes de limpieza y el roce durante el embalaje, borrando la información antes del despacho.
* **Falta de Integración con el ERP:** El registro manual de series en planillas de Excel generaba un **12% de errores por digitación humana**, afectando la trazabilidad de inventarios y la atención de garantías.

### 2.2 Requisitos del Nuevo Sistema
El nuevo método debía cumplir simultáneamente con tres criterios críticos:
1. **Inalterabilidad física:** Resisitir condiciones ambientales y operativas extremas.
2. **Escalabilidad de datos:** Permitir la incorporación de nuevas familias de productos durante los próximos 10 años sin saturar el formato.
3. **Lectura automatizada:** Reducir a cero el registro manual en línea de producción.

---

## 3. Acciones Tomadas: Análisis de Propuestas y Toma de Decisión

Para resolver el desafío, organizamos mesas de trabajo interdepartamentales (Producción, Calidad, Sistemas y Mantenimiento) para diseñar, evaluar y presentar tres alternativas a la Dirección general.

### 3.1 Cuadro Comparativo de Propuestas

| Propuesta | Descripción Técnica | Pros | Contras | Dictamen |
| :--- | :--- | :--- | :--- | :--- |
| **A: Etiquetado de Poliéster + Correlativo Ampliado** | Impresión de etiquetas de alta resistencia con código de barras 1D básico. | • Bajo costo inicial.<br>• Cero tiempo de capacitación. | • No resuelve el riesgo de desprendimiento.<br>• Capacidad de datos muy limitada en espacios reducidos. | ❌ Descartado |
| **B: Grabado Laser Fiber + Código DataMatrix 2D + Estructura Alfa-Numérica Inteligente** | Micrograbado directo en chasis (`Direct Part Marking`) con formato `[Línea]-[Modelo]-[Año][Semana]-[Secuencia]`. | • Marcado indeleble para siempre.<br>• Alta densidad de datos en áreas pequeñas.<br>• Lectura automatizada rápida.<br>• Sistema de numeración escalable. | • Requiere inversión moderada en equipo láser.<br>• Ajuste técnico inicial en línea. | **✅ SELECCIONADO** |
| **C: Identificación por Radiofrecuencia (RFID Tags)** | Inserción de un chip RFID en la estructura interna del producto. | • Lectura masiva a distancia sin línea de visión directa.<br>• Almacenamiento dinámico de datos. | • Costo unitario elevado por producto.<br>• Interferencias electromagnéticas por las estructuras metálicas del chasis. | ❌ Descartado |

### 3.2 Estructura del Nuevo Esquema de Numeración Seleccionado
Se diseñó un formato estándar de 12 caracteres alfanuméricos:

$$\text{Formato: } \underbrace{\text{AC}}_{\text{Línea}} - \underbrace{\text{01}}_{\text{Modelo}} - \underbrace{\text{2630}}_{\text{Año / Semana}} - \underbrace{\text{0001}}_{\text{Secuencia}}$$

> **Ejemplo:** `AC-01-2630-0145`  
> *Identifica un producto de la Línea **Alpha-Control**, Modelo **01**, fabricado en el **año 2026, semana 30**, unidad **145**.*

### 3.3 Presentación a Directivos y Aprobación
Presentamos la **Propuesta B** ante la Dirección General sustentando el Retorno de Inversión (ROI):
* **Ahorro de costos por garantías no válidas:** El grabado indeleble elimina la clonación de etiquetas o el reclamo de productos fuera de cobertura.
* **Eficiencia operativa:** Reducción del tiempo de registro en la estación final de **45 segundos a solo 2 segundos** por unidad mediante lector de código 2D.

**Resultado:** La junta directiva aprobó el presupuesto para la adquisición del marcador láser y la actualización del sistema.

---

## 4. Evidencia en Control de Versiones (Git Workflow)

Para mantener la estandarización y evitar que la documentación del proceso quede desactualizada en carpetas locales, implementamos **Git** como repositorio de los Procedimientos Operativos Estándar (SOP) y arquitecturas de numeración:

* 🔀 **Pull Request de Propuestas:** [PR #12: Propuestas de marcado y estructura de numeración de serie v2.0](https://github.com/tu-usuario/blog-tecnico/pull/1) *(Reemplazar con tu enlace)*
* 📌 **Commit de Estándar Aprobado:** `git commit -m "docs(sop): agrega manual de marcado laser y estructura alfanumerica aprobada"`
* 📌 **Commit de Script de Integración:** `git commit -m "feat(erp): agrega script de validacion de estructura de serie para lector 2D"`

---

## 5. Aprendizajes y Mejores Prácticas

1. **El valor de la diversidad de perspectivas:** Escuchar activamente a los operarios de la línea reveló datos cruciales que la gerencia no tenía en el radar, como el impacto de los líquidos de limpieza en las etiquetas anteriores.
2. **Optimización de recursos y costos:** La solución elegida no fue ni la más barata (etiquetas) ni la más costosa/compleja (RFID), sino la que ofreció el mejor balance de costo-beneficio y durabilidad en el tiempo.
3. **Cultura de documentación viva:** La adopción de Markdown y repositorios para documentar procesos industriales asegura que cualquier cambio futuro en el esquema de series sea revisado, aprobado y registrado de manera transparente.

---

## 6. Reflexión: Aplicación de Feedback Radicalmente Sincero (*Radical Candor*)

Durante la elaboración de las propuestas, el equipo de producción expresó directamente que la **Propuesta C (RFID)** impulsada inicialmente por el área de Innovación no era viable operacionalmente por costos y problemas de interferencia.

Aplicando **Feedback Radicalmente Sincero**:
* **Desafiar directamente con empatía:** El equipo técnico no dudó en señalar los puntos débiles de la propuesta RFID con datos empíricos de planta, evitando que la empresa realizara un gasto ineficiente.
* **Aceptación y Redirección:** El área de diseño aceptó las observaciones sin tomarlo como una descalificación personal y canalizó los esfuerzos en perfeccionar la **Propuesta B (Láser + DataMatrix)**.
* **Resultado:** Esta comunicación franca y sin rodeos permitió tomar la decisión más efectiva en tiempo récord, logrando que la línea de productos arrancara a término.
