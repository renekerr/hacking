# Principios de Seguridad

## Principios de Seguridad

Los **principios de seguridad** son fundamentos esenciales para proteger la confidencialidad, integridad y disponibilidad de la información y sistemas. Estos principios guían el diseño, implementación y gestión de controles de seguridad para mitigar riesgos y amenazas, asegurar la continuidad del negocio y proteger contra accesos no autorizados y ciberataques.

## CIA

El triángulo de la seguridad está representado por los principios de **Confidencialidad, Integridad y Disponibilidad (CIA)**. El objetivo de un sistema de seguridad es asegurar una o más de estas funciones:
- **Confidencialidad**: Evita la divulgación no autorizada de información.
- **Integridad**: Garantiza que los datos no sean alterados de manera no autorizada.
- **Disponibilidad**: Asegura que los datos y sistemas estén disponibles para su uso cuando sea necesario.

## DAD

El opuesto del triángulo CIA es el triángulo **DAD**: **Divulgación, Alteración y Destrucción/Denegación**. Cada una de estas acciones representa una violación a los principios de seguridad:
- **Divulgación**: Ataque contra la confidencialidad.
- **Alteración**: Ataque contra la integridad.
- **Destrucción/Denegación**: Ataque contra la disponibilidad.

## Conceptos Fundamentales de Modelos de Seguridad

Los modelos de seguridad son marcos teóricos que proporcionan una estructura para entender y aplicar principios de seguridad en sistemas informáticos. Estos modelos ayudan a definir y controlar cómo se gestionan los accesos y las operaciones dentro de un sistema.

### Modelo Bell-LaPadula
Se enfoca en la confidencialidad mediante las siguientes reglas:
- **Propiedad de Seguridad Simple**: "No leer hacia arriba"; un sujeto en un nivel inferior no puede leer un objeto en un nivel superior.
- **Propiedad de Seguridad Estrella**: "No escribir hacia abajo"; un sujeto en un nivel superior no puede escribir en un objeto en un nivel inferior.
- **Propiedad de Seguridad Discrecional**: Uso de una matriz de acceso para permitir operaciones de lectura y escritura.

### Modelo Biba
Se enfoca en la integridad mediante las siguientes reglas:
- **Propiedad de Integridad Simple**: "No leer hacia abajo"; un sujeto de mayor integridad no debe leer un objeto de menor integridad.
- **Propiedad de Integridad Estrella**: "No escribir hacia arriba"; un sujeto de menor integridad no debe escribir en un objeto de mayor integridad.

### Modelo Clark-Wilson
Busca asegurar la integridad mediante:
- **Elementos de Datos Restringidos (CDI)**: Datos cuya integridad se debe preservar.
- **Elementos de Datos No Restringidos (UDI)**: Otros tipos de datos como entradas de usuario.
- **Procedimientos de Transformación (TP)**: Operaciones programadas que mantienen la integridad de los CDIs.
- **Procedimientos de Verificación de Integridad (IVP)**: Verifican la validez de los CDIs.

### Otros Modelos de Seguridad
- **Modelo Brewer y Nash**: También conocido como el Modelo de la Muralla China, este modelo se centra en la prevención de conflictos de interés dentro de una empresa.
- **Modelo Goguen-Meseguer**: Basado en la teoría de sistemas y enfocado en la seguridad de la información mediante la separación de dominios.
- **Modelo Sutherland**: Se centra en la integridad de la información, basado en la teoría de la seguridad de la información y los flujos de información.
- **Modelo Graham-Denning**: Describe un conjunto de comandos para definir cómo los sujetos y objetos pueden ser creados o manipulados dentro de un sistema.
- **Modelo Harrison-Ruzzo-Ullman**: Extiende el modelo Graham-Denning añadiendo mecanismos para definir y controlar las autorizaciones en un sistema informático.

## ISO/IEC 19249

La norma **ISO/IEC 19249:2017** describe principios arquitectónicos y de diseño para productos, sistemas y aplicaciones seguros. Los cinco principios arquitectónicos son:
1. **Separación de Dominios**: Agrupar componentes relacionados en una única entidad con atributos de seguridad comunes.
2. **Capas**: Estructurar el sistema en múltiples niveles o capas para imponer políticas de seguridad y validar operaciones.
3. **Encapsulación**: Ocultar implementaciones de bajo nivel y prevenir la manipulación directa de datos.
4. **Redundancia**: Asegurar disponibilidad e integridad mediante sistemas redundantes.
5. **Virtualización**: Compartir hardware entre múltiples sistemas operativos, mejorando la seguridad mediante aislamiento.

Los cinco principios de diseño son:
1. **Privilegio Mínimo**: Proveer la menor cantidad de permisos necesarios para realizar una tarea.
2. **Minimización de la Superficie de Ataque**: Reducir las vulnerabilidades deshabilitando servicios no necesarios.
3. **Validación Centralizada de Parámetros**: Validar entradas a través de una biblioteca o sistema centralizado.
4. **Servicios de Seguridad Centralizados**: Centralizar servicios de seguridad como la autenticación.
5. **Preparación para el Manejo de Errores y Excepciones**: Diseñar sistemas que fallen de manera segura y no filtren información confidencial.

## Defensa en Profundidad

La **Defensa en Profundidad** implica crear un sistema de seguridad con múltiples niveles, también conocido como Seguridad de Niveles Múltiples. Ejemplo: asegurar un objeto valioso no solo con una cerradura, sino también con puertas y cámaras adicionales para dificultar el acceso no autorizado.

## Confianza Cero

El principio de **Confianza Cero** considera que la confianza es una vulnerabilidad y trata de eliminarla. No se confía en ningún dispositivo basado en su ubicación o propiedad; se requiere autenticación y autorización antes de acceder a cualquier recurso. Microsegmentación es una implementación de este principio.

## Confía pero Verifica

El principio de **Confía pero Verifica** sugiere que siempre se debe verificar, incluso cuando se confía en una entidad. Esto implica configurar mecanismos de registro adecuados y revisar estos registros para asegurarse de que todo esté funcionando como debería.

## Amenazas y Riesgos

En el contexto de la seguridad de la información, es crucial comprender los conceptos de amenazas y riesgos para gestionar adecuadamente la protección de los sistemas.

- **Vulnerabilidad**: Una debilidad en el sistema que puede ser explotada para causar daño o acceder de manera no autorizada.
- **Amenaza**: Un potencial peligro que podría explotar una vulnerabilidad. Las amenazas pueden ser internas o externas, intencionales o accidentales.
- **Riesgo**: La probabilidad de que una amenaza explote una vulnerabilidad y el impacto consecuente en el negocio. La gestión de riesgos implica evaluar estas probabilidades e impactos para tomar decisiones informadas sobre cómo mitigarlos.

---
