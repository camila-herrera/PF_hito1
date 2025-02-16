# PF_hito1
Proyecto Final del Marketplace de Seguridad – Hito 1
by Herrera Camila & Marín Luis

Introducción
El marketplace de seguridad es una aplicación web diseñada para la venta de implementos de defensa, con roles específicos para usuarios, clientes y administradores. Este documento detalla cada componente del Hito 1, incluyendo diseño de interfaz, navegación, dependencias, base de datos y contrato de API REST.

1. Diseño de la Interfaz Gráfica (Wireframes Finales)
Vistas Públicas (Sin Login):
Página Principal (Home): Lista de productos sin precios. Navbar solo con opciones de Login y Register.

Vistas Privadas (Con Login):
Usuarios:
Navbar: Cambia para mostrar "Perfil" y habilitar el carrito de compras.
Perfil: Historial de compras con detalles y botón para repetir compras.
Home: Ahora muestra precios y desbloquea el carrito.
Cliente:
Navbar: Muestra "Pedidos" en lugar de "Perfil".
Pedidos: Lista de todos los pedidos generados, acceso al detalle completo de cada pedido, opción de actualizar estados y deshabilitar/habilitar productos por stock.
Admin:
Navbar: Acceso a gestión completa.
Funciones: Crear, editar y eliminar productos, gestionar usuarios y pedidos.
Se incluirán bocetos diseñados en Figma que representen cada vista: página principal, perfil de usuario, carrito, pedidos de cliente y panel de administración. Estos bocetos mostrarán la disposición de los elementos, navegación y componentes visuales.



2. Navegación
Público: Solo home, login y registro.
Usuarios Logueados: Home con precios, carrito, perfil con historial.
Cliente: Pedidos completos y gestión.
Admin: Gestión total.
Se utilizará React Router para gestionar la navegación entre vistas públicas y privadas, respetando el flujo definido: home, login/registro, perfil, carrito, pedidos y administración.


3. Dependencias
Frontend: React, Vite, Bootstrap, React Router, Redux, Axios.
Backend: Express.js, PostgreSQL, pgAdmin, JWT, bcryptjs.

4. Base de Datos:
Tablas principales:
Usuarios:
id_usuario (PK): INT
nombre: VARCHAR
email: VARCHAR
contraseña: VARCHAR (guardada de forma segura, encriptada)
rol: ENUM('usuario', 'cliente', 'admin') — Definir los roles según el acceso.
fecha_registro: DATETIME

Productos:
id_producto (PK): INT
nombre: VARCHAR
descripcion: TEXT
precio: DECIMAL
categoria: VARCHAR
stock: INT
imagen_url: VARCHAR
fecha_agregado: DATETIME

Pedidos:
id_pedido (PK): INT
id_usuario (FK): INT (relacionado con la tabla de Usuarios)
estado: ENUM('pendiente', 'enviado', 'entregado')
total: DECIMAL
fecha_pedido: DATETIME

Detalle_Pedidos:
id_detalle (PK): INT
id_pedido (FK): INT (relacionado con la tabla de Pedidos)
id_producto (FK): INT (relacionado con la tabla de Productos)
cantidad: INT
subtotal: DECIMAL

Transacciones:
id_transaccion (PK): INT
id_pedido (FK): INT
fecha_transaccion: DATETIME
monto: DECIMAL
metodo_pago: ENUM('tarjeta', 'transferencia', 'otros')
estado: ENUM('completada', 'fallida')


Relaciones entre tablas:
Un usuario puede tener muchos pedidos.
Un pedido puede tener muchos productos a través de la tabla de detalle_pedidos.
Cada pedido tiene una transacción asociada.
img adjunta




5. Contrato de la API REST:
Se incluirá documentación en Polacode para mostrar ejemplos de código de los endpoints definidos:
POST /usuarios/registro – Registrar usuario.
POST /usuarios/login – Iniciar sesión.
GET /usuarios/:id/compras – Historial de compras.
POST /publicaciones – Crear publicación.
GET /publicaciones – Listar publicaciones.
POST /compras – Realizar compra.
PATCH /clientes/pedidos/:id – Actualizar estado de pedido.
POST /pagos – Registrar pago.
Cada endpoint se describirá con parámetros de solicitud y respuestas esperadas que se encuentra en api-docs.js


