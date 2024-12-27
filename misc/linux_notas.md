## Referencia Rápida de Operadores y Atajos de Teclado en Linux

### Operadores de Linux

**¿Qué hacen los operadores de Linux?**
Permiten combinar y dirigir el flujo de comandos en tu terminal.

| Símbolo/Operador | Descripción |
|---|---|
| & | **Ejecución en segundo plano:** Envía un comando a ejecutarse en segundo plano, permitiendo continuar con otras tareas en el terminal. |
| && | **Ejecución condicional:** Ejecuta el siguiente comando solo si el anterior se completó exitosamente. |
| > | **Redirección de salida:** Redirige la salida estándar (generalmente, lo que se muestra en pantalla) de un comando a un archivo, sobreescribiéndolo. |
| >> | **Anexar a un archivo:** Redirige la salida estándar de un comando a un archivo, pero agrega la nueva información al final del archivo existente. |

**Ejemplo:**
```markdown
# Crear un archivo y escribir algo en él
echo "Hola, mundo!" > mi_archivo.txt

# Añadir una nueva línea al archivo
echo "Esta es una nueva línea." >> mi_archivo.txt



## Usage Examples

```text
# Background process with &
long-running-command &

# Command chaining with &&
cd /path/to/directory && ls -la

# Output redirection with >
echo "Hello" > file.txt

# Output appending with >>
echo "World" >> file.txt

```
# Atajos de Linux

## Tabla de Atajos de Teclado

| Atajo | Descripción |
|-------|-------------|
| Ctrl + A | Ir al principio de la línea |
| Ctrl + E | Ir al final de la línea |
| Ctrl + L | Limpiar pantalla (similar a clear) |
| Ctrl + U | Borrar línea anterior al cursor |
| Ctrl + H | Borrar carácter anterior (retroceso) |
| Ctrl + R | Buscar comandos anteriores |
| Ctrl + C | Interrumpir programa en ejecución |
| Ctrl + D | Cerrar shell actual |
| Ctrl + W | Cortar palabra anterior |
| Ctrl + K | Cortar línea siguiente |
| Ctrl + T | Intercambiar últimos dos caracteres |
| Esc + T | Intercambiar últimas dos palabras |
| Alt + . o !$ | Referenciar último argumento |
| Alt + F | Avanzar una palabra |
| Alt + B | Retroceder una palabra |
| Alt + l/u | Convertir a mayúsculas/minúsculas |
| Tab | Autocompletar archivos y carpetas |

