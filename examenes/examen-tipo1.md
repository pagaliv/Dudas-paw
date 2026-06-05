# Examen completo de Programación de Aplicaciones Web (PAW)

## Instrucciones

- **Duración:** 2 horas 30 minutos.
- Lee atentamente cada pregunta.
- Para las preguntas de código, escribe la solución en el espacio indicado.
- Puedes usar pseudocódigo cuando se especifique, pero se valorará la sintaxis correcta en Java/JavaScript.

---

## Parte I: Preguntas tipo test (3 puntos)

1. **¿Cuál de las siguientes opciones describe correctamente el método `doFilter` de un filtro en Jakarta EE?**  
   a) `void doFilter(ServletRequest req, ServletResponse res)`  
   b) `void doFilter(ServletRequest req, ServletResponse res, FilterChain chain)`  
   c) `void doFilter(HttpServletRequest req, HttpServletResponse res)`  
   d) `void doFilter(FilterChain chain)`
   

3. **Según la prioridad de CSS, ¿qué regla tiene mayor jerarquía?**  
   a) `p { color: blue; }`  
   b) `.clase { color: green; }`  
   c) `#identificador { color: red; }`  
   d) `<p style="color: orange;">`

4. **¿Qué cabecera HTTP utiliza el navegador para devolver las cookies al servidor?**  
   a) `Set-Cookie`  
   b) `Cookie`  
   c) `Cache-Control`  
   d) `Set-Cookie2`

5. **En un pool de conexiones, ¿cuál es la principal ventaja de mantener un conjunto de conexiones abiertas?**  
   a) Evitar el uso de transacciones.  
   b) Reducir el coste de crear nuevas conexiones cada vez.  
   c) Aumentar el número máximo de usuarios simultáneos.  
   d) Mejorar la seguridad mediante encriptación.

6. **¿Qué atributo de una cookie impide que sea accesible desde JavaScript?**  
   a) `Secure`  
   b) `HttpOnly`  
   c) `SameSite`  
   d) `Domain`

7. **Dado el siguiente código JavaScript, ¿qué línea selecciona correctamente el segundo `<img>` del HTML y cambia su `src` a `"perro.png"`?**  
   ```html
   <div>
     <img src="hola.png">
   </div>
   <div class="container" id="mio">
     <img src="adios.png">
   </div>
   ```
   
   a) `document.querySelector("#mio img").src = "perro.png";`  
   b) `document.getElementById("mio").children[0].src = "perro.png";`   
   c) `document.getElementsByTagName("img")[1].src = "perro.png";`  
   d) `Todas las anteriores son correctas.`  

7. **¿Cuál de las siguientes afirmaciones sobre los filtros es FALSA?**
   a) `Un filtro puede modificar la petición y la respuesta.`  
   b) `Un filtro está obligado a llamar a chain.doFilter() para que la petición continúe.`  
   c) `Es posible envolver la respuesta con HttpServletResponseWrapper para modificar su contenido.`  
   d) `La anotación @WebFilter permite declarar un filtro sin web.xml.`  

8. En el modelo arquitectónico Model 2 (MVC) para aplicaciones web, ¿qué componente recibe primero la petición?
a) `El modelo (Model)`  
b) `La vista (View)`  
c) `El controlador (Controller)`  
d) `La base de datos`  

9. ¿Qué método de HttpServletResponse se usa para añadir una cookie en Jakarta EE?
a) `setCookie(Cookie c)`  
b) `sendCookie(Cookie c)`  
c) `addCookie(Cookie c)`  
d) `putCookie(Cookie c)`  

10. Dado el siguiente fragmento de código Thymeleaf, ¿qué muestra en el HTML?

```html
<p th:text="${usuario.nombre}">Nombre por defecto</p>
```
a) `Nombre por defecto siempre`  
b) `El valor de la variable usuario.nombre si existe, o "Nombre por defecto" en caso contrario.`  
c) `El texto literal ${usuario.nombre}.`  
d) `Una excepción porque falta el atributo th:value.`  

---
## Parte 2 - Preguntas Cortas
**11. Explica la diferencia entre el Model 0 (Modelo basado en páginas) y el Model 2 (MVC). Nombra una ventaja del Model 2 sobre el Model 0.**

**12. ¿Por qué es importante usar un pool de conexiones en una aplicación web que accede a una base de datos? Describe brevemente cómo implementarías uno en Java (pseudocódigo válido).**

**13. En JavaScript, escribe una función que reciba un array de nombres y los muestre como una lista `<ul>` dentro de un elemento con id "contenedor". Si el array está vacío, debe mostrar un párrafo con el texto "No hay elementos".**

**14- Enumera, de mayor a menor prioridad, los tipos de selectores CSS que intervienen en la cascada (incluye !important, inline, id, clase, tipo y estilo por defecto del navegador).**

---

## Parte III - Ejercicios de código
**Ejercicio A (1.5 puntos)** – Filtro de autenticación y roles
Diseña un filtro Jakarta EE que verifique:

- Que exista un atributo de sesión llamado "usuario".

- Que dicho atributo sea de tipo User y tenga un método getRol() que devuelva un String.

- Solo se permitirá el acceso si el rol es "ADMIN". En caso contrario, se redirige a una página "/acceso-denegado".

- Si no hay usuario logueado, redirige a "/login".

Escribe el código completo del filtro (incluye anotación @WebFilter para que se aplique a todas las rutas /*). Usa HttpServletRequest y HttpServletResponse.

**Ejercicio B (1.5 puntos) – Controlador REST en Spring**
Implementa un controlador REST llamado ProductoController que mapee en /api/productos con los siguientes endpoints:

- GET /api/productos → devuelve la lista de todos los productos (usando un ProductoRepository inyectado con @Autowired).

- GET /api/productos/{id} → devuelve un producto por su id. Si no existe, lanza una excepción con ResponseStatusException(HttpStatus.NOT_FOUND).

- POST /api/productos → crea un nuevo producto. Solo está permitido si en la sesión existe el atributo "user" (simula la comprobación). Si no existe, lanza HttpStatus.UNAUTHORIZED. El cuerpo de la petición es un objeto Producto (sin id). Devuelve el producto guardado con código 201.

Escribe las clases necesarias (solo el código del controlador y las anotaciones). No es necesario escribir el repositorio.

**Ejercicio C (2 puntos) – DOM y Fetch**
Dado el siguiente HTML:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Ejercicio Fetch</title>
</head>
<body>
    <h1>Lista de tareas desde JSONPlaceholder</h1>
    <button id="cargar">Cargar tareas del usuario 1</button>
    <ul id="listaTareas"></ul>
    <script src="script.js"></script>
</body>
</html>
```
---
## Parte IV: Ampliación (opcional, hasta 1 punto extra)
Explica cómo modificarías el filtro del Ejercicio A para que, además de comprobar el rol, registre en un log la URL solicitada y la hora de acceso, y luego permita continuar. Escribe solo el fragmento relevante dentro del método doFilter
