# Angular Server Side Rendering (SSR)

Ce projet est une implémentation simple du rendu coté serveur d'une application [Angular](https://github.com/angular/angular) avec [express](https://github.com/expressjs/express) sur Node.Js.
L'application en elle même est une todo list.

![todo-list](https://i.imgur.com/2uA4ywp.png)

## Build du projet

La CLI Angular n'a pas été éjectée afin de pouvoir continuer à utiliser des générateurs (`ng g c monComposant` par exemple). 
La build de ce projet s'effectue donc en 2 étapes :
 1. `ng build -prod`
 2. `webpack --config="webpack.server.config.ts"`

Pour lancer le serveur, il suffit ensuite de se placer dans le répertoire `dist` et d'y lancer la commande `node ./main.server.js`

## Les branches 

Ce projet comporte plusieurs branches permettant de comparer les différents cas d'usage du rendu coté serveur.

### master

Sur la branche master se trouve l'exemple le plus simple de rendu coté serveur. Les données sont récupérées de manière synchrone de l'application.

### master-async

Sur cette branche les données sont récupérées de manière asynchrone. Lorsque le navigateur reprend la main sur le DOM généré par le serveur, on peut observer un effet de clignotement dû la mise à jour de ces données.

### preboot

Sur cette branche, [Preboot.js](https://github.com/angular/preboot) est ajouté et la récupération des données est synchrone. Preboot permet de sauvegarder les événements effectués entre le moment où la page est rendue et le moment où elle est interactive. Une fois la page interactive, les événement sont rejoués.

### preboot-async

Sur cette branche, Preboot.js est ajouté et la récupération des données est asynchrone. Ici, plus de clignotement comme dans master-async. En revanche on est obligé d'effectuer le replay des événements manuellement. Si on laisse le replay automatique, Preboot va essayer de rejouer des évenements sur des éléments DOM qui n'existe plus.
