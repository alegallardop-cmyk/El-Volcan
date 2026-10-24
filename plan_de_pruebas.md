# Plan de Pruebas Unitarias

**Nombre del Estudiante:** Alen Gallardo
<br />

**Componente / Módulo Principal:** Validaciones, TarjetaProducto, BotonFavorito, Productos, DetalleProducto, FormularioLogin, RutaPrivada.
<br />

**Fecha:** 23-10-2026

| ID | Componente<br>*(describe)* | Caso de Prueba<br>*(it / test)* | Preparación<br>*(Arrange: props, mocks)* | Acción<br>*(Act: fireEvent, render)* | Resultado Esperado<br>*(Assert: expect)* | Estado<br>*(Pasa / Falla)* |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Validaciones de formularios | Login: rechaza un correo sin formato válido | Objeto `datos` con correo `correo-sin-arroba` y clave `clave1234` | Se llama a `validarLogin(datos)` | `errores.correo` es "El correo no tiene un formato válido" | Pasa |
| 2 | Validaciones de formularios | Login: rechaza una contraseña de menos de 8 caracteres | Objeto `datos` con correo `admin@volcan.cl` y clave `123` | Se llama a `validarLogin(datos)` | `errores.clave` es "La contraseña debe tener al menos 8 caracteres" | Pasa |
| 3 | Validaciones de formularios | Registro: rechaza a un menor de 18 años y contraseñas distintas | Objeto `datos` con fecha de nacimiento `2015-01-01` y contraseñas distintas | Se llama a `validarRegistro(datos)` | `errores.fecnac` es "Debes ser mayor de 18 años para registrarte" y `errores.confirmarClave` es "Las contraseñas no coinciden" | Pasa |
| 4 | Validaciones de formularios | Panel de control: rechaza un producto con precio 0 | Objeto `datos` del producto con precio `0` | Se llama a `validarProducto(datos)` | `errores.precio` es "El precio debe ser mayor a 0" | Pasa |
| 5 | Componentes del catálogo | TarjetaProducto muestra el nombre y el precio con formato | Props del cilindro de 11 kg (`productoMock`) dentro de `MemoryRouter` | `render(<TarjetaProducto {...productoMock} />)` | Se muestra "Cilindro de gas 11 kg" y "$16.990" (`toBeInTheDocument`) | Pasa |
| 6 | Componentes del catálogo | BotonFavorito cambia a "★ Favorito" al hacer click | Sin props | `render(<BotonFavorito />)` y `fireEvent.click(boton)` | El botón tiene el texto "★ Favorito" (`toHaveTextContent`) | Pasa |
| 7 | Componentes del catálogo | El filtro "Comercial" muestra solo el cilindro de 15 kg | Prop `productos` con los 3 cilindros, dentro de `MemoryRouter` | `render(<Productos />)` y `fireEvent.click` en "Comercial" | Hay 1 solo título y es "Cilindro de gas 15 kg" | Pasa |
| 8 | Componentes del catálogo | DetalleProducto calcula el total según la cantidad | Prop `producto` (11 kg) y `agregarAlCarrito` vacío | `fireEvent.change` cantidad a 3 y `fireEvent.click` en "Calcular total" | Se muestra "Total: $50.970" | Pasa |
| 9 | Sesión y rutas privadas | Login muestra un error si las credenciales no existen | Prop `iniciarSesion` vacía; `localStorage` limpio | Se escriben `nadie@volcan.cl` / `clave12345` y `fireEvent.click` en "Iniciar sesión" | Se muestra "Correo o contraseña incorrectos" | Pasa |
| 10 | Sesión y rutas privadas | RutaPrivada redirige al login si no hay sesión en localStorage | `localStorage` sin usuario; `MemoryRouter` con ruta inicial `/admin` | `render` de las rutas `/admin` (protegida) y `/login` | Se muestra "Pantalla de login" y no se muestra "Panel de control" | Pasa |
