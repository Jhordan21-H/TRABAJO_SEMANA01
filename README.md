---
date: 2025-08-31
---

# 5) Bucles (for, while, do…while)

## for clásico

Sirve para repetir un bloque un número conocido de veces (control por contador: inicialización → condición → actualización).

```javascript
const n = 5;
let suma = 0;
for (let i = 1; i <= n; i++) {
  suma += i;
}
console.log(suma); // 15

```

Variantes útiles


•	for...of: recorre valores de iterables (arrays, strings, Maps, Sets).

•	for...in: recorre claves (propiedades enumerables) —útil para objetos, con cuidado.

```javascript
// for...of (valores)
const nums = [3, 7, 2, 9];
let max = -Infinity;
for (const x of nums) {
  if (x > max) max = x;
}
console.log(max); // 9

// for...in (claves) en objetos
const persona = { nombre: "Ana", edad: 21 };
for (const key in persona) {
  if (Object.hasOwn(persona, key)) { // evita propiedades heredadas
    console.log(key, "→", persona[key]);
  }
}


```

Tip: Para objetos, muchas veces es más claro Object.entries(obj).forEach(([k,v]) => ...)
## Explicación gráfica 
En este ejemplo observaremos un caso sobre como definir una lista de personas y aplicar for ,  for ..of y for ... in
```javascript
var listaPersonas = [
 {"nombre": "pepe", "apellidos": "perez"},
 {"nombre": "ana", "apellidos": "gomez"},
 {"nombre": "almudena", "apellidos": "blanco"}
];
```
![Image](https://github.com/user-attachments/assets/741004b5-1dd6-4efe-affe-46af1d2c7ee8)
<img width="1591" height="81" alt="image" src="https://github.com/user-attachments/assets/b33f802f-e0e8-489a-9f9e-8c36416a69f8" />

## while

Repite mientras la condición sea verdadera (puede ejecutarse 0 veces).

```javascript
// Factorial con while
const n = 5;
let r = 1, i = 2;
while (i <= n) {
  r *= i;
  i++;
}
console.log(r); // 120

```
Lo más clásico para poder ejecutar es usar un ciclo for 
```javascript
for (var i = 0; i < listaPersonas.length; i++) {
 console.log(listaPersonas[i].nombre);
 console.log(listaPersonas[i].apellidos);
}
```
![Image](https://github.com/user-attachments/assets/2079bcc2-8b86-4f96-9d76-18445392c1e6)
<img width="1617" height="81" alt="image" src="https://github.com/user-attachments/assets/03de78a7-3132-40e6-bd86-31196d4f4556" />
Como seria utilizando el ciclo for ...of
```javascript
for (var persona of listaPersonas) {
console.log(persona.nombre);
console.log(persona.apellidos);
}
```
![Image](https://github.com/user-attachments/assets/a1297200-aa42-493a-9f04-f323b61c48e1)
<img width="1607" height="81" alt="image" src="https://github.com/user-attachments/assets/6a85ef01-adad-49df-90c1-404ca7728d34" />

Como seria utilizando el ciclo for ... in 
```javascript
 for (var propiedad in listaPersonas) {
 // Imprime el valor de cada propiedad
 console.log(listaPersonas[propiedad]);
 }
```
![Image](https://github.com/user-attachments/assets/6b203890-fe4e-4fb4-b667-46456b18911a)
<img width="1612" height="81" alt="image" src="https://github.com/user-attachments/assets/c307e50f-ab23-429f-8f82-f1c6fff587ee" />

## do…while

Ejecuta el bloque al menos una vez, y luego verifica la condición.

```javascript
// Ejecuta al menos una vez
let conteo = 0;
do {
  console.log("Paso", conteo);
  conteo++;
} while (conteo < 3);
// Imprime Paso 0, Paso 1, Paso 2

```

## break y continue

•	break sale por completo del bucle.

•	continue salta a la siguiente iteración.

```javascript
// Suma solo impares hasta encontrar el 0
const datos = [5, 3, 8, 11, 0, 7];
let sumaImpares = 0;
for (const n of datos) {
  if (n === 0) break;       // corto el bucle
  if (n % 2 === 0) continue; // salto pares
  sumaImpares += n;
}
console.log(sumaImpares); // 5 + 3 + 11 = 19

```

Errores comunes: bucles infinitos (while(true) sin break), modificar el array mientras lo recorres, usar for...in en arrays (te da índices como strings y puede incluir propiedades añadidas).

# 6) Funciones (declaración, expresiones, parámetros, retorno)

## Declaración de función

•	Tiene hoisting: puedes llamarla antes de su definición.

```javascript
console.log(suma(2, 3)); // 5
function suma(a, b) {
  return a + b;
}

```

## Expresión de función

•	Se asigna a una variable. No puedes usarla antes de la línea donde se define.

```javascript
const resta = function(a, b) {
  return a - b;
};
console.log(resta(7, 4)); // 3

```

## Arrow function (=>)

•	Sintaxis corta; no tiene su propio this ni arguments. No sirve como constructor.

```javascript
const mult = (a, b) => a * b;          // retorno implícito
const cuadrado = x => x * x;           // un parámetro → sin paréntesis
const toObj = (k, v) => ({ [k]: v });  // devolver objeto → usa paréntesis
console.log(mult(3, 4), cuadrado(5), toObj("id", 10));

```

## Parámetros

### Valores por defecto

```javascript
function saludar(nombre = "Invitado", idioma = "es") {
  return idioma === "es" ? `Hola, ${nombre}` : `Hello, ${nombre}`;
}
console.log(saludar());                // Hola, Invitado
console.log(saludar("Ana", "en"));     // Hello, Ana

```

## Parámetros rest (...)

### Agrupa argumentos adicionales en un array.

```javascript
function sumarTodos(...nums) {
  return nums.reduce((acc, n) => acc + n, 0);
}
console.log(sumarTodos(1, 2, 3, 4)); // 10

```

### Desestructuración en parámetros (con defaults)

Ideal para “parámetros nombrados” mediante objeto.

```javascript
function crearUsuario({ nombre, rol = "user", activo = true }) {
  return { nombre, rol, activo, creadoEn: new Date() };
}
console.log(crearUsuario({ nombre: "Ana", rol: "admin" }));

```

## Retorno (return)

•	Finaliza la función y devuelve un valor.

•	Puedes retornar objetos/arrays para “múltiples valores”.

```javascript
function dividir(a, b) {
  if (b === 0) return { ok: false, error: "División por cero" };
  return { ok: true, resultado: a / b };
}
console.log(dividir(10, 2)); // { ok: true, resultado: 5 }
console.log(dividir(5, 0));  // { ok: false, error: ... }

```
