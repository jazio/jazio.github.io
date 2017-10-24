#Elm

A fully functional language.

Unlike Javascript is strongly typed (immutable data), requires less testing, is a unified language.

It compiles to Javascript.

No runtime errors.

Inspired by Haskell.

Indentation is strict as in Python.

Suitable for reactive programming.



##Union types

A natural way to shape data.

```
type Shape
    = Circle Float
    | Square Float
    -- Polygons have Int sides and Float length
    | Poly Int Float
```

Now we write the function to render

```
render : Shape -> String
render shape =
    case shape of
        Circle radius ->
          "circle"
         Square length ->
          "a square"
         Poly sides length
          "A poly"
```

First is declared the function render having its signature: It inputs a shape type (which is a custom type) and outputs a string.
There is no way to cheat it, it will always output a string. The compiler will penalize.

Create a module

```
module myFileLoader exposing (load)

load : String -> String
load filename =
...
```

We use it via ```import```

import myFileLoader as L

process = L.load "data.csv"
```

If you want to directly access the function ```load```

```
import MyFileLoader exposing (load)

process = load "data.csv"
```


Elm Architecture


init
You get started by writing a function called init. Its job is to generate the application initial Model.

Model
Model is not a single entity in database (as it is used in other contexts: MVC, Ruby etc) but a complete model of the current state of UI.
You write then the View which take the Model and renders it in Html.

View
Everytime there is a change it rerenders a complete change of a user interface into a Virtual DOM which
later compares to the actual DOM and only reproduce the changes were made. Similar to React.

It listen to the events and whenever this event occurs it sends the program a message Msg

You write a function called Update that receive those messages.
Then regenerate an updated Model. Which later renders a renewed DOM.

