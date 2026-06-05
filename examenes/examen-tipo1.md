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
