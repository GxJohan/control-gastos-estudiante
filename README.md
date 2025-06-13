# Control de Gastos para Estudiantes

Este proyecto es una aplicación web diseñada para ayudar a los estudiantes a llevar un control detallado de sus gastos. La aplicación permite registrar, visualizar, categorizar y analizar los gastos de una manera sencilla e intuitiva. Está construida con tecnologías modernas de desarrollo web y diseñada para ser fácil de entender, mantener y extender.

## ✨ Características Principales

- **Registro de Gastos**: Formulario intuitivo para agregar nuevos gastos con descripción, cantidad, categoría y fecha.
- **Visualización de Gastos**: Lista completa de todos los gastos registrados, con la posibilidad de ordenarlos por fecha o por cantidad.
- **Eliminación de Gastos**: Opción para eliminar gastos individuales de la lista.
- **Resumen Detallado**: Dashboard con un resumen completo de los gastos, incluyendo:
    - Total general gastado.
    - Desglose de gastos por categoría.
    - Barra de progreso visual para cada categoría, mostrando su peso porcentual.
    - Identificación del gasto más alto realizado.
- **Persistencia de Datos**: Los datos de los gastos se guardan localmente en el navegador (`localStorage`), por lo que la información no se pierde al recargar la página.
- **Diseño Responsivo**: Interfaz adaptable a diferentes tamaños de pantalla.

## 🛠️ Stack Tecnológico

- **Frontend**:
    - [**React 19**](https://react.dev/): Biblioteca para construir interfaces de usuario.
    - [**TypeScript**](https://www.typescriptlang.org/): Superset de JavaScript que añade tipado estático.
    - [**Vite**](https://vitejs.dev/): Herramienta de desarrollo frontend extremadamente rápida.
    - [**React Router DOM**](https://reactrouter.com/): Para la gestión de rutas en la aplicación.
- **Estilos**:
    - CSS puro con una estructura modular por componente.
- **Linting**:
    - [**ESLint**](https://eslint.org/): Para identificar y corregir problemas en el código.

## 📂 Estructura del Proyecto

El proyecto sigue una estructura de carpetas lógica y escalable:

```
/
├── public/                # Archivos estáticos
├── src/
│   ├── assets/            # Imágenes y otros recursos
│   ├── components/        # Componentes reutilizables
│   │   └── GastoItem.tsx  # Componente para un solo item de gasto
│   ├── pages/             # Componentes que representan páginas completas
│   │   ├── AgregarGasto.tsx
│   │   ├── Inicio.tsx
│   │   ├── ListaGastos.tsx
│   │   └── Resumen.tsx
│   ├── types/             # Definiciones de tipos de TypeScript
│   │   └── Gasto.ts
│   ├── App.tsx            # Componente principal y enrutador
│   ├── main.tsx           # Punto de entrada de la aplicación
│   └── ...                # Archivos de configuración y estilos
├── .gitignore
├── package.json
└── README.md
```

## 🧠 Lógica y Componentes Clave

### 1. `App.tsx`
Es el componente raíz que configura el enrutador (`react-router-dom`) y define la estructura general de la aplicación, incluyendo el encabezado, el contenido principal y el pie de página.

### 2. Gestión de Datos (`localStorage`)
La aplicación utiliza el `localStorage` del navegador para persistir los datos de los gastos.
- **Guardado**: Al agregar un nuevo gasto en `AgregarGasto.tsx`, el nuevo arreglo de gastos se serializa a JSON y se guarda en `localStorage` bajo la clave `'gastos'`.
- **Lectura**: Los componentes `ListaGastos.tsx` y `Resumen.tsx` leen los datos de `localStorage` al montarse para mostrar la información actualizada.

### 3. Tipos (`types/Gasto.ts`)
Para asegurar la consistencia de los datos en toda la aplicación, se define la interfaz `Gasto`:

```typescript
export interface Gasto {
  id: string;
  descripcion: string;
  cantidad: number;
  categoria: 'comida' | 'transporte' | 'entretenimiento' | 'estudios' | 'otros';
  fecha: string;
}
```

### 4. Páginas (`pages/`)

- **`Inicio.tsx`**: Página de bienvenida que ofrece una breve introducción y enlaces a las secciones principales.
- **`AgregarGasto.tsx`**: Contiene el formulario para añadir un nuevo gasto. Utiliza el estado local de React (`useState`) para manejar los datos del formulario. Al enviar, crea un nuevo objeto `Gasto`, lo añade a la lista existente en `localStorage` y redirige al usuario a la lista de gastos.
- **`ListaGastos.tsx`**: Muestra todos los gastos guardados. Permite ordenar la lista por fecha o por cantidad y delegada la renderización de cada item al componente `GastoItem`.
- **`Resumen.tsx`**: La página más compleja en términos de lógica.
    1. Carga los gastos de `localStorage`.
    2. Calcula el total general.
    3. Agrupa los gastos por categoría, sumando los totales y contando el número de gastos en cada una.
    4. Calcula el porcentaje que representa cada categoría sobre el total.
    5. Identifica el gasto individual de mayor importe.
    6. Muestra toda esta información de forma visual, incluyendo barras de progreso.

### 5. Componentes (`components/`)

- **`GastoItem.tsx`**: Componente de presentación que recibe un objeto `Gasto` y una función `onEliminar`. Muestra la información del gasto y un emoji representativo de la categoría.

## 🚀 Instalación y Uso Local

Para ejecutar este proyecto en tu máquina local, sigue estos pasos:

1.  **Clona el repositorio:**
    ```bash
    git clone https://github.com/tu-usuario/control-gastos-estudiante.git
    cd control-gastos-estudiante
    ```

2.  **Instala las dependencias:**
    ```bash
    npm install
    ```

3.  **Ejecuta el servidor de desarrollo:**
    ```bash
    npm run dev
    ```
    La aplicación estará disponible en `http://localhost:5173` (o el puerto que Vite asigne).

## 🔮 Posibles Mejoras Futuras

- **Gráficos Avanzados**: Implementar librerías como `Chart.js` o `D3.js` para visualizaciones más ricas en la página de resumen.
- **Edición de Gastos**: Añadir la funcionalidad para editar un gasto ya existente.
- **Filtrado de Gastos**: Permitir filtrar los gastos por categoría o por rango de fechas en la `ListaGastos`.
- **Autenticación de Usuarios**: Implementar un sistema de login para que múltiples usuarios puedan usar la aplicación de forma privada.
- **Backend y Base de Datos**: Conectar la aplicación a un backend (Node.js, Python, etc.) y una base de datos (PostgreSQL, MongoDB) para almacenar los datos de forma persistente y segura.
- **PWA (Progressive Web App)**: Convertir la aplicación en una PWA para que pueda ser "instalada" en dispositivos y funcionar offline.