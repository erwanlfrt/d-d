# tp

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).



# Informations
L'onglet "configure" est un onglet de filtre. Par défaut, tous les sorts sont retournés à l'utilisateur dans l'onglet "search". Ensuite l'utilisateur peut appliquer des filtres pour sélectionner des sorts par livre, classes, niveau (implique que la classe soit sélectionnée), ... 

Le filtre "name" filtrent tous les sorts contenant "name" dans le nom. Par exemple en tapant "abri" le site retournera les sorts "fabrication" ainsi que "abri". 

Si les filtres ne contiennent rien (la valeur par défaut étant soit rien pour les input de type texte soit "select a ..." pour les select), ils ne sont pas appliqués dans la recherche. 


