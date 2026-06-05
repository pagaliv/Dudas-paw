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

2. **Según la prioridad de CSS, ¿qué regla tiene mayor jerarquía?**  
   a) `p { color: blue; }`  
   b) `.clase { color: green; }`  
   c) `#identificador { color: red; }`  
   d) `<p style="color: orange;">`

3. **¿Qué cabecera HTTP utiliza el navegador para devolver las cookies al servidor?**  
   a) `Set-Cookie`  
   b) `Cookie`  
   c) `Cache-Control`  
   d) `Set-Cookie2`

4. **En un pool de conexiones, ¿cuál es la principal ventaja de mantener un conjunto de conexiones abiertas?**  
   a) Evitar el uso de transacciones.  
   b) Reducir el coste de crear nuevas conexiones cada vez.  
   c) Aumentar el número máximo de usuarios simultáneos.  
   d) Mejorar la seguridad mediante encriptación.

5. **¿Qué atributo de una cookie impide que sea accesible desde JavaScript?**  
   a) `Secure`  
   b) `HttpOnly`  
   c) `SameSite`  
   d) `Domain`

6. **Dado el siguiente código JavaScript, ¿qué línea selecciona correctamente el segundo `<img>` del HTML y cambia su `src` a `"perro.png"`?**  
   ```html
   <div>
     <img src="hola.png">
   </div>
   <div class="container" id="mio">
     <img src="adios.png">
   </div>
   ´´´
a) document.querySelector("#mio img").src = "perro.png";
b) document.getElementById("mio").children[0].src = "perro.png";
c) document.getElementsByTagName("img")[1].src = "perro.png";
d) Todas las anteriores son correctas.

7. ¿Cuál de las siguientes afirmaciones sobre los filtros es FALSA?
a) Un filtro puede modificar la petición y la respuesta.
b) Un filtro está obligado a llamar a chain.doFilter() para que la petición continúe.
c) Es posible envolver la respuesta con HttpServletResponseWrapper para modificar su contenido.
d) La anotación @WebFilter permite declarar un filtro sin web.xml.

8. En el modelo arquitectónico Model 2 (MVC) para aplicaciones web, ¿qué componente recibe primero la petición?
a) El modelo (Model)
b) La vista (View)
c) El controlador (Controller)
d) La base de datos

9. ¿Qué método de HttpServletResponse se usa para añadir una cookie en Jakarta EE?
a) setCookie(Cookie c)
b) sendCookie(Cookie c)
c) addCookie(Cookie c)
d) putCookie(Cookie c)

10. Dado el siguiente fragmento de código Thymeleaf, ¿qué muestra en el HTML?

html
<p th:text="${usuario.nombre}">Nombre por defecto</p>
a) "Nombre por defecto" siempre.
b) El valor de la variable usuario.nombre si existe, o "Nombre por defecto" en caso contrario.
c) El texto literal ${usuario.nombre}.
d) Una excepción porque falta el atributo th:value.

---
## Parte 2 - Preguntas Cortas
**11. Explica la diferencia entre el Model 0 (Modelo basado en páginas) y el Model 2 (MVC). Nombra una ventaja del Model 2 sobre el Model 0.**

**12. ¿Por qué es importante usar un pool de conexiones en una aplicación web que accede a una base de datos? Describe brevemente cómo implementarías uno en Java (pseudocódigo válido).**

**13. En JavaScript, escribe una función que reciba un array de nombres y los muestre como una lista `<ul>` dentro de un elemento con id "contenedor". Si el array está vacío, debe mostrar un párrafo con el texto "No hay elementos".**

**14- Enumera, de mayor a menor prioridad, los tipos de selectores CSS que intervienen en la cascada (incluye !important, inline, id, clase, tipo y estilo por defecto del navegador).**

---


