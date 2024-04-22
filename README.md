# Laboratorio Pruebas Unitarias y la complejidad ciclomática
Pruebas Unitarias, Complejidad Ciclomática

## i. Introducción
En el mundo actual del desarrollo de software, la calidad y la eficiencia del código son aspectos clave para garantizar la entrega exitosa de aplicaciones y sistemas. Este taller tiene como objetivo proporcionar a los estudiantes una comprensión sólida de las pruebas unitarias, la evaluación de la calidad del código y el análisis de la complejidad ciclomática. A través de ejercicios prácticos y ejemplos de la vida real, los participantes aprenderán cómo aplicar estas técnicas y herramientas para mejorar la calidad y el rendimiento de su código.

## ii. Requisitos
Conocimientos básicos de programación y JavaScript
Node.js y npm instalado
Entorno de desarrollo integrado (IDE) o editor de código (visual studio)

## iii. Código JavaScript
### 1. Crear un directorio llamado tallerpruebas e instalar jest
```bash
cd tallerpruebas
npm init -y
npm install --save jest
```

### 2. Modifica el archivo package.json para agregar el siguiente script:
```json
"scripts": {
  "test": "jest"
}
```

### 3. Crea un archivo index.js que exporta unas funciones para una calculadora
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
