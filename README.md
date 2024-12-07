# Facultad-Carrera CRUD Project

## Descripción del Proyecto

Este proyecto implementa una aplicación de consola en Kotlin para gestionar una relación de **UNO a MUCHOS** entre entidades de tipo `Facultad` y `Carrera`. Las operaciones CRUD (**Crear, Leer, Actualizar, Eliminar**) pueden realizarse tanto sobre las facultades como sobre sus respectivas carreras. 

El proyecto está diseñado siguiendo la **Clean Architecture** y aplica principios **SOLID**, garantizando un código limpio, escalable y mantenible. Los datos se almacenan y recuperan desde un archivo JSON (`facultades.json`), en lugar de utilizar una base de datos.

## Tabla de Contenidos

1. [Arquitectura del Proyecto](#arquitectura-del-proyecto)
2. [Requisitos](#requisitos)
3. [Instalación](#instalación)
4. [Uso](#uso)
5. [Estructura del Código](#estructura-del-código)
6. [Funcionamiento de la Aplicación](#funcionamiento-de-la-aplicación)
7. [Ejemplo de Archivo JSON](#ejemplo-de-archivo-json)
8. [Contribuciones](#contribuciones)
9. [Licencia](#licencia)

---

## Arquitectura del Proyecto

El proyecto se basa en la **Clean Architecture**, donde cada capa tiene una responsabilidad específica:

### Capas Principales
1. **Domain (Dominio):**
   - Define las entidades principales (`Facultad` y `Carrera`) y las interfaces para los repositorios.
   - No depende de ninguna otra capa.
   
2. **Use Case (Casos de Uso):**
   - Contiene la lógica de negocio en forma de casos de uso.
   - Depende únicamente de la capa de dominio.

3. **Data (Datos):**
   - Implementa los repositorios definidos en la capa de dominio.
   - Incluye el almacenamiento en JSON utilizando `kotlinx.serialization`.

4. **Presentation (Presentación):**
   - Proporciona una interfaz de usuario en consola para interactuar con el sistema.
   - Es la capa más externa del sistema.

---

## Requisitos

Para ejecutar este proyecto, necesitas:

- **Kotlin 1.9+**
- **Gradle 8.0+**
- **IntelliJ IDEA** (recomendado)
- JDK 11 o superior

---

## Instalación

1. **Clona el repositorio:**

   ```bash
   git clone https://github.com/tuusuario/facultad-carrera-crud.git
   cd facultad-carrera-crud
   ```

2. **Configura el entorno:**
   Asegúrate de tener Kotlin y Gradle configurados en tu entorno.

3. **Instala las dependencias:**
   En el archivo `build.gradle.kts`, las dependencias necesarias ya están configuradas. Puedes instalarlas ejecutando:

   ```bash
   ./gradlew build
   ```

4. **Prepara el archivo JSON:**
   Asegúrate de que el archivo `facultades.json` existe en `src/main/resources` con el contenido inicial `[]`.

---

## Uso

1. **Ejecuta la aplicación:**

   Desde la línea de comandos o IntelliJ IDEA, ejecuta el archivo `Main.kt` en el paquete `presentation`.

2. **Explora las opciones del menú:**

   El programa presenta un menú con opciones para CRUD de **Facultades** y **Carreras**. Sigue las instrucciones en pantalla.

---

## Estructura del Código

```plaintext
src
└── main
    ├── kotlin
    │   ├── domain
    │   │   ├── model
    │   │   │   ├── Carrera.kt
    │   │   │   └── Facultad.kt
    │   │   └── repository
    │   │       ├── CarreraRepository.kt
    │   │       └── FacultadRepository.kt
    │   ├── usecase
    │   │   ├── carrera
    │   │   │   ├── CreateCarreraUseCase.kt
    │   │   │   ├── DeleteCarreraUseCase.kt
    │   │   │   ├── GetCarrerasByFacultadUseCase.kt
    │   │   │   └── UpdateCarreraUseCase.kt
    │   │   ├── facultad
    │   │   │   ├── CreateFacultadUseCase.kt
    │   │   │   ├── DeleteFacultadUseCase.kt
    │   │   │   ├── GetAllFacultadesUseCase.kt
    │   │   │   └── UpdateFacultadUseCase.kt
    │   ├── data
    │   │   ├── repository
    │   │   │   ├── JsonFacultadRepository.kt
    │   │   │   └── JsonCarreraRepository.kt
    │   │   └── storage
    │   │       └── JsonStorage.kt
    │   └── presentation
    │       └── Main.kt
    └── resources
        └── facultades.json
```

### Detalle de cada sección

1. **domain:** Define el modelo de datos (`Facultad` y `Carrera`) y las interfaces (`FacultadRepository` y `CarreraRepository`).
2. **usecase:** Implementa los casos de uso, que son acciones específicas como crear, leer, actualizar y eliminar.
3. **data:** Implementa los repositorios utilizando un archivo JSON como medio de almacenamiento persistente.
4. **presentation:** Contiene el menú de consola para interactuar con el usuario.
5. **resources:** Almacena el archivo `facultades.json`, que contiene los datos del sistema.

---

## Funcionamiento de la Aplicación

### Menú Principal
El programa comienza mostrando un menú principal con las siguientes opciones:

1. **CRUD Facultad**
   - Crear, listar, actualizar y eliminar facultades.
   
2. **CRUD Carrera**
   - Agregar carreras a una facultad, listar carreras por facultad, actualizar y eliminar carreras.

3. **Salir**
   - Finaliza la ejecución del programa.

### Operaciones CRUD
Las entidades tienen los siguientes atributos:

- **Facultad:**
  - `id`: Identificador único.
  - `nombre`: Nombre de la facultad.
  - `fechaCreacion`: Fecha en formato `yyyy-MM-dd`.
  - `activa`: Si la facultad está activa o no (booleano).
  - `numeroDepartamentos`: Número de departamentos en la facultad.
  - `presupuestoAnual`: Presupuesto anual de la facultad.

- **Carrera:**
  - `id`: Identificador único.
  - `nombre`: Nombre de la carrera.
  - `anioInicio`: Año en que comenzó la carrera.
  - `acreditada`: Si la carrera está acreditada (booleano).
  - `creditosTotales`: Créditos necesarios para completar la carrera.
  - `mensualidad`: Mensualidad promedio de la carrera.

---

## Ejemplo de Archivo JSON

Contenido inicial del archivo `facultades.json`:

```json
[]
```

Después de agregar una facultad y una carrera, el archivo podría verse así:

```json
[
  {
    "id": 1,
    "nombre": "Facultad de Ingeniería",
    "fechaCreacion": "2000-05-15",
    "activa": true,
    "numeroDepartamentos": 5,
    "presupuestoAnual": 1500000.0,
    "carreras": [
      {
        "id": 1,
        "nombre": "Ingeniería en Software",
        "anioInicio": 2010,
        "acreditada": true,
        "creditosTotales": 240,
        "mensualidad": 300.0
      }
    ]
  }
]
```

---

## Contribuciones

Las contribuciones son bienvenidas. Para contribuir:

1. Haz un fork del repositorio.
2. Crea una rama (`git checkout -b feature/tu-feature`).
3. Realiza tus cambios y haz commit (`git commit -m 'Añadida nueva funcionalidad'`).
4. Haz push a la rama (`git push origin feature/tu-feature`).
5. Abre un Pull Request.

---

## Licencia

Este proyecto está licenciado bajo la **MIT License**. Puedes consultar los detalles en el archivo `LICENSE`.
