# Entrega: Rol Personalizado "Revisor de Calidad"

## 1. Definición del Rol
- **Nombre corto:** `revisordecalidad`
- **Nombre completo:** quality_reviewer
- **Propósito:** Permitir a auditores visualizar contenidos, participantes, calificaciones e informes dentro de una categoría de cursos sin capacidad de edición, calificación ni interacción en foros.
<img width="1844" height="647" alt="image" src="https://github.com/user-attachments/assets/97f6b8c7-f6ca-4d25-bfd1-44f2b2b8b385" />


## 2. Contextos Permitidos
- Categoría (`CONTEXT_COURSECAT`)
- Curso (`CONTEXT_COURSE`)
<img width="1314" height="792" alt="image" src="https://github.com/user-attachments/assets/cc3cee48-74e1-4f4d-8aab-b6f27019ca3c" />


## 3. Ajuste de Capacidades (8 Cambios Clave respecto al Arquetipo)
1. `moodle/category:viewcourselist`: **PERMITIR** (Ver cursos de la categoría).
2. `moodle/course:view`: **PERMITIR** (Acceder a los cursos sin matriculación directa).
3. `moodle/gradereport/user:view`: **PERMITIR** (Consultar informes de calificaciones).
4. `moodle/site:viewreports`: **PERMITIR** (Ver informes de logs y actividad).
5. `moodle/course:manageactivities`: **PROHIBIR** (Impide crear o editar actividades).
6. `mod/quiz:grade`: **PROHIBIR** (Impide calificar intentos de cuestionarios).
7. `mod/forum:startdiscussion`: **PROHIBIR** (Impide publicar hilos en foros).
8. `moodle/user:viewhiddendetails`: **PROHIBIR** (Impide ver datos personales ocultos).

## 4. Asignación y Prueba
- **Asignación en Categoría:** Se asignó al usuario de prueba en el contexto de **Categoría**, heredando acceso a todos los cursos contenidos en ella sin necesidad de matriculación explícita.
- **Efecto de Sobrescritura Local:** Se aplicó un bloqueo local (`PREVENIR`) en la capacidad `moodle/gradereport/user:view` dentro de un curso específico para verificar cómo la regla local anula la regla heredada de la categoría.

<img width="1430" height="632" alt="image" src="https://github.com/user-attachments/assets/1b46d755-0932-4bdb-815d-437afdb6d0d5" />


## 5. Instalación del Preset XML
Para importar este rol en otro Moodle:
1. Ir a `Administración del sitio > Usuarios > Permisos > Definir roles`.
2. Pulsar en `Añadir un nuevo rol`.
3. Subir el archivo `role_qualityreviewer.xml` adjunto en este repositorio.

## Consulta de PostgreSQL donde se muestran los usuarios en moodle Stable_503 con rol de Revisor de Calidad y su contexto:
SELECT 
ID AS ID_USUARIO,
USERNAME AS USUARIO,
FIRSTNAME, 
LASTNAME, 
EMAIL, 
CONTEXTID AS ID_CONTEXTO
