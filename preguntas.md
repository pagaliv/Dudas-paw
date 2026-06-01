# Ejercicios de examen

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

API REST para una aplicación y queremos hacer unos endpoints para usuarios acceder a la información de usuarios es publico. Cambiar los requiere login y no se pueden borrar.

Haz el controlador y razona las decisiones.

("api/usuarios")

```java
@RestController
class UsuarioController {
  @GetMapping("api/usuarios") // Obtener todos los usuarios
  ...
  @GetMapping("api/login/{id}") // Obtener un usuario en concreto
  ...
  @PostMapping("api/usuarios/{id}") // Crear nuevos usuarios
  ...
  @PutMapping("api/usuarios/{id}") // Crear nuevos usuarios
  ...
  @PatchMapping("api/usuarios/{id}") // Crear nuevos usuarios
  ...
}
```

El endpoint de creación:

```java
public UsuarioEntity create(UsuarioEntity nuevo) {
  if(session.getAttribute("user") == null) {
    throw new NotAuthorizedException("...");
  }
  UsuarioEntity nuevo = new UsuarioEntity();
  nuevo.nombre = req.getParameter("nombre");
  ...
  usuarioRepository.save(nuevo);
  resp.write(Gson.serialize(nuevo));
}
```

Hay que decir:

> El framework (spring) se encarga de leer de la request la entidad del usuario `UsuarioEntity`.

Otra opción sería poner en la implementación la creación de usuario entity

```java
public create(HttpRequest req, HttpResponse resp) {
  if(session.getAttribute("user") == null) {
    throw new NotAuthorizedException("...");
  }
  UsuarioEntity nuevo = new UsuarioEntity();
  nuevo.nombre = req.getParameter("nombre");
  ...
  usuarioRepository.save(nuevo);
  resp.write(Gson.serialize(nuevo));
}
```

## Ejercicio 3

¿Cómo navegarías este árbol con DOM hasta llegar a la segunda imagen y cambiar la imagen por `perro.png`?

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

Añadir una nueva tarea con título "Hacer el ejercicio" y `id` 2.

```javascript
const lista = document.getElementById("lista");
const element = document.createElement("li");
element.innerHTML = '<h1>Hacer el ejercicio</h1><input type="checkbox">';
element.dataset.id = 2 // element.setAttribute("data-id", 2);
lista.appendChild(element);
```

### Variación

Hacer que el título proventa del input entrada:

```javascript
const ent = document.getElementById("entrada");
<h1>${ent.value}</h1><input type="checkbox"''>
ent.value = ""
```

## Ejercicio 4

> ¿Por qué es importante tener un pool de conexiones?

Crear conexiones es algo costoso, así que tener ya conexiones creadas entre el servidor y la BD aumenta la velocidad de respuesta.
Además, por seguridad, no queremos que dos clientes tengan la misma conexión.

> ¿Cómo lo implementarías?

```java
class DBPool {
  private DBConnection[20];

  public DBConnection getConnection() {
    int i = 0;
    while (true) {
      if (!occupation[i]) {
        ocupation[i] = true;
        return array[i];
      }
      i = (i+1)%20;
    }
  }

  public void freeConnecion(DBConnection conn) {
    ...
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

Endpoints a implementar "/horarios"  y "/horarios?id={id}"

En Spring

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

Sin spring:

```java
public boolean doGet(req, resp) {
  String id = req.getParameter("id");
  List<Horario> hrs = horarioRepository.findAll();
  response.setAttribute("hrs", hrs);
  return "todos";
}
```
## Ejercicio 6
¿En que prioridad actua css?
De más importante a menos importante:
1. !important (es una etiqueta que se le puede poner a los css)
2. css inline, es decir css en el codigo de html
3. el css de #id, es decir el del propio elemento.
4. el css de .clase, es decir el de la clase a la que se le haya definido
5. el css de tipo, es decir su tipo, como por ejemplo <ul>
6. el css por defecto del motor de busqueda.
Qué puede preguntar:

- Uno o varios controladores
- Manipular html con javascript
- Teoría: todo
_ Un ejemplo de como implementar algo en Thymeleaf o un JSP.
- Filtro
- De teoria las diapositivas de arquitecturas que no hemos implementado como la hexagonal o la bola de barro no la va a preguntar.
- De css lo único que puede preguntar ha dicho que es la prioridad de comportamiento.
