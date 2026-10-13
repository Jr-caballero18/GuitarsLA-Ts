# GuitarsLA-Ts

Aplicación web de una tienda de guitarras desarrollada con React y TypeScript. Permite visualizar una colección de instrumentos y administrar un carrito de compras mediante componentes reutilizables y un hook personalizado.

## Índice

- [1. Visión General del Proyecto](#1-visión-general-del-proyecto)
- [2. Ficha Técnica y Tecnologías](#2-ficha-técnica-y-tecnologías)
- [3. Arquitectura e Implementación en React](#3-arquitectura-e-implementación-en-react)
- [4. Patrones y Buenas Prácticas](#4-patrones-y-buenas-prácticas)
- [5. Manejo de Estado y Persistencia](#5-manejo-de-estado-y-persistencia)
- [6. Puesta en Marcha](#6-puesta-en-marcha)

---

## 1. Visión General del Proyecto

### 1.1 Nombre y propósito de la aplicación

**Nombre:** GuitarsLA-Ts.

GuitarsLA-Ts es una aplicación web interactiva que simula una tienda virtual de instrumentos musicales. Su propósito principal es permitir a los usuarios consultar un catálogo de guitarras, agregar instrumentos a un carrito de compras interactivo, modificar las cantidades de cada producto, eliminar elementos individualmente, vaciar el carrito completo y calcular el importe total a pagar en tiempo real.

La aplicación fue desarrollada utilizando React y TypeScript, estructurando el sistema en componentes reutilizables y desacoplando la lógica de negocio en un hook personalizado (*Custom Hook*).

### 1.2 Problema que resuelve

La aplicación resuelve la necesidad de administrar las interacciones de un carrito de compras en una tienda digital sin necesidad de recargar la página ni realizar peticiones innecesarias al servidor. Facilita la exploración visual de productos, el cálculo dinámico de subtotales y la persistencia de la selección del usuario durante su sesión de navegación.

### 1.3 Funcionalidades principales

- Visualización dinámica del catálogo de guitarras.
- Presentación detallada del nombre, imagen, descripción y precio de cada instrumento[cite: 3].
- Agregado de productos al carrito de compras desde el catálogo[cite: 1, 3].
- Incrementar y decrementar unidades de un producto dentro del carrito[cite: 1, 4].
- Eliminación individual de artículos del carrito mediante su identificador[cite: 1, 4].
- Opción para vaciar completamente el carrito de compras[cite: 1, 4].
- Cálculo automatizado e inmutable del monto total a pagar[cite: 1].
- Evaluación de estado derivado para detectar si el carrito se encuentra vacío (`isEmpty`)[cite: 1, 4].
- Conservación automática de los productos seleccionados mediante `localStorage`.

### 1.4 Capturas de pantalla de la aplicación

#### Página principal y colección de guitarras
![Página Principal](./public/img/logo.svg)

#### Carrito de compras
![Carrito de compras](./public/img/cart.png)



### 1.5 Repositorio y despliegue

- **Repositorio de GitHub:** [https://github.com/Jr-caballero18/GuitarsLA-Ts.git](https://github.com/Jr-caballero18/GuitarsLA-Ts.git)
- **Despliegue en producción:** No se cuenta con una URL de producción activa confirmada. La aplicación se ejecuta en entorno local en `http://localhost:5173`.

---

## 2. Ficha Técnica y Tecnologías

### 2.1 Lenguajes de programación

| Tecnología | Uso en el proyecto |
| :--- | :--- |
| **TypeScript** | Proporciona tipado estático estricto para describir las propiedades de componentes, modelos de datos y estructuras de productos (`.tsx` y `.ts`)[cite: 1, 2, 3, 4]. |
| **JavaScript ES6+** | Base de ejecución de la aplicación React; se utilizan funciones flecha, desestructuración, iteradores y métodos inmutables de arreglos (`map`, `filter`)[cite: 1, 3, 4]. |
| **TSX** | Sintaxis que permite escribir componentes de React combinando TypeScript con la estructura declarativa de JSX[cite: 1, 2, 3, 4]. |
| **CSS** | Define los estilos globales y las reglas de presentación de la aplicación[cite: 2]. |

**Nivel de tipado:** Tipado estático mediante TypeScript. Se emplean definiciones explícitas (`types.d.ts`) como `CartProps` y `GuitarProps` para garantizar la integridad de los datos en el flujo de la aplicación[cite: 3, 4].

### 2.2 Framework y librerías de interfaz

| Tecnología | Función |
| :--- | :--- |
| **React 18** | Construcción de la interfaz de usuario mediante componentes funcionales y hooks declarativos[cite: 2]. |
| **React DOM** | Encargado del renderizado y montaje de la aplicación en el DOM del navegador[cite: 2]. |
| **Bootstrap / Utility CSS** | Maquetación responsiva, grillas (`container-xl`, `row`, `col-md-6`), tablas y estilos para botones[cite: 1, 3, 4]. |
| **CSS** | Estilos globales y personalización de la interfaz[cite: 2]. |

### 2.3 Entorno de desarrollo y herramientas

| Herramienta | Función |
| :--- | :--- |
| **Vite** | Servidor de desarrollo ultrarrápido y empaquetador de módulos (*bundler*)[cite: 2]. |
| **npm** | Gestor de paquetes utilizado para instalar y administrar las dependencias del proyecto[cite: 2]. |
| **Git** | Sistema de control de versiones distribuido. |
| **GitHub** | Plataforma de alojamiento para el repositorio remoto. |
| **Visual Studio Code** | Editor de código fuente utilizado para el desarrollo. |

### 2.4 Dependencias clave

- `react`: Librería principal para la creación de componentes y gestión de estados/hooks[cite: 2].
- `react-dom`: Módulo para renderizar la aplicación en el entorno web[cite: 2].
- `typescript`: Compilador que añade verificación de tipos en tiempo de desarrollo[cite: 2].
- `@types/react` / `@types/react-dom`: Paquetes con definiciones de tipos para React[cite: 2].
- `vite`: Herramienta de compilación y servidor local[cite: 2].

*Nota:* No se utiliza un cliente HTTP externo ni enrutamiento dinámico; la información de los productos se importa desde una colección estática local.

---

## 3. Arquitectura e Implementación en React

### 3.1 Organización de la aplicación

La aplicación está organizada en componentes presentacionales, un contenedor principal y lógica encapsulada en un Custom Hook:
