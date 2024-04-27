![ASS Banner](https://cdn.discordapp.com/attachments/1233393558828879902/1233393559160356945/ass.banner.png?ex=662d9783&is=662c4603&hm=266e0b8907f9e04845de755ff3de0ee0652727a18f88fa14ea19c088fefc8371)

# Advanced Style Sheet

Style Sheet with advanced functions for your web usage.

**Advanced StyleSheet (ASS)** est une librairie de gestion de feuille de style (CSS) avec des fonctionnalités inédites afin de facilité la stylisation de vos composants WEB.

- Elle dispose de fonctionnalités tel que `component` permettant de créer des bloques de code CSS réutilisable dans chacun de vos composants avec la possibilité d'entrer des paramètres pour custom des valeurs qui peuvent être typé.

| Type      | Description                                           |
| --------- | ----------------------------------------------------- |
| color     | Permet d'entrer une couleur sous différents format    |
| number    | Permet d'entrer une nombre                            |
| unit      | Permet d'entrer une unité de mesure (px, %, vw...)    |

- Un système de déclaration de variable modifiable dans la StyleSheet ou bien en JS.

- ASS Facilite la communication et l'accès aux informations de style entre le CSS et le JS.

- Mais également des propriétés CSS inédites facilitant le développement de certaine tache compliqué.

- Ainsi que des fonctions spéciales permettant de réaliser des calcules de couleur...

- Elle dispose d'une simplification de la gestion du responsive.

- Utilisez des conditions pour styliser vos composants !


## Imports
Les imports permettent d'importer des composants CSS, des fonts, des animations... Via des fichiers `.ass` ou bien des CDN de composants `.ass` !

```ass
## Imports component from relative path :
@import(component: Name) from './Your/Component.ass';

## Imports component from a CDN :
@import(component: Name) from url('https://cdn.ass.org/Your/Component.ass');
```

Cette façon d'importer des composants est fonctionnelle pour les polices d'écriture.

```ass
## Imports font from relative path :
@import(font: Name) from './Your/Font.woff';

## Imports font from a CDN :
@import(font: Name) from url('https://cdn.fonts.org/Your/font.woff');
```

```ass
## Imports animation from relative path :
@import(animation: Animation) from './Your/Animation.ass';

## Imports animation from a CDN :
@import(animation: Animation) from url('https://cdn.animations.org/Your/Animation.ass');
```

## Création et utilisation de composant :

La création de composant permet d'éviter de répéter des propriétés CSS entre les composants.

```ass
## Create an ASS component
@create component Modal(size: unit) {
    top: 50%;
    left: 50%
    z-index: 9999;
    position: absolute;
    transform: translate(-50%, -50%);

    width: size;
    height: calc(size / 2);
}
```

```ass
## Using an ASS component
.modal {
    components: Modal(50vw);
}
```

## Déclaration de variables

Toute les variables sont ensuite ajouté dans un index CSS à la racine de la feuille de style.

```ass
## Declare variables
@var black-0 = rgb(0, 0, 0);

@var black-1 = #0a0a0a;
```

## Récupérer des informations entre ASS et le JS

```js
import ass from 'ass.js';

// Get all variables
ass.variables.all(); // Return an map with all variables.

// Get a variable
ass.variables.get('black-1'); // Return the value of 'black-1' variable.

// Edit a variable
ass.variables.edit('black-1', 'rgb(10, 10, 10)'); // Edit the value until page reloading
```

## Fonctions spéciales
Ces fonctions ont vocations à éviter de créer une infinité de variable pour dégrader une couleur.

```as
## Change opacity from a color :
h1 {
    color: @color(#f5f5f5, .5); ## Reduce opacity from the color
}

## Change opacity from a color variable
h1 {
    color: @color(@var(black-1), .5); ## Reduce opacity from the color variable
}

## Use a attribute
h1 {
    color: @attr('color', 'default'); ## Use data-color to color text or us a default
}

input[type=checkbox]:checked {
    @addClass('checked', 'Another one', 'Other one to...') ## Add class when 
}
```

## Simplification des animations et du responsive

- Responsive :
```ass
h1 {
    font-size: 32px;

    @res(1000px to 650px) {
        font-size: 24px;
    }

    @res(650px to 400px) {
        font-size: 16px;
    }
}
```

## Conditions de style
```ass
button {
    @if( @attr('type') = 'primary' ) {
        color: @var(button-primary-color);
    }

    @if( @attr('type') = 'danger') {
        color: @var(button-danger-color);
    }
}
