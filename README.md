# Laboratorio práctico: Trabajando con APIs en JavaScript

En este laboratorio, trabajaremos con la API de Open Brewery DB para practicar los conceptos de APIs, Fetch, Promesas y Async/Await en JavaScript.

## Objetivo

Crear una pequeña aplicación que permita buscar y mostrar información sobre cervecerías utilizando la API de Open Brewery DB.

## Retos

### Reto 1: Obtener una lista de cervecerías

Utiliza la API para obtener una lista de las primeras 5 cervecerías y muestra sus nombres en la consola.

### Reto 2: Buscar cervecerías por ciudad

Crea una función que permita buscar cervecerías por ciudad y muestre los resultados en la consola.

### Reto 3: Obtener detalles de una cervecería

Implementa una función que obtenga los detalles de una cervecería específica por su ID y muestre la información en la consola.

### Reto 4: Manejo de errores

Modifica tus funciones para manejar posibles errores en las peticiones a la API.

### Reto 5: Implementación con Async/Await

Reescribe una de las funciones anteriores utilizando la sintaxis Async/Await.

## Instrucciones

1. Utiliza la documentación de la API: https://www.openbrewerydb.org/documentation
2. Implementa cada reto en orden.
3. Prueba tus funciones en la consola del navegador o en un entorno Node.js.

## Código base

Puedes comenzar con el siguiente código base:

```javascript
const BASE_URL = "https://api.openbrewerydb.org/v1/breweries";

// Implementa tus funciones aquí

// Ejemplo de uso:
// obtenerCervecerias();
// buscarCerveceriasPorCiudad('san diego');
// obtenerDetallesCerveceria('madtree-brewing-cincinnati');
```

¡Buena suerte!

---

## Respuestas

A continuación, se presentan las soluciones para cada reto. Intenta resolver los retos por tu cuenta antes de mirar las respuestas.

### Reto 1: Obtener una lista de cervecerías

```javascript
function obtenerCervecerias() {
  fetch(`${BASE_URL}?per_page=5`)
    .then((response) => response.json())
    .then((data) => {
      console.log("Primeras 5 cervecerías:");
      data.forEach((brewery) => console.log(brewery.name));
    })
    .catch((error) => console.error("Error:", error));
}
```

### Reto 2: Buscar cervecerías por ciudad

```javascript
function buscarCerveceriasPorCiudad(ciudad) {
  fetch(`${BASE_URL}?by_city=${encodeURIComponent(ciudad)}`)
    .then((response) => response.json())
    .then((data) => {
      console.log(`Cervecerías en ${ciudad}:`);
      data.forEach((brewery) => console.log(brewery.name));
    })
    .catch((error) => console.error("Error:", error));
}
```

### Reto 3: Obtener detalles de una cervecería

```javascript
function obtenerDetallesCerveceria(id) {
  fetch(`${BASE_URL}/${id}`)
    .then((response) => response.json())
    .then((data) => {
      console.log("Detalles de la cervecería:");
      console.log(`Nombre: ${data.name}`);
      console.log(`Tipo: ${data.brewery_type}`);
      console.log(`Dirección: ${data.street}, ${data.city}, ${data.state}`);
      console.log(`Sitio web: ${data.website_url}`);
    })
    .catch((error) => console.error("Error:", error));
}
```

### Reto 4: Manejo de errores

```javascript
function buscarCerveceriasPorCiudadConErrores(ciudad) {
  fetch(`${BASE_URL}?by_city=${encodeURIComponent(ciudad)}`)
    .then((response) => {
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      return response.json();
    })
    .then((data) => {
      if (data.length === 0) {
        console.log(`No se encontraron cervecerías en ${ciudad}`);
      } else {
        console.log(`Cervecerías en ${ciudad}:`);
        data.forEach((brewery) => console.log(brewery.name));
      }
    })
    .catch((error) => console.error("Error:", error.message));
}
```

### Reto 5: Implementación con Async/Await

```javascript
async function obtenerCerveceriasAsync() {
  try {
    const response = await fetch(`${BASE_URL}?per_page=5`);
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    const data = await response.json();
    console.log("Primeras 5 cervecerías:");
    data.forEach((brewery) => console.log(brewery.name));
  } catch (error) {
    console.error("Error:", error.message);
  }
}
```

Recuerda que estas son solo soluciones de ejemplo. Puede haber múltiples formas válidas de resolver cada reto.
