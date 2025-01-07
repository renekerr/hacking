# Principios Fundamentales en Seguridad

## Principios Generales

Los **principios de seguridad** son fundamentos esenciales para proteger la confidencialidad, integridad y disponibilidad (CIA) de la información y sistemas. Estos principios guían el diseño, implementación y gestión de controles para mitigar riesgos.

## CIA

El triángulo CIA representa:
- **Confidencialidad**: Evita la divulgación no autorizada.
- **Integridad**: Garantiza que los datos no sean alterados sin autorización.
- **Disponibilidad**: Asegura acceso a datos cuando sea necesario.

## DAD

El triángulo opuesto CIA es DAD:
- **Divulgación**: Ataque contra confidencialidad.
- **Alteración**: Ataque contra integridad.
- **Destrucción/Denegación**: Ataque contra disponibilidad.

## Modelos Fundamentales

Los modelos son marcos teóricos que ayudan a aplicar principios en sistemas informáticos:

### Modelo Bell-LaPadula
Enfocado en confidencialidad:
1. "No leer hacia arriba".
2. "No escribir hacia abajo".
3. Uso discrecional mediante matriz.

### Modelo Biba
Enfocado en integridad:
1. "No leer hacia abajo".
2. "No escribir hacia arriba".

### Modelo Clark-Wilson
Asegura integridad mediante elementos restringidos (CDI) y procedimientos programados (TP).

### Otros Modelos
Incluyen Brewer-Nash, Goguen-Meseguer, Sutherland, Graham-Denning, Harrison-Ruzzo-Ullman.

---

## ISO/IEC 19249

La norma ISO/IEC 19249 describe principios arquitectónicos para productos seguros:

1. Separación de Dominios
2. Capas
3. Encapsulación
4. Redundancia
5. Virtualización

Principios adicionales incluyen Privilegio Mínimo, Minimización Superficie Ataque, Validación Centralizada, Servicios Centralizados, Preparación Manejo Errores.

---

## Defensa en Profundidad

La Defensa en Profundidad implica múltiples niveles para asegurar un sistema.

## Confianza Cero

El principio considera que la confianza es una vulnerabilidad; se requiere autenticación antes del acceso a recursos.

## Confía pero Verifica

Siempre se debe verificar incluso cuando se confía; esto implica revisar registros adecuados.

---

## Amenazas y Riesgos

Conceptos clave:
- **Vulnerabilidad**: Debilidad que puede ser explotada.
- **Amenaza**: Potencial peligro que explota vulnerabilidades.
- **Riesgo**: Probabilidad e impacto del daño causado por amenazas.
