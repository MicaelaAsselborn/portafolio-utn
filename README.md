# portafolio-utn

Proyecto personal para practicar.

Enfoque a intentar: Mobile first, Responsive

SE LOGRO:

- Menú hamburguesa despegable.
- Animación underline.
- Borde animado.

INFORMACIÓN:

"+" y "~" son selectores de hermanos. "+" selecciona al hermano inmediatamente adyacente y "~" selecciona o todos los hermanos del mismo tipo que se encuentren después del elemento señalado. Para usar selectores hermanos, el posicionamiento es importante.

FLIP CARD ITEM FLEX:
Para crear una carta flip que sea item flex, necesitamos 5 contenedores:

- El primer contenedor, deberá tener display: flex
- El el segundo contenedor, deberá tener position: relative. Este sera el item flex.
- Dentro, un hijo que será la CARTA, y deberá tener position: relative, transform-style: preserve-3D y las condiciones de transition.
- Dentro, 2 contenedores hermanos, que serán el frente y el dorso de la carta. Estos deben tener position: absolute.
- Por último, para crear la animación, crear un :hover de la carta y darle una transform: rotateY(180deg).

ANIMACIÓN UNDERLINE
Para crear una animación underline al hover, necesitamos crear 1 clase y 2 pseudo-clases:

- Primero creamos .underline (O el nombre que queramos) y le damos estas reglas:
  .underline{
  display: inline-block; <- Esto hace que el underline sea del tamaño de la palabra
  position: relative; <- Obligatorio
  }
- Luego creamos la pseudo-clase: .underline::after para dar forma y posicionar al underline:
  .underline::after{
  content:""; <- Obligatorio
  position: absolute; <- Obligatorio
  width: 100%; <- Esto hace que sea del mismo largo que la palabra
  height: 1px; <- Esto es a gusto
  bottom: 0; <- Esto y
  left: 0; <- Esto lo posicionan debajo de la palabra
  background-color: var(--lila);
  transform: scaleX(0); <- Esto lo esconde cuando no estamos haciendo hover
  transform-origin: bottom right; <- Esto controla desde donde se origina la linea
  transition: all 0.5s ease-in-out;
  }
- Y por último, se le vuelve dar el ancho al hover con transform: scaleX(1)

MENÚ HAMBURGUESA
Este es un poco más complejo, pero no imposible. Esta echo con enfoque "mobile first".

- Primero, en el HTML, en el NAV, vamos a necesitar:
- Un <input: checkbox> con un ID. Le damos la clase "menu-hamburguesa".
- Un <label for: ID>
- Como hijo de label, 2 iconos (Pueden ser SVG o iconos), uno de hamburguesa y uno de cruz. Le vamos a dar una clase a cada uno.
- Un <ul> con sus <li> dentro. A ul le daremos la clase "navbar"
- En el CSS, vamos a darle los siguientes estilos al <ul>:
  .navbar{
  background-color: black;
  width: 100%; <- Esto hace que ocupe toda la pantalla al desplegar
  position: absolute; <- Obligatorio
  top: var(--altura-header); <- Esto lo posiciona exactamente debajo del header
  left: 0; <- Y esto que comience a la izquierda
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-size: 4rem;
  height: 0; <- Esto lo esconde
  overflow: hidden;
  transition: all 0.4s ease;
  }
  .menu-hamburguesa, .icono-cerrar{
  display: none; <- Esconde el checkbox y el icono de cerrar
  }
  .menu-hamburguesa:checked ~ .navbar{
  height: calc(100% - var(--altura-header)); <- Esto que ocupe el 100% de la pantalla menos el header al hacer click
  }
  .menu-hamburguesa:checked + .icono-hamburguesa .icono-abrir{
  display: none; <- Esconde el icono de abrir cuando esta abierto
  }
  .menu-hamburguesa:checked + .icono-hamburguesa .icono-cerrar{
  display: inline; <- Muestra el icono de cerrar cuando esta desplegado.
  }
  - Por último, agregamos un media query para esconder el menu hamburguesa en pantallas más grandes:
    @media (min-width: 768px){
    .icono-hamburguesa{
    display: none; <- Esconde el icono cuando el tamaño de la pantalla es superior al de mobile.
    }
    .navbar{
    position: static; <- Devuelve al ul su posición normal
    width: auto;
    flex-direction: row;
    font-size: 2rem;
    height: var(--altura-header);
    background-color: var(--negro);
    }
    }

BORDE ANIMADO
