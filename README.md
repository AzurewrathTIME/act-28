# 🏫 Sistema Escolar - Procesando Formularios en C++

Implementación de la lectura, parseo y validación de peticiones HTTP POST con formato JSON directamente desde el servidor programado en C++.

![C++](https://img.shields.io/badge/C++-00599C?style=flat&logo=c%2B%2B&logoColor=white)
![API](https://img.shields.io/badge/API-REST-blue)
![JSON](https://img.shields.io/badge/Format-JSON-orange)
![Status](https://img.shields.io/badge/status-completado-success)

---

## 📌 Descripción

En esta actividad, el servidor en C++ dio un paso gigante: ahora es capaz de **leer el cuerpo (Body)** de una petición HTTP POST, extraer los datos en formato JSON que envía el frontend (`fetch()`), procesarlos, guardarlos temporalmente en memoria y responder con un mensaje personalizado.

---

## ✨ Características

- 📥 **Lectura completa del socket:** El servidor lee en bucle hasta asegurar que ha recibido todos los bytes indicados por `Content-Length`.
- 🧩 **Parseo de JSON manual:** Extracción de claves y valores sin depender de librerías externas.
- 🛡️ **Validación de datos:** Verificación de campos vacíos o formatos inválidos antes de procesar.
- 🚫 **Manejo de conflictos:** Validación para evitar registrar dos alumnos con la misma matrícula (Error `409 Conflict`).
- 💬 **Respuesta personalizada:** El servidor construye dinámicamente un mensaje usando los datos recibidos (ej. *"Bienvenido Ana, matrícula A001"*).
- 💾 **Memoria temporal:** Uso de un `std::vector` para mantener una lista de los alumnos registrados mientras el servidor esté encendido.

---

## 🛠️ Tecnologías

| Tecnología | Uso |
|------------|-----|
| C++17 | Lógica de red, lectura de sockets y parseo de strings |
| Sockets TCP | Recepción de peticiones HTTP |
| JSON | Formato de intercambio de datos entre frontend y backend |

---

## 🧠 Conceptos aplicados

### Anatomía de una petición HTTP POST
A diferencia de un GET, el POST envía datos en el cuerpo:
1. **Cabeceras:** Terminan con una línea vacía (`\r\n\r\n`).
2. **Content-Length:** Indica cuántos bytes mide el cuerpo.
3. **Cuerpo (Body):** Aquí viaja el JSON con los datos (`{"nombre":"Ana", ...}`).

### Funciones clave en C++
- `leerPeticionCompleta()`: Se asegura de recibir los datos hasta completar el `Content-Length`.
- `extraerCuerpo()`: Corta el string justo después de `\r\n\r\n` para obtener el JSON.
- `extraerValorJSON()`: Función artesanal que busca la clave (ej. `"nombre"`) y extrae el valor usando índices de string.
- `parsearAlumno()`: Agrupa los datos extraídos en un `struct` (estructura) manejable en C++.

---

## 🚀 Cómo probarlo

### 1. Compilar y ejecutar
Recuerda recompilar el servidor para aplicar los cambios:
```bash
g++ servidor.cpp -o servidor.exe -std=c++17 -lws2_32
.\servidor.exe
```

### 2. Prueba visual (Navegador)
1. Abre `http://localhost:8080`.
2. Rellena el formulario y presiona **Registrar**.
3. En el navegador aparecerá un mensaje del servidor confirmando el registro.

### 3. Prueba de procesamiento (Consola)
Mira la ventana de la terminal donde corre C++. Al enviar el formulario, deberías ver:
```text
[API] POST /api/alumnos

--- POST recibido ---
Nombre:    Ana
Edad:      20
Matricula: A001
Correo:    ana@escuela.com
---------------------
```

### 4. Prueba del Mini-Reto (Matrícula duplicada)
1. Intenta registrar un alumno usando la **misma matrícula** que ya registraste.
2. El servidor rechazará la petición y en el navegador verás un mensaje de error indicando que la matrícula ya existe (`409 Conflict`).

---

## 📁 Estructura del proyecto

```text
Sistema-Escolar/
├── servidor.cpp       <-- Servidor web en C++ (procesa el JSON)
├── README.md
└── Public/
    ├── index.html
    ├── styless.css
    ├── app.js         <-- Frontend que envía el JSON
    └── img/
```

---

## 📄 Licencia

MIT License
