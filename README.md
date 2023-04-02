# Proyecto final de analisis y sistemas

 ![Ucateci Logo](https://github.com/JoseAngelAlba/Examen-Final/blob/main/Imagen1.png)
  

  
- Alumno: José Angel Alba
- Matrícula: 2022-0398
- Docente: Prof. Lizandro Ramírez
- Código: ISC 010 001
- Asignatura: Análisis de Sistemas
- Fecha de Entrega: 10-04-2023

# Introducción
En este análisis se aborda el estudio de los diferentes componentes que conforman una aplicación React. Estos componentes utilizan una base de datos Redis y Postgre, API Rest, un cliente web con React, y un servicio Worker para simular cálculos complejos. En el caso de Redis y el servicio Worker, se muestra cómo se realiza un cálculo de Fibonacci y se guarda en Redis. Sin embargo, se sugieren algunas mejoras, como manejar errores, agregar pruebas unitarias, separar responsabilidades, configuración centralizada y mejorar el rendimiento. En cuanto a Express, Redis y Postgre, se tiene un servidor Node.js que utiliza Express para manejar solicitudes HTTP, un cliente PostgreSQL para almacenar valores y un cliente Redis para almacenar valores en proceso de cálculo. La configuración inicial del servidor establece los detalles de conexión en keys.js. El servidor tiene varios manejadores de ruta HTTP para diferentes solicitudes. En el caso de React, se utiliza React Router para mostrar dos páginas diferentes al usuario. La aplicación consiste en un componente funcional llamado App que renderiza el contenido. El componente tiene un estado que contiene tres variables y métodos para llamar a la API del servidor y calcular los valores de Fibonacci. Se sugiere que el código se mejore agregando pruebas unitarias y separando responsabilidades.


# Marco Teórico
# Worker y Redis
Este código crea un cliente Redis que se suscribe a un canal llamado "insert". Cuando se publica un mensaje en ese canal, se llama a la función "fib" con el valor del mensaje como argumento. La función "fib" calcula el número de Fibonacci para ese valor y lo guarda en Redis con la clave "message" y el valor del número de Fibonacci.
Algunos posibles casos de mejora para este código podrían incluir:
Manejo de errores: el código no maneja explícitamente los errores que pueden ocurrir al comunicarse con Redis. Podría ser beneficioso agregar algún tipo de manejo de errores para asegurarse de que el código se comporte correctamente en caso de una excepción.
Pruebas unitarias: sería beneficioso agregar pruebas unitarias para la función "fib" y para el manejo de mensajes del cliente Redis. Esto ayudaría a garantizar que el código se comporte correctamente en una variedad de situaciones y ayudaría a detectar errores temprano.
Separación de responsabilidades: el código actualmente mezcla la lógica de almacenamiento de Redis con la lógica de cálculo de números de Fibonacci. Sería beneficioso separar estas responsabilidades en diferentes módulos o funciones para mantener el código más organizado y modular.
Configuración centralizada: el código actualmente tiene la configuración de Redis como parte del código fuente. Sería mejor mover esta configuración a un archivo de configuración externo o una variable de entorno para que sea más fácil de cambiar sin necesidad de modificar el código fuente.
Mejora de rendimiento: si bien el código actual es funcional, no es muy eficiente. La función "fib" se llama de forma recursiva, lo que puede generar un gran número de llamadas para valores grandes de "index". También es posible que el código pueda beneficiarse de una mejor estrategia de almacenamiento en caché o de una mejor integración con la base de datos subyacente.
# Express, Redis y Postgre
La app tiene un servidor Node.js que utiliza Express para manejar solicitudes HTTP. Hay tres componentes principales: un cliente PostgreSQL para almacenar valores, un cliente Redis para almacenar valores que están siendo calculados, y una aplicación Express que maneja solicitudes HTTP y comunica el almacenamiento de datos entre el cliente PostgreSQL y el cliente Redis.
La configuración inicial del servidor crea instancias del cliente PostgreSQL y el cliente Redis y los configura con los detalles de conexión especificados en keys.js.
El código define varios manejadores de ruta HTTP para diferentes solicitudes. Por ejemplo, la ruta / simplemente envía una respuesta de Hi. La ruta /values/all obtiene todos los valores almacenados en la base de datos PostgreSQL y los devuelve como una respuesta HTTP. La ruta /values/current obtiene todos los valores actualmente en el almacenamiento Redis y los devuelve como una respuesta HTTP. La ruta /values acepta un índice enviado por un cliente, lo almacena en Redis con un valor temporal "Nothing yet!" y publica un mensaje para que un trabajador lo procese. Luego inserta el índice en la base de datos PostgreSQL y envía una respuesta HTTP de éxito.

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
# Nginx
Nginx es una configuración de un servidor en un ambiente Docker que se encarga de redirigir las solicitudes del cliente y del servidor a diferentes puertos en la máquina host.

La primera sección del código define los servidores del cliente y del API como 'upstreams', que son grupos de servidores que pueden ser referenciados en las reglas de proxy.

Luego, se define el servidor que escuchará en el puerto 80 y se configuran tres ubicaciones diferentes:

La ubicación raíz / redirige las solicitudes al servidor del cliente en el puerto 3000 utilizando la regla proxy_pass.
La ubicación /ws también redirige las solicitudes al servidor del cliente en el puerto 3000, pero incluye configuración adicional para soportar WebSockets.

La ubicación /api redirige las solicitudes al servidor del API en el puerto 5000 utilizando la regla proxy_pass. Además, utiliza la directiva rewrite para eliminar el prefijo /api de la URL antes de pasarla al servidor del API.

# Conclusión
El análisis presenta tres componentes diferentes: React, Redis y Postgre. Cada uno de ellos tiene ciertas características y funcionalidades que permiten crear una aplicación web que se conecta a una base de datos Redis y Postgre, utiliza una API Rest y un cliente web con React, y también utiliza Redis y un servicio Worker para simular cálculos complejos.

En general, el análisis sugiere varias mejoras para el código presentado en cada uno de los componentes. En el caso de Redis y el servicio Worker, se recomienda manejar errores, agregar pruebas unitarias, separar responsabilidades, centralizar la configuración y mejorar el rendimiento. En el caso de Postgre y Express, se sugiere mejorar la modularidad, agregar pruebas unitarias, mejorar el manejo de errores y mejorar el rendimiento. Finalmente, para React, se recomienda mejorar la modularidad, agregar pruebas unitarias y mejorar la eficiencia en la obtención de información de la secuencia de Fibonacci.

En general, se puede concluir que este análisis presenta una buena descripción de los componentes y sus funcionalidades, y proporciona sugerencias útiles para mejorar el código en cada uno de los componentes. Al seguir estas sugerencias, se podría mejorar significativamente la eficiencia, modularidad y manejo de errores en la aplicación.
