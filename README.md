# Proyecto final de analisis y sistemas
<p align="center">
  <img src="https://github.com/JoseAngelAlba/Examen-Final/blob/main/Imagen1.png" />
</p>
<p align="center">Alumno</p>
            José Angel Alba 
<p align="center">Matrícula</p>
                2022-0398
<p align="center">Docente</p>
        Prof. Lizandro Ramírez
 <p align="center">Código</p>
                ISC_010
<p align="center">Asignatura</p>
            Análisis de Sistemas
<p align="center">Fecha de Entrega</p>
                10-04-2023



# Worker y Redis
Este código crea un cliente Redis que se suscribe a un canal llamado "insert". Cuando se publica un mensaje en ese canal, se llama a la función "fib" con el valor del mensaje como argumento. La función "fib" calcula el número de Fibonacci para ese valor y lo guarda en Redis con la clave "message" y el valor del número de Fibonacci.
Algunos posibles casos de mejora para este código podrían incluir:
Manejo de errores: el código no maneja explícitamente los errores que pueden ocurrir al comunicarse con Redis. Podría ser beneficioso agregar algún tipo de manejo de errores para asegurarse de que el código se comporte correctamente en caso de una excepción.
Pruebas unitarias: sería beneficioso agregar pruebas unitarias para la función "fib" y para el manejo de mensajes del cliente Redis. Esto ayudaría a garantizar que el código se comporte correctamente en una variedad de situaciones y ayudaría a detectar errores temprano.
Separación de responsabilidades: el código actualmente mezcla la lógica de almacenamiento de Redis con la lógica de cálculo de números de Fibonacci. Sería beneficioso separar estas responsabilidades en diferentes módulos o funciones para mantener el código más organizado y modular.
Configuración centralizada: el código actualmente tiene la configuración de Redis como parte del código fuente. Sería mejor mover esta configuración a un archivo de configuración externo o una variable de entorno para que sea más fácil de cambiar sin necesidad de modificar el código fuente.
Mejora de rendimiento: si bien el código actual es funcional, no es muy eficiente. La función "fib" se llama de forma recursiva, lo que puede generar un gran número de llamadas para valores grandes de "index". También es posible que el código pueda beneficiarse de una mejor estrategia de almacenamiento en caché o de una mejor integración con la base de datos subyacente.

# React
Este código es una aplicación básica de React que utiliza React Router para mostrar dos páginas diferentes al usuario.
La aplicación consiste en un componente funcional llamado App que renderiza el contenido. Dentro del componente, se utiliza BrowserRouter de React Router para enrutar la navegación del usuario.
El encabezado de la página incluye una imagen del logo de la aplicación, un enlace externo a la página de documentación de React, y dos enlaces internos que utilizan el componente Link para navegar entre páginas.
El componente Route se utiliza para definir las rutas y qué componente se mostrará en cada ruta. En este caso, la ruta raíz mostrará el componente Fib, y la ruta "otherpage" mostrará el componente OtherPage.
El archivo OtherPage.js y Fib.js serán otros componentes que se importarán en este archivo.
Este código define un componente de React llamado Fib, que obtiene y muestra información relacionada con la secuencia de Fibonacci.
El componente tiene un estado que contiene tres variables:
seenIndexes: una matriz de objetos que representan índices de secuencia de Fibonacci que se han calculado previamente.
valores: un objeto que contiene pares clave-valor, donde cada clave representa un índice de secuencia de Fibonacci y cada valor es el resultado del cálculo de ese índice.
índice: una cadena que representa el valor de entrada para un nuevo índice de secuencia de Fibonacci.
El método componentDidMount se llama cuando se monta el componente y realiza dos llamadas a la API para obtener los índices vistos y los datos de valores del servidor.

Se llama al método handleSubmit cuando el usuario envía un nuevo valor de índice a través de un formulario. Hace una llamada API al servidor para calcular el valor de Fibonacci para ese índice y luego borra la variable de estado del índice.

El método renderSeenIndexes mapea sobre la matriz seenIndexes y devuelve una lista de números de índice separados por comas.

El método renderValues recorre el objeto de valores y crea una matriz de elementos JSX que representan los valores calculados para cada índice. Luego, estos elementos se representan en la interfaz de usuario del componente.

En general, este componente permite al usuario ingresar un nuevo índice de secuencia de Fibonacci, ver una lista de índices calculados previamente y ver los valores calculados para cada índice.

# Express, Redis y Postgre
La app tiene un servidor Node.js que utiliza Express para manejar solicitudes HTTP. Hay tres componentes principales: un cliente PostgreSQL para almacenar valores, un cliente Redis para almacenar valores que están siendo calculados, y una aplicación Express que maneja solicitudes HTTP y comunica el almacenamiento de datos entre el cliente PostgreSQL y el cliente Redis.
La configuración inicial del servidor crea instancias del cliente PostgreSQL y el cliente Redis y los configura con los detalles de conexión especificados en keys.js.
El código define varios manejadores de ruta HTTP para diferentes solicitudes. Por ejemplo, la ruta / simplemente envía una respuesta de Hi. La ruta /values/all obtiene todos los valores almacenados en la base de datos PostgreSQL y los devuelve como una respuesta HTTP. La ruta /values/current obtiene todos los valores actualmente en el almacenamiento Redis y los devuelve como una respuesta HTTP. La ruta /values acepta un índice enviado por un cliente, lo almacena en Redis con un valor temporal "Nothing yet!" y publica un mensaje para que un trabajador lo procese. Luego inserta el índice en la base de datos PostgreSQL y envía una respuesta HTTP de éxito.

