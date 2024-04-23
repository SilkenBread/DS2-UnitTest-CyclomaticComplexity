# Laboratorio Pruebas Unitarias y la complejidad ciclomática
Pruebas Unitarias, Complejidad Ciclomática

## i. Introducción
En el mundo actual del desarrollo de software, la calidad y la eficiencia del código son aspectos clave para garantizar la entrega exitosa de aplicaciones y sistemas. Este taller tiene como objetivo proporcionar a los estudiantes una comprensión sólida de las pruebas unitarias, la evaluación de la calidad del código y el análisis de la complejidad ciclomática. A través de ejercicios prácticos y ejemplos de la vida real, los participantes aprenderán cómo aplicar estas técnicas y herramientas para mejorar la calidad y el rendimiento de su código.

## ii. Requisitos
Conocimientos básicos de programación y JavaScript
Node.js y npm instalado
Entorno de desarrollo integrado (IDE) o editor de código (visual studio)

## iii. Código JavaScript
#### 1. Crear un directorio llamado tallerpruebas e instalar jest
```bash
cd tallerpruebas
npm init -y
npm install --save jest
```

#### 2. Modifica el archivo package.json para agregar el siguiente script:
```json
"scripts": {
  "test": "jest"
}
```

#### 3. Crea un archivo index.js que exporta unas funciones para una calculadora
```javascript
// index.js
function sum(a, b) {
  return a + b;
}

function subtract(a, b) {
  return a - b;
}

function multiply(a, b) {
  return a * b;
}

function divide(a, b) {
  if (b === 0) {
    throw new Error("Division by zero is not allowed");
  }
  return a / b;
}

module.exports = {
  sum,
  subtract,
  multiply,
  divide
};
```
#### 4. Ahora, crea un archivo index.test.js que contiene las pruebas para todas estas funciones:
```javascript
// index.test.js
const { sum, subtract, multiply, divide } = require("./index");

test("sums two numbers", () => {
  expect(sum(1, 2)).toBe(3);
  expect(sum(-1, 1)).toBe(0);
  expect(sum(0, 0)).toBe(0);
});

test("subtracts two numbers", () => {
  expect(subtract(3, 2)).toBe(1);
  expect(subtract(-1, 1)).toBe(-2);
  expect(subtract(0, 0)).toBe(0);
});

test("multiplies two numbers", () => {
  expect(multiply(3, 2)).toBe(6);
  expect(multiply(-1, 1)).toBe(-1);
  expect(multiply(0, 0)).toBe(0);
});

test("divides two numbers", () => {
  expect(divide(6, 2)).toBe(3);
  expect(divide(-6, 2)).toBe(-3);
  expect(divide(6, -2)).toBe(-3);
  expect(() => divide(6, 0)).toThrow("Division by zero is not allowed");
});

```

Ahora ejecuta las pruebas con el comando npm run  test esto ejecutará las pruebas y mostrará los resultados en la consola.
```bash
npm run test
```

#### 5. Ahora, vamos a agregar pruebas de cobertura y evaluar la complejidad ciclomática. Por favor instalar ESLint con el siguiente comando
```bash
npm install eslint eslint-plugin-complexity --save-dev
```

Crear un archivo eslint.config.js con el siguiente contenido 
```javascript
module.exports = [
    {
        rules: {
            "complexity":["warn", 5],
            semi: "error",
            "prefer-const": "error"
        }
    }
];

```

Y ahora ejecuta el comando npm run lint por el momento el código no tiene complejidad ciclomática alta ( No se vera nada en consola) .  En consecuencia, para poder testear el funcionamiento de ESLint vamos a agregar una función que tiene complejidad 8

Agrega el siguiente código al archivo index.js
```javascript
function complexFunction(a, b, c, d, e, f) {
if (a > 0) {
      if (b > 0) {
        if (c > 0) {
          return "a > 0, b > 0, c > 0";
        } else {
          return "a > 0, b > 0, c <= 0";
        }
      } else {
        if (c > 0) {
          return "a > 0, b <= 0, c > 0";
        } else {
          return "a > 0, b <= 0, c <= 0";
        }
      }
    } else {
      if (d > 0) {
        if (e > 0) {
          if (f > 0) {
            return "a <= 0, d > 0, e > 0, f > 0";
          } else {
            return "a <= 0, d > 0, e > 0, f <= 0";
          }
        } else {
          return "a <= 0, d > 0, e <= 0";
        }
      } else {
        return "a <= 0, d <= 0";
      }
    }
  }
```

```bash
npm run lint
```

## iv. Configuración Coverage
En el archivo package.json agrega un nuevo script test:coverage": "jest --coverage

```json
scripts": {
    "test": "jest",
    "lint": "eslint .",
    "test:coverage": "jest --coverage"
  }
```

```bash
npm run test:coverage
```

Se puede evidenciar que debido a que existen líneas sin cobertura y sin propósito, también que no se utilizan todas ramas,  ni funciones. Para arreglar este inconveniente, vamos a borrar la funcion ComplexFuntion y a ejecutar nuevamente el coverage

Ahora es un código de mejor calidad
Si desea ver de forma más gráfica el resultado, en la carpeta coverage puede encontrar el resultado con una tabla en html 

![image](https://github.com/juanrubio110729/DS2-UnitTest-CyclomaticComplexity/assets/105334586/4674680a-f14f-4222-8102-2279d242d070)

