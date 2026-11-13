# Up Up Progress!

**Aplicación móvil para el seguimiento de entrenamientos, alimentación y progreso físico**  
**Proyecto de título — Ingeniería en Informática**  
**Integrantes:** Franco Manríquez y Javier Loaiza

## 1. Descripción del proyecto

**Up Up Progress!** es una aplicación móvil nativa para Android dirigida a personas que desean organizar sus entrenamientos y alimentación, consultar su evolución física y tomar decisiones informadas sobre sus hábitos.

El proyecto busca resolver la **dispersión de registros** entre notas, planillas y aplicaciones independientes. Centraliza información relacionada con tres objetivos personales: **aumentar masa muscular, reducir peso o mantenerlo**.

El alcance del sistema contempla:

- **Entrenamiento:** crear rutinas propias y registrar ejercicios, series, repeticiones y cargas, con acceso al historial.
- **Progreso corporal:** registrar el peso y consultar su evolución a través del tiempo.
- **Alimentación:** registrar cantidades consumidas y consultar calorías y macronutrientes, con apoyo del catálogo de **Open Food Facts**.
- **Configuración nutricional:** establecer metas de calorías y macronutrientes de manera manual o mediante cálculos orientativos.
- **Inteligencia artificial:** analizar información registrada y presentar sugerencias que el usuario puede aceptar o descartar. **La aplicación no modifica automáticamente las rutinas ni los objetivos.**

> **Nota de alcance:** las funcionalidades descritas corresponden al diseño del producto. Su disponibilidad efectiva depende de la versión de la aplicación y de los servicios desplegados. El repositorio contiene documentación de requisitos, arquitectura y pruebas para contrastar el alcance con las evidencias.

## 2. Tecnologías utilizadas

| Área | Tecnología | Uso en el proyecto |
| --- | --- | --- |
| Desarrollo móvil | **Kotlin** | Lenguaje de la aplicación Android. |
| Interfaz | **Jetpack Compose y Material Design 3** | Construcción de las pantallas y componentes visuales. |
| Entorno y compilación | **Android Studio, Gradle y Android Gradle Plugin** | Desarrollo, construcción y ejecución. |
| Backend y nube | **Supabase Cloud** | Servicios de autenticación, acceso a datos y lógica del backend. |
| Base de datos | **PostgreSQL** | Persistencia de perfiles, objetivos, entrenamientos y alimentos. |
| Autenticación y seguridad | **Supabase Auth, JWT y Row Level Security (RLS)** | Identidad y control de acceso a los datos personales. |
| Servicios de backend | **Supabase Data API, funciones PostgreSQL (RPC) y Edge Functions** | Consultas, validaciones e integraciones según el módulo. |
| Comunicación de red | **supabase-kt y Ktor** | Comunicación entre la aplicación Android y Supabase. |
| Información alimentaria | **Open Food Facts API** | Consulta de productos y datos nutricionales. |
| Inteligencia artificial | **Groq API** | Servicio de IA representado en la arquitectura de integración. |
| Diseño y prototipado | **Figma** | Diseño de interfaces y mockups. |
| Control de versiones | **Git y GitHub** | Historial de cambios y colaboración del equipo. |

**Configuración de desarrollo Android utilizada:** Kotlin 2.4.21, Android Gradle Plugin 9.4.1, Gradle 9.6.0, Supabase Kotlin SDK 3.8.0, Ktor 3.5.1, `minSdk` 26 y `targetSdk` 36. Las versiones deben contrastarse con los archivos Gradle de la entrega final.

## 3. Arquitectura de la solución

La solución sigue una arquitectura **cliente-servidor**, con una aplicación Android como cliente y **Supabase Cloud** como plataforma de backend.

La aplicación, desarrollada en Kotlin y Jetpack Compose, se comunica por HTTPS con los servicios de autenticación y datos de Supabase. La información persistente se almacena en **PostgreSQL**, donde las políticas **RLS** controlan el acceso a los registros personales. Para las operaciones que lo requieren, el backend utiliza funciones PostgreSQL y **Edge Functions**. Las integraciones externas del diseño contemplan **Open Food Facts** para productos alimentarios y **Groq API** para análisis apoyados por IA.



Entre las entidades principales del modelo de datos se encuentran `profiles`, `user_goals`, `routines`, `exercises`, `workout_sessions`, `performed_sets`, `body_weight_logs`, `food_products` y `food_entries`.

## 4. Instrucciones para ejecutar el proyecto localmente

### 4.1. Obtener el repositorio de evidencias

```bash
git clone https://github.com/JavierPelao/Loaiza_Manriquez_Capstone.git
cd Loaiza_Manriquez_Capstone
```

**Importante:** este repositorio contiene principalmente los documentos y evidencias del proyecto, organizados en `Fase 1` y `Fase 2`. **El código fuente Android compilable no se encuentra actualmente en la rama `main` de este repositorio.** Por lo tanto, el comando anterior permite revisar la documentación, pero no ejecutar por sí solo la aplicación.

### 4.2. Preparar el entorno Android

Una vez obtenida la **carpeta del proyecto Android** (que incluye `settings.gradle.kts`, el módulo `app` y el *Gradle Wrapper*):

1. Instalar **Android Studio** y los componentes de Android SDK correspondientes al proyecto (SDK 36 para compilación).
2. Abrir en Android Studio **la carpeta raíz del proyecto Android**, no la carpeta de evidencias.
3. Configurar un dispositivo físico Android compatible o un emulador; durante el desarrollo se ha utilizado un **Pixel 7**.
4. Crear un archivo local `supabase.properties` junto a `settings.gradle.kts`, con las credenciales públicas del proyecto Supabase al que se tenga acceso:

   ```properties
   SUPABASE_URL=https://TU_PROYECTO.supabase.co
   SUPABASE_PUBLIC_KEY=TU_CLAVE_PUBLICABLE
   ```

5. Mantener `supabase.properties` fuera del control de versiones mediante `.gitignore`. **Nunca incluir `service_role`, claves `sb_secret_`, contraseñas ni tokens privados** en el proyecto Android o en GitHub.
6. Ejecutar **Sync Project with Gradle Files** y, posteriormente, la configuración de ejecución `app` desde Android Studio.
7. Utilizar una cuenta de pruebas autorizada para comprobar el registro, el inicio de sesión y los módulos conectados a Supabase.

Para reproducir las operaciones de backend también debe existir un entorno Supabase con el esquema, las políticas RLS y las funciones correspondientes desplegadas. La aplicación no ejecuta las migraciones de base de datos al iniciarse.

**Pendiente de publicación:** incorporar el proyecto Android a este repositorio o enlazar aquí el repositorio que contiene el código fuente, junto con cualquier instrucción adicional necesaria para la versión final.

## 5. Integrantes y roles

| Integrante | Rol y responsabilidades principales |
| --- | --- |
| **Franco Manríquez** | Desarrollo de la aplicación Android; diseño e implementación de interfaces con Jetpack Compose, navegación, formularios e integración del cliente con Supabase. |
| **Javier Loaiza** | Desarrollo y administración del backend en Supabase; modelo de datos PostgreSQL, funciones y servicios, autenticación, políticas RLS e integraciones de backend. |

Ambos integrantes participan en la definición de requisitos, planificación, documentación, integración y validación de la solución.

## 6. Metodología de trabajo

El proyecto se organiza de manera **incremental**, dividiendo el desarrollo en tareas funcionales pequeñas que pueden implementarse, integrarse y verificarse por separado.

El equipo utiliza un seguimiento visual de actividades **tipo Kanban**, apoyado en **Trello**, y una **Carta Gantt** para planificar las etapas, entregables y fechas del proyecto. **Git y GitHub** permiten controlar las versiones del código y los documentos, mientras que las pruebas y evidencias registran los resultados de cada etapa.

Este enfoque describe la organización aplicada por el equipo y no implica la adopción formal de todas las ceremonias de Scrum.

## 7. Documentación del proyecto

El repositorio reúne los entregables académicos y las evidencias de desarrollo:

- [Fase 1 — Evidencias y planificación](Fase%201/)
- [Fase 2 — Evidencias y documentación](Fase%202/)
- [Especificación de Requisitos de Software (ERS)](Fase%202/Evidencias%20de%20Proyecto/1.Especificaci%C3%B3n%20de%20Requisitos%20de%20Software%20%28ERS%29.pdf)
- [Diseño y arquitectura](Fase%202/Evidencias%20de%20Proyecto/2.Dise%C3%B1o%20y%20Arquitectura.docx.pdf)
- [Plan de pruebas y evidencias](Fase%202/Evidencias%20de%20Proyecto/3.Plan%20de%20Pruebas%20y%20Evidencias.docx.pdf)
- [Manual técnico](Fase%202/Evidencias%20de%20Proyecto/4.Manual%20Tecnico.docx.pdf)
- [Mockups en Figma](https://www.figma.com/design/k4bgudz3apnP9CwsDBgqMs/Capstone-Fitness-App-%E2%80%94-Mockup?node-id=0-1)

---

**Up Up Progress!** · Proyecto de título de Ingeniería en Informática · Franco Manríquez y Javier Loaiza.
