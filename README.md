# CURSO: APRENDE BLAZOR

# LECCIÓN 35: Interoperatibilidad con JavaScript (InvokeVoidAsync)

1. Abrir la aplicación con Visual Studio 2022 o VSCode

2. Creamos el archivo (example.js) donde definimos nuestra función de JavaScript a invocar desde C#. Localizamos el archivo dentro de una carpeta localizada en wwwroot

```javascript
function showAlert(message) {
    alert(message);
}
```

3. Creamos el nuevo componente para invocar desde C# la función showAlert() de JavaScript

```razor
@page "/NuevoComponente"
@inject IJSRuntime JSRuntime

<h3>JS Interop Example</h3>

<button @onclick="CallJSFunction">Show Alert</button>

@code {
    private async Task CallJSFunction()
    {
        // Call the JavaScript function 'showAlert' and pass a message
        await JSRuntime.InvokeVoidAsync("showAlert", "Hello from Blazor!");
    }
}
```

4. Incluimos en el componente App.razor la localización de nuestro archivo example.js

```razor
<body>
    <Routes @rendermode="InteractiveServer" />
    <script src="_framework/blazor.web.js"></script>
    <script src="js/example.js"></script>
</body>
```

5. Creamos un nuevo NavLink en el componente NavMenu.razor para navegar hacia nuestro nuevo componente

```razor
 <div class="nav-item px-3">
     <NavLink class="nav-link" href="NuevoComponente">
         <span class="bi bi-list-nested-nav-menu" aria-hidden="true"></span> Nuevo Componente
     </NavLink>
 </div>
'''

6. Ejecutamos la aplicación
