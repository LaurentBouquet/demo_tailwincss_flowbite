## Démo Flowbite

Flowbite est une bibliothèque d'interface utilisateur (UI) basée sur Tailwind CSS. 
Elle fournit des composants préconstruits pour accélérer le développement d'interfaces modernes et réactives. 
Ce guide explique étape par étape comment créer un projet HTML simple avec **Flowbite** et un fichier `index.html` unique.

---

### Pré-requis

Avant de commencer, assurez-vous d'avoir :

1. **Node.js et npm** installés sur votre machine (pour installer Tailwind CSS et Flowbite). Vous pouvez les télécharger depuis [Node.js](https://nodejs.org/).
2. Un éditeur de texte ou un IDE (comme [Visual Studio Code](https://code.visualstudio.com/)).
3. Un navigateur web pour visualiser le projet.

---

### Étape 1 : Créer la structure de base du projet

1. Créez un dossier pour votre projet. Par exemple :
   ```bash
   mkdir projet-flowbite
   cd projet-flowbite
   ```

2. Initialisez un projet Node.js avec npm :
   ```bash
   npm init -y
   ```
   Cela génère un fichier `package.json` qui gère les dépendances de votre projet.

3. Créez un fichier `index.html` dans le dossier principal :
   ```bash
   touch index.html
   ```

---

### Étape 2 : Installer Tailwind CSS

Flowbite repose sur **Tailwind CSS**, vous devez donc commencer par l'installer.

1. Installez Tailwind CSS via npm :
   ```bash
   npm install -D tailwindcss postcss autoprefixer
   ```

2. Initialisez la configuration de Tailwind CSS :
   ```bash
   npx tailwindcss init
   ```
   Cela crée un fichier `tailwind.config.js` dans votre projet.

3. Configurez Tailwind CSS pour qu'il prenne en compte les fichiers HTML. Modifiez le fichier `tailwind.config.js` :
   ```javascript
   module.exports = {
     content: ["./index.html"], // Indiquez que Tailwind doit analyser le fichier index.html
     theme: {
       extend: {},
     },
     plugins: [],
   };
   ```

4. Créez un fichier CSS pour inclure Tailwind. Par exemple, créez un fichier `styles.css` dans le dossier principal :
   ```bash
   touch styles.css
   ```

5. Ajoutez les directives de base de Tailwind dans `styles.css` :
   ```css
   @tailwind base;
   @tailwind components;
   @tailwind utilities;
   ```

6. Compilez le fichier CSS avec Tailwind :
   Ajoutez une commande dans le fichier `package.json` pour générer le CSS :
   ```json
   "scripts": {
     "build:css": "npx tailwindcss -i ./styles.css -o ./dist/output.css --watch"
   }
   ```
   Cela indique à Tailwind de lire `styles.css`, de le compiler et de produire un fichier `output.css` dans un dossier `dist`.

7. Lancez la compilation CSS :
   ```bash
   npm run build:css
   ```

---

### Étape 3 : Installer Flowbite

1. Installez Flowbite via npm :
   ```bash
   npm install flowbite
   ```

2. Ajoutez Flowbite comme plugin dans la configuration de Tailwind. Modifiez le fichier `tailwind.config.js` :
   ```javascript
   module.exports = {
     content: [
       "./index.html",
       "./node_modules/flowbite/**/*.js", // Ajoutez cette ligne pour inclure les composants Flowbite
     ],
     theme: {
       extend: {},
     },
     plugins: [
       require('flowbite/plugin'), // Ajoutez Flowbite comme plugin
     ],
   };
   ```

3. Relancez la commande de compilation de Tailwind si elle n'est pas déjà en cours :
   ```bash
   npm run build:css
   ```

---

### Étape 4 : Ajouter Flowbite à votre fichier HTML

1. Ajoutez la structure de base dans le fichier `index.html` :
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>Projet Flowbite</title>
     <!-- Inclure le CSS généré par Tailwind -->
     <link href="./dist/output.css" rel="stylesheet">
   </head>
   <body>
     <h1 class="text-3xl font-bold text-center mt-8">Bienvenue dans Flowbite</h1>
     <div class="container mx-auto mt-8">
       <!-- Votre contenu Flowbite ira ici -->
     </div>
     <!-- Inclure Flowbite JS -->
     <script src="./node_modules/flowbite/dist/flowbite.min.js"></script>
   </body>
   </html>
   ```

2. Ajoutez un composant Flowbite pour tester. Par exemple, un bouton simple avec un modal :
   ```html
   <button data-modal-target="example-modal" data-modal-toggle="example-modal" class="block text-white bg-blue-500 hover:bg-blue-700 font-medium rounded-lg text-sm px-5 py-2.5 text-center">
     Ouvrir un Modal
   </button>

   <!-- Modal -->
   <div id="example-modal" tabindex="-1" class="hidden fixed top-0 left-0 right-0 z-50 w-full p-4 overflow-x-hidden overflow-y-auto h-full max-h-full">
     <div class="relative w-full max-w-2xl max-h-full">
       <div class="relative bg-white rounded-lg shadow">
         <div class="flex items-start justify-between p-4 border-b rounded-t">
           <h3 class="text-xl font-semibold text-gray-900">
             Exemple de Modal
           </h3>
           <button type="button" class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm p-1.5 ml-auto inline-flex items-center" data-modal-hide="example-modal">
             <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
               <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 011.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"></path>
             </svg>
           </button>
         </div>
         <div class="p-6 space-y-6">
           <p class="text-base leading-relaxed text-gray-500">
             Ceci est un exemple de contenu dans un modal.
           </p>
         </div>
         <div class="flex items-center p-6 space-x-2 border-t border-gray-200 rounded-b">
           <button data-modal-hide="example-modal" type="button" class="text-white bg-blue-500 hover:bg-blue-700 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center">
             Fermer
           </button>
         </div>
       </div>
     </div>
   </div>
   ```

---

### Étape 5 : Tester le projet

1. Ouvrez le fichier `index.html` dans un navigateur pour voir le résultat :
   ```bash
   open index.html # Sur Mac
   start index.html # Sur Windows
   xdg-open index.html # Sur Linux
   ```

2. Cliquez sur le bouton pour ouvrir le modal et vérifier que tout fonctionne correctement.

---

### Étape 6 : Résolution des problèmes

- Si le CSS ne s'applique pas, vérifiez que le fichier `output.css` est bien généré et référencé correctement dans le fichier HTML.
- Si les composants Flowbite ne fonctionnent pas (comme le modal), assurez-vous que le script `flowbite.min.js` est correctement inclus dans le fichier HTML.

---

### Résultat attendu

Vous devriez voir une page avec un titre centré, un bouton, et un modal fonctionnel. Félicitations, vous avez créé un projet HTML simple avec Flowbite ! 🎉
