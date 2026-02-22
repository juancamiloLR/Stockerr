# Stockerr
Descripción general del sistema
Las tiendas de barrio gestionan su inventario de forma manual o con hojas de cálculo, lo que genera errores, pérdida de información y dificultad para tomar decisiones sobre reposición de productos. Este sistema nace como respuesta a esa necesidad: una aplicación web sencilla, accesible desde cualquier dispositivo con internet, que permite llevar un control completo del inventario sin requerir conocimientos técnicos avanzados.
Con él, el dueño de la tienda puede registrar sus productos con código de barras, controlar las entradas y salidas de mercancía, recibir alertas cuando un producto está por agotarse o por vencer, y consultar reportes básicos de costos y balances. Los empleados, por su parte, pueden registrar movimientos del día a día sin tener acceso a funciones administrativas sensibles.
El sistema está pensado para crecer junto con el negocio: su arquitectura modular permite incorporar en el futuro módulos de ventas, facturación electrónica o analítica, sin necesidad de reescribir la solución desde cero.
Funcionalidades

📦 Gestión de Productos
Registro de productos con campos: código de barras (estándar GS1), nombre, categoría, precio de compra, precio de venta, stock inicial, stock mínimo y fecha de vencimiento (opcional para perecederos).
Modificación de datos del producto (excepto el código de barras una vez registrado).
Eliminación lógica de productos: los productos se marcan como inactivos conservando el historial de movimientos.
Listado paginado (máx. 20 por página) con ordenamiento por nombre, precio y stock.
Búsqueda por nombre (parcial), categoría (filtro desplegable) y código de barras (exacta), con posibilidad de combinar criterios.

🔄 Control de Movimientos de Inventario
Registro de entradas de mercancía con referencia opcional (ej. número de factura).
Registro de salidas de inventario con tipo de salida y nota de referencia.
Historial detallado de todos los movimientos por producto.
Actualización automática del stock tras cada movimiento registrado.

📷 Escáner de Código de Barras
Integración con dispositivos de lectura compatibles con el estándar GS1.
Búsqueda y registro de productos directamente desde el escáner.

📊 Reportes
Reporte de costos del inventario actual.
Reporte de stock disponible por producto y categoría.
Reporte de balances (diferencia precio compra / venta).
Listado de productos próximos a vencer.

👥 Gestión de Usuarios y Acceso
Autenticación con usuario y contraseña.
Dos roles: Administrador (dueño) y Operador (empleado).
Gestión de usuarios por parte del Administrador (crear, modificar, deshabilitar operadores).

🗂️ Gestión de Categorías y Proveedores
CRUD de categorías de productos.
Registro y gestión de proveedores asociados a los productos.
Arquitectura
El sistema está construido sobre un patrón Cliente-Servidor en el que el frontend y el backend son independientes que se comunican exclusivamente a través de una API REST. Esto significa que la interfaz visual (lo que ve el usuario) está completamente separada de la lógica del negocio y los datos, lo que facilita el mantenimiento, las pruebas y futuras integraciones.
Cliente (React)  →  API REST (Node.js + Express)  →  Base de Datos (MongoDB)
Tecnologías usadas

Capa
Tecnología
Responsabilidad
Frontend
React (SPA)
Renderiza la interfaz, gestiona la navegación entre módulos y consume los endpoints de la API.
Backend
Node.js + Express
Expone la API REST, aplica las reglas de negocio, gestiona la autenticación y controla los permisos por rol.
Base de Datos
MongoDB (NoSQL)
Persiste los documentos de productos, movimientos, usuarios, categorías y proveedores.


Instalación del entorno
Requisitos previos
Para poder instalar y ejecutar el proyecto es necesario tener Node.js en su versión 18, disponible en nodejs.org. Esta instalación incluye npm automáticamente, que es el gestor de paquetes que se usa para instalar las dependencias tanto del frontend como del backend.
Para la base de datos se requiere MongoDB Atlas. Como alternativa, es posible usar MongoDB Community server, que se puede instalar localmente desde mongodb.com.
El proyecto también requiere Git para clonar el repositorio, descargable desde git-scm.com. En cuanto al editor de código, se recomienda usar Visual Studio Code. Para el despliegue y la ejecución del entorno de desarrollo se utiliza Docker, que permite correr todos los servicios del proyecto de forma consistente sin necesidad de configuraciones adicionales en cada máquina; está disponible en docker.com.
La aplicación en sí no requiere ninguna instalación especial en el navegador, basta con cualquier navegador moderno como Chrome, Firefox o Edge.

Clonar el repositorio
Para obtener una copia local del proyecto, primero es necesario tener Git instalado en la máquina. Una vez confirmado esto, se abre una terminal y se navega hasta la carpeta donde se quiere guardar el proyecto usando el comando cd. Desde ahí, se ejecuta “git clone” seguido de la URL del repositorio, que se puede copiar directamente desde el botón verde "Code" en la página del repositorio en GitHub. El comando completo se vería así:
git clone https://github.com/usuario/nombre-del-repositorio.git
Esto creará automáticamente una carpeta con el nombre del repositorio en el directorio actual y descargará todo el contenido del proyecto dentro de ella. Para entrar a esa carpeta se usa cd nombre-del-repositorio, y a partir de ahí ya se puede comenzar con la instalación de dependencias y la configuración del entorno.
Ejecutar el proyecto
Una vez clonado el repositorio, se abre Visual Studio Code y desde el menú superior se selecciona "File" y luego "Open Folder" para abrir la carpeta del proyecto. Con el proyecto abierto, se accede a la terminal integrada de Visual Studio Code desde el menú "Terminal" seleccionando "New Terminal", lo que abrirá una consola directamente en la raíz del proyecto.
Desde esa terminal se instalan las dependencias del proyecto ejecutando npm install, lo cual descargará todos los paquetes necesarios definidos en el archivo package.json. Este paso solo es necesario la primera vez o cuando se agreguen nuevas dependencias al proyecto.
Antes de iniciar la aplicación, es necesario crear un archivo .env en la raíz del proyecto con las variables de entorno correspondientes, como la cadena de conexión a MongoDB Atlas y el puerto del servidor.
Finalmente, para iniciar el proyecto se ejecuta npm run dev si se está en modo desarrollo, o npm start para correrlo en modo producción. También basta con ejecutar docker compose up y este se encargará de levantar todos los servicios automáticamente.
