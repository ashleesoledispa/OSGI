🧩 OSGi Demo — Clock Provider & Greeter Consumer

ISWZ2202 – Diseño y Arquitectura de Software
Facultad de Ingeniería y Ciencias Aplicadas

📌 Descripción del Proyecto

Este proyecto es una demostración práctica del uso de OSGi y Apache Karaf para construir aplicaciones modulares, desacopladas y dinámicas.

La aplicación está compuesta por dos bundles:

clock-provider

Proporciona un servicio OSGi llamado ClockService

Devuelve la hora actual del sistema

greeter-consumer

Consume el ClockService mediante OSGi Declarative Services

Expone un comando en la consola de Karaf:

greeter:say <nombre>


Cuando se ejecuta el comando, el bundle imprime un saludo junto con la hora obtenida dinámicamente del proveedor.

🏛️ Arquitectura

Este proyecto implementa dos patrones de arquitectura:

✔ Microkernel Architecture

El framework OSGi funciona como un microkernel donde los bundles actúan como plugins dinámicos.

✔ Service-Oriented Architecture (SOA)

Los módulos se comunican mediante servicios registrados y descubiertos en el Service Registry de OSGi.

📂 Estructura del Proyecto
osgi-demo/
│   pom.xml                      → POM principal (módulo padre)
│
├── clock-provider/             → Bundle proveedor de hora
│      ├── src/main/java/com/example/clock/
│      │       ClockService.java
│      │       impl/ClockServiceImpl.java
│      └── pom.xml
│
└── greeter-consumer/           → Bundle consumidor
       ├── src/main/java/com/example/greeter/
       │       GreeterCommand.java
       └── pom.xml

📦 Requisitos Previos

Asegúrate de tener instalado:

Java 8

Apache Karaf 4.4.x (probado en 4.4.8)

Maven 3.x

Puedes verificar:

java -version
mvn -version

🛠️ 1. Compilar el proyecto

En la raíz del proyecto:

mvn clean install


Esto generará los bundles en:

clock-provider/target/*.jar
greeter-consumer/target/*.jar


También quedarán instalables vía Maven en:

mvn:com.example/clock-provider/1.0.0
mvn:com.example/greeter-consumer/1.0.0

🚀 2. Ejecutar Apache Karaf

Abre Karaf:

En Windows:

bin\karaf.bat


Al cargar verás:

karaf@root()>

⚙️ 3. Activar Declarative Services

Necesario para que las anotaciones @Component y @Reference funcionen:

feature:install scr


Puedes verificar:

bundle:list | grep -i scr


Debe aparecer como Active.

📥 4. Instalar los Bundles
Instalar el proveedor de hora:
bundle:install -s mvn:com.example/clock-provider/1.0.0

Instalar el consumidor:
bundle:install -s mvn:com.example/greeter-consumer/1.0.0


Si todo está correcto, ejecutar:

bundle:list | grep -i example


Debe mostrar ambos bundles como Active.

🎉 5. Ejecutar la aplicación

Usa el comando expuesto por el bundle consumidor:

greeter:say Ashlee

Ejemplo de salida:
Hola Ashlee, son las 21:14


El resultado confirma:

✔ El greeter-consumer está funcionando
✔ El servicio ClockService está activo
✔ Karaf resolvió correctamente la dependencia OSGi

🧪 6. Reiniciar/Actualizar bundles
Detener un bundle
bundle:stop <ID>

Iniciar un bundle
bundle:start <ID>

Actualizar un bundle ya instalado
bundle:update <ID>


Los bundles pueden modificarse y recargarse sin reiniciar Karaf.
Esto demuestra el poder de OSGi como arquitectura modular dinámica.

🩺 7. Troubleshooting
❌ Error: osgi.extender (component) missing

Solución:

feature:install scr

❌ Bundles aparecen como Installed pero no Active

Solución:

log:tail


Buscar qué servicio no puede resolverse.

❌ No encuentra el comando greeter:say

Verifica que el bundle esté activo:

bundle:list | grep greeter

📚 8. Conclusiones

OSGi permite crear aplicaciones altamente modulares basadas en servicios.

Apache Karaf simplifica la instalación, monitoreo y actualización dinámica de bundles.

La implementación demuestra desacoplamiento total mediante inversión de dependencias y servicios OSGi.

El proyecto cumple los objetivos de reforzar patrones de arquitectura y prácticas de diseño modular.

📎 Autora

Ashlee Soledispa
Facultad de Ingeniería y Ciencias Aplicadas – UDLA
Ingeniería de Software
