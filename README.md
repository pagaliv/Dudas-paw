 <div align="center">

<!-- Banner animado con nombre -->
<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:36013f,50:1a1a2e,100:16213e&height=140&section=header&text=EJERCICIOS%20PAW&fontSize=42&fontColor=58a6ff&fontAlignY=55&animation=fadeIn&desc=Computer%20Engineering%20%40%20Universidad%20de%20La%20Rioja&descColor=32174d&descSize=16&descAlignY=75"/>

[![Typing SVG](https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=500&size=16&duration=3500&pause=1000&color=58A6FF&center=true&vCenter=true&width=500&lines=Autores+Pablo+Galilea+y+Jacobo+Ruiz+%F0%9F%8E%93;Ejercicios+para+examen+final)](https://git.io/typing-svg)

</div>

---

## Ejercicio 1

Filtro de autentificación en JakartaEE/tomcat

```java
doFilter() {
  user = session.getAttribute("user");
  if (user == null) {
      redirect("login");
  }
  doChain(request,resp);
}
```

Responsabilidades:

- Si hay sesión iniciada
- redirigir al login
- Comprobar permisos de usuario
- Guardar acceso

## Ejercicio 2

API REST para una aplicación y queremos hacer unos endpoints para que los usuarios puedan puedan acceder a la información de usuarios. Los endpoints de aceso a los datos son públicos.
Cambiar los datos requiere _login_ y no se permite el borrado.

Haz el controlador y razona las decisiones.

("api/usuarios")

```java
@RestController
@RequestMapping("/api/usuarios")
class UsuarioController {
  @Autowired UserRepositry ur;
  @GetMapping // Obtener todos los usuarios
  ...
  @GetMapping("/{id}") // Obtener un usuario en concreto
  ...
  @PostMapping // Crear nuevos usuarios
  ...
  @PutMapping("/{id}") mod user
  ...
  @PatchMapping("{id}") // Crear nuevos usuarios
  ...
}
```

### Endpoints en Spring

#### Endpoint para ver todos los usuarios

```java
@GetMapping
public List<UsuarioEntity> getAll(){
 return ur.getAll();
}
```
#### Endpoint ver un usuario
```java
@GetMapping(/{id})
public UsuarioEntity getbyId(@PathVariable string id){
 return ur.getById(id).orElseThrow(new ExcepcionDeApp("no existe el elemento");)
//se puede hacer tambien con un if comproband si esta vacio.
}
```
#### Endpoint Creacion

```java
@PostMapping
public ResponseEntity<UsuarioEntity> create(@RequestBody UsuarioEntity nuevo, HttpSession session) {
  if(session.getAttribute("user") == null) {
    throw new NotAuthorizedException("...");
  }
  UsuarioEntity guardado = ur.save(nuevo);
  return ResponseEntity.status(HttpStatus.CREATED).body(guardado);
  //HttpStatus.CREATED es una constante de Spring que representa el número 201
}
```
#### Endpoint mod entero
```java
@PutMapping(/{id})
public UsuarioEntity update(@PathVariable id, RequestBody UsuarioEntity nuevosDatos, HttpSession s){
if(s.getAtrribute("user")==null){throw new ExcepcionDeApp("No existe user")}else{
 UsuarioEntity user = ur.getById(id)
 if(user==null){throw new ExcepcionDeApp("No existe user")}else{
   user.setNombre(nuevosDatos.getNombre());
   [así con todos los datos]
   return ur.save(user)
  }
 }
}
```
#### Endpoint modificar partial
```java
@PatchMapping(/{id}}
public UsuarioEntity updatepartial(@PathValue id, @RequestBody Map<String, Object> campos, HttpSession s){
  if(s.getAtribute("user")==null){
    throw new ExcepcionDeApp("user no encontrado");
  }
  UsuarioEntity user = ur.getyId(id)
  if(user==null){
   throw new ExceptiondeApp("usuario que se quiere editar no existe")
  }
  for(Map.Entry<String, Object> entry : campos.EntrySet()){
    String key = entry.getKey();
    Object value = entry.getValue();
    swich(key){
      case "nombre":
           user.setNombre((String) value);
           break;
      [asi con todos]
    }
  }
   return ur.save(user)
  
}
```
#### Eliminar (Se dice implicitamente que no debe estar, pero par tener un ejemplo de como se haría)
```java
@DeleteMapping("/{id}")
public ResponseEntity<Void> delete(@PathVariable Long id, HttpSession session) {
    // 1. Verificar login
    verificarLogin(session);
    
    // 2. Buscar el usuario de forma tradicional
    Optional<UsuarioEntity> optional = usuarioRepository.findById(id);
    if (!optional.isPresent()) {
        throw new ResponseStatusException(HttpStatus.NOT_FOUND, "Usuario no encontrado");
    }
    
    // 3. Eliminar (no necesitamos siquiera obtener el objeto, pero podemos hacerlo)
    // UsuarioEntity usuario = optional.get(); // si se necesitara para algo
    usuarioRepository.deleteById(id);
    
    // 4. Devolver 204 No Content (sin cuerpo)
    return ResponseEntity.noContent().build();
}
```
Hay que decir:

> El framework (Spring) se encarga de leer de la _request_ la entidad del usuario `UsuarioEntity`.

Otra opción sería poner en la implementación la creación de un nuevo `UsuarioEntity`:

```java
public create(HttpRequest req, HttpResponse resp) {
  if(session.getAttribute("user") == null) {
    throw new NotAuthorizedException("...");
  }
  UsuarioEntity nuevo = new UsuarioEntity();
  nuevo.nombre = req.getParameter("nombre");
  ...
  usuarioRepository.save(nuevo);
  resp.getWriter().write(gson.toJson(nuevo));
}
```

## Ejercicio 3

¿Cómo navegarías este árbol con DOM hasta llegar a la segunda etiqueta `<img>` y cambiar la imagen por `perro.png`?

```html
<html>
    <head></head>
    <body>
      <div>
        <img src="hola.png">
      </div>
      <div class="container" id="mio">
        <img src="adios.png"> 
      </div>
    </body>
</html>
```

Respuesta:

```javascript
const div = document.getElementbyId("mio");
div.childNodes()[1]; // Opcion 1
for (let e of div.childNodes) { // Opcion 2
  if(e.type == "Element"){
    ...
  }
}
div.children()[0] // Opcion 3
document.querySelector("#mio img");


// Finalmente
imagen.src = "perro.png";
```

## Ejercicio 4

Tenemos este HTML

```html
<ul id="lista">
    <li data-id="1">
      <h1>Mi titulo</h1>
      <input type="checkbox">
    </li>
</ul>
```

Añadir usando JavaScript una nueva tarea con título "Hacer el ejercicio" y `id` 2.

```javascript
const lista = document.getElementById("lista");
const element = document.createElement("li");
element.innerHTML = '<h1>Hacer el ejercicio</h1><input type="checkbox">';
element.dataset.id = 2 // element.setAttribute("data-id", 2);
lista.appendChild(element);
```

### Variación

Hacer que el título provenga del `input` con identificador `entrada`:

```javascript
const ent = document.getElementById("entrada");
<h1>${ent.value}</h1><input type="checkbox"''>
ent.value = ""
```

## Ejercicio 4

Enunciado:
> ¿Por qué es importante tener un pool de conexiones?

Respuesta:

Crear conexiones es algo costoso, así que tener ya conexiones creadas entre el servidor y la BD aumenta la velocidad de respuesta.
Además, por seguridad, no queremos que dos clientes tengan la misma conexión.

Enunciado:
> ¿Cómo lo implementarías?

Respuesta:

```java
class DBPool {
  private Connection DBConnection[20];
  private boolean ocupation[20];
  public DBPool (){
    for(int i=0; i<20 ; i++){
      DBConnection[i]=DriverManager.getConnection(url,user,pwd);
      ocupation[i]=false;
    }
  }
  public DBConnection getConnection() {
    int i = 0;
    while (true) {
      if (!occupation[i]) {
        ocupation[i] = true;
        return DBConnection[i];
      }
      i = (i+1)%20;
    }
    try{wait()}catch(Exception e){ e.printStacktrace();}
    //no se debe encapsular en exception pero es un ejemplo generalista y ""pseudocodigo""
  }

  public void freeConnecion(DBConnection con) {
    for(int i=0; i < 20; i++){
      if(DBConnection[i] == con){
        ocupation[i] == false;
        notifyAll(); //para avisar a quienes esten esperando para usar una conexión
        break
      }
    }
  }
}
```

## Ejercicio 5

Controlador para mostrar horarios

```java
class Horarios {
  public List<Horas> horas;

  class Hora {
    public int inicio;
    public int final;
    public String asignatura;
  }
}
```

Endpoints a implementar: "/horarios"  y "/horarios?id={id}"

Implementación en Spring:

```java
@Controller
class Controlador {
  @AutoWired
  private HorarioRepository horarioRepo;

  @GetMapping("/horarios")
  public String getHorarios(@RequestParam("id") String id, Model model) {
    if (id == null || id.isBlank()) {
      List<Horario> horario = horarioRepo.findAll();
      model.addAttribute("horarios", horario);
      return "horarios";
    } else {
      Optional<Horario> horarioOptional = horarioRepo.findById(id);
      if (!horarioOptional.isPresent()) {
        throw new NoSuchElementException("No existe el elemento con id " + id);
      }
      
      model.addAttribute("horario", horarioOptional.get());
      return "uno";
    }
  }
}
```

Implementación en JakartaEE:

```java
public String doGet(req, resp) {
  String id = req.getParameter("id");
  if( id == null ) {//no hay id, se mandan todos los horarios
     List<Horario> hrs = horarioRepository.findAll();
     response.setAttribute("hrs", hrs);
     return "todos";
  }else{ //si hay id
    Horario hr = horarioRepoitory.finbyId(id);
    response.setAttribute("hr", hr);
    return "horarioInfo" //el nombre que quieras realmente
  }
}
```

## Ejercicio 6

¿En que prioridad actúa CSS?
De más importante a menos importante:

1. `!important` (es una etiqueta que se le puede poner a los CSS).
2. CSS inline, es decir CSS en el código de HTML.
3. El CSS de `#id`, es decir el del propio elemento.
4. El CSS de `.clase`, es decir el de la clase a la que se le haya definido.
5. El CSS de tipo, es decir su tipo, como por ejemplo `<ul>`.
6. El CSS por defecto del motor de búsqueda.

# Ejercicios Extra
## Ejercicio diapositivas DOM
Dado el siguiente html:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>lista</h1>
    <ul id="Lista">
        <li>Nombre aquí</li>
    </ul>
    <button disabled onclick="alert('Botón 1')">Botón 1</button>
    <button onclick="alert('Botón 2')">Botón 2</button>
    <button disabled onclick="alert('Botón 3')">Botón 3</button>
    <button disabled onclick="alert('Botón 4')">Botón 4</button>
    <script>
        // Aquí irá tu código JavaScript
    </script>
</body>
</html>
```

1. Cambia el contenido del elemento `<h1>` a **“Lista de nombres”**.
2. Crea un array de nombres de personas (por ejemplo, `["Ana", "Juan", "María", "Pedro"]`).
3. Elimina del `<ul id="Lista">` el único elemento `<li>` que contiene (el que dice "Nombre aquí").
4. Configura la lista (`<ul>`) para que contenga un elemento `<li>` por cada nombre del array definido anteriormente.
5. Habilita todos los botones que estén deshabilitados (cambia su propiedad `disabled` a `false`).

```javascript
 let nombreLista = document.getElementsbyTagName("h1")[0];
 nombreLista.innerText = "Lista de nombres";
 const nombres = ["Ana", "Juan", "María", "Pedro"];
 let lista = document.getElementbyId("lista");
 let elementoLista = lista.getElementsByTagName("li")[0];
 lista.removeChild(elementoLista);
 for(let i = 0; 0 < nombre.legth ; i ++){
   let elemento = document.createElement("li");
   elemento.innerText = nombre[i];
   lista.appendChild(elemento);
 }
for ( let i = 0; i < 4 ; i++){
  document.getElementsByTagName("button")[i].disabled=false;
}
```

## Ejercicio extra DOM
Dado el siguiente html:
```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Ejercicio DOM - Lista de tareas</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 2rem; }
        .completada { text-decoration: line-through; color: gray; }
        button { margin: 0.2rem; }
    </style>
</head>
<body>
    <h2>Mis tareas</h2>
    <ul id="listaTareas">
        <li>Tarea de ejemplo</li>
    </ul>
    <button id="btnAgregar" disabled>Agregar nueva tarea</button>
    <button id="btnMarcar">Marcar primera como completada</button>
    <button id="btnEliminar" disabled>Eliminar última tarea</button>
    <button id="btnReset">Reiniciar lista</button>

    <script>
        // Aquí irá tu código JavaScript
    </script>
</body>
</html>
```

1. **Cambiar el título** del `<h2>` a **“Lista de tareas pendientes”**.
2. **Crear un array** con al menos 3 tareas iniciales (por ejemplo, `["Estudiar JavaScript", "Hacer ejercicio", "Leer un libro"]`).
3. **Vaciar la lista** `<ul id="listaTareas">` eliminando el `<li>` de ejemplo que contiene (“Tarea de ejemplo”).
4. **Rellenar la lista** añadiendo un `<li>` por cada tarea del array creado en el paso 2.
5. **Habilitar** el botón con `id="btnAgregar"` y el botón con `id="btnEliminar"` (cambiar `disabled` a `false`).
6. **Añadir funcionalidad** (escribe el código que responda a los clics):
   - Al hacer clic en **“Agregar nueva tarea”**, se debe mostrar un `prompt()` pidiendo una nueva tarea y, si el usuario escribe algo, añadir esa tarea como un nuevo `<li>` al final de la lista.
   - Al hacer clic en **“Marcar primera como completada”**, se debe añadir la clase CSS `"completada"` al primer `<li>` de la lista (si existe). Si ya tiene la clase, no pasa nada.
   - Al hacer clic en **“Eliminar última tarea”**, se debe eliminar el último `<li>` de la lista (si hay al menos uno).
   - Al hacer clic en **“Reiniciar lista”**, se debe restaurar la lista a exactamente el mismo estado que dejaste en los pasos 3 y 4 (es decir, vaciar y volver a poner las tareas del array original, sin tareas adicionales que se hayan agregado después).
  

```javascript
let hdos = document.getElementsByTagName("h2")[0]
hdos.innerText = "Lista de tareas pendientes"
const tarea = ["peo", "caca", "pis" ]
let  lista = document.getElementById("listaTareas")
let elementoListaToMatar = lista.getElementsByTagName("li")[0]
lista.removeChild(elementoListaToMatar)
for(int i; i<tarea.lenght; i++){
 let elementoNuevo = document.newElement("li")
 elementoNuevo.innerText = tarea[i]
 lista.appendChild(elementoNuevo)
}
let btnagr = document.getElementById("btnAgregar")
let btneli = document.getElementById("btnEliminar")
btnagr.disabled =false
btneli.desabled= false 
btnagr.addEventListener("click", addTarea())

addTarea(){
  const tarea = promt("introduce tarea")
  if(tarea && tarea.trim()!=""){
    let nuevoelemento = document.newElement("li")
    li.innerText = tarea;
    lista.appendChild(nuevoelemento)
  }
}
// el resto de cosas es hacer todo el rato lo mismo 

```

## Test sobre Cookies 

Responde las siguientes preguntas según la información del material "Cookies.pdf".

1. **¿Qué son las cookies según la introducción del material?**  
   a) Programas ejecutables que pueden ser virus.  
   b) Datos binarios almacenados en el servidor.  
   c) Datos de texto definidos por el servidor y enviados al navegador.  
   d) Cabeceras HTTP obligatorias en toda petición.

2. **¿Qué ocurre con una cookie que no tiene los atributos `Expires` ni `Max-Age`?**  
   a) Se convierte en una cookie persistente.  
   b) Se elimina inmediatamente después de ser recibida.  
   c) Se elimina cuando el navegador se cierra (cookie de sesión).  
   d) Se almacena indefinidamente en el cliente.

3. **¿Cuál es el tamaño máximo aproximado por cookie según el material?**  
   a) 1 KB  
   b) 4 KB  
   c) 8 KB  
   d) 16 KB

4. **¿Qué atributo de una cookie impide que sea accesible desde JavaScript en el navegador?**  
   a) `Secure`  
   b) `HttpOnly`  
   c) `Domain`  
   d) `Path`

5. **¿Qué cabecera HTTP utiliza el navegador para devolver las cookies al servidor?**  
   a) `Set-Cookie`  
   b) `Cookie`  
   c) `Cache-Control`  
   d) `Set-Cookie2`

6. **Las cookies de terceros (third-party cookies) se caracterizan por:**  
   a) Tener el mismo dominio que la página que las establece.  
   b) Ser establecidas únicamente por el servidor principal.  
   c) Tener un dominio diferente al de la página a través de la cual se reciben.  
   d) No poder ser leídas nunca por el servidor.

7. **Según la Guía de la AEPD actualizada a enero de 2024, el usuario debe poder:**  
   a) Retirar el consentimiento en cualquier momento.  
   b) Impedir siempre el acceso al sitio web si no acepta cookies.  
   c) No tener alternativa al servicio si rechaza las cookies.  
   d) Recibir cookies sin información previa.

8. **¿Qué método de `HttpServletResponse` se usa para enviar una cookie al navegador en JakartaEE?**  
   a) `setCookie(Cookie)`  
   b) `sendCookie(Cookie)`  
   c) `addCookie(Cookie)`  
   d) `putCookie(Cookie)`

9. **Si una cookie tiene el atributo `Max-Age=0`, ¿qué significa?**  
   a) La cookie es de sesión.  
   b) La cookie se elimina inmediatamente.  
   c) La cookie nunca expira.  
   d) La cookie dura 0 segundos después de cerrar el navegador.

10. **En Expression Language (EL) de JSP, ¿cómo se accede al valor de una cookie llamada “miCookie”?**  
    a) `${cookie.miCookie}`  
    b) `${cookies.miCookie.value}`  
    c) `${cookie.miCookie.value}`  
    d) `${request.cookie['miCookie']}`

---

## Respuestas correctas

1. c  
2. c  
3. b  
4. b  
5. b  
6. c  
7. a  
8. c  
9. b  
10. c

# Qué puede preguntar
- Uno o varios controladores.
- Manipular HTML con JavaScript.
- Teoría: todo.
- Un ejemplo de como implementar algo en Thymeleaf o un JSP.
- Filtro.
- De teoría las diapositivas de arquitecturas que no hemos implementado como la hexagonal o la bola de barro no la va a preguntar.
- De CSS lo único que puede preguntar ha dicho que es la prioridad de comportamiento.
- Diferencias entre Model 0,1,2.
- Hacer el pool de conexiones e implementar uno o varios de sus métodos.

## Preguntas de otros años con respuestas 


- En una petición GET ¿qué cabeceras usamos para?  
  - Determinar la codificación de caracteres  
  - Saber qué tipo de cliente usa el usuario  
  - Especificar un idioma  

- Enviar una cookie de nombre `skin` cuyo valor sea `clásico` y que dure hasta dentro de dos años  

- Especificar el dominio  

- Función de JavaScript para evitar el comportamiento por defecto de eventos  

- Dominio de una Cookie  

- ¿Qué es el locale?  

- ¿Qué es el bundle?  

- Tipos falsy  

- ¿Qué necesita un formulario para soportar el envío de ficheros?
