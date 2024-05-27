# Questions et Réponses pour un Développeur Angular Senior

## Questions sur les concepts de base

1. **Expliquez le concept de "data binding" en Angular et les différents types qui existent.**
   - Le data binding est un mécanisme qui permet de synchroniser les données entre le modèle (le code TypeScript) et la vue (le template HTML). Les différents types de data binding en Angular sont :
     - **Interpolation ({{}})** : Utilisé pour afficher des données dans le template.
     - **Property binding ([property])** : Permet de lier des propriétés du DOM à des propriétés du composant.
     - **Event binding ((event))** : Permet de lier des événements du DOM à des méthodes du composant.
     - **Two-way binding ([(ngModel)])** : Combine property binding et event binding pour synchroniser les données dans les deux sens.

2. **Qu'est-ce qu'un "Decorator" en Angular et quels sont les différents types de décorateurs que vous pouvez utiliser ?**
   - Les décorateurs sont des fonctions qui modifient le comportement des classes, méthodes ou propriétés. Les types de décorateurs en Angular incluent :
     - **@Component** : Définit une classe comme un composant Angular.
     - **@Directive** : Définit une classe comme une directive Angular.
     - **@Pipe** : Définit une classe comme un pipe Angular.
     - **@Injectable** : Indique qu'une classe peut être injectée comme une dépendance.
     - **@NgModule** : Définit une classe comme un module Angular.

3. **Quelle est la différence entre un module, un composant et un service en Angular ?**
   - **Module (NgModule)** : Un conteneur pour un ensemble de composants, directives, pipes et services. Chaque application Angular a au moins un module racine, AppModule.
   - **Composant** : Une classe associée à un template HTML qui contrôle une partie de l'interface utilisateur.
   - **Service** : Une classe qui encapsule une logique métier réutilisable et peut être injectée dans des composants ou d'autres services via le système de dependency injection d'Angular.

4. **Comment fonctionne le cycle de vie d'un composant Angular ? Pouvez-vous décrire les différents hooks disponibles ?**
   - Les composants Angular ont plusieurs hooks de cycle de vie que vous pouvez utiliser pour intervenir à différents points de leur vie :
     - **ngOnChanges** : Appelé quand une propriété liée à des données change.
     - **ngOnInit** : Appelé après la création du composant, idéal pour initialiser les données.
     - **ngDoCheck** : Appelé à chaque cycle de détection des changements.
     - **ngAfterContentInit** : Appelé après l'insertion du contenu dans le composant.
     - **ngAfterContentChecked** : Appelé après chaque vérification du contenu du composant.
     - **ngAfterViewInit** : Appelé après l'initialisation des vues du composant.
     - **ngAfterViewChecked** : Appelé après chaque vérification des vues du composant.
     - **ngOnDestroy** : Appelé juste avant la destruction du composant, utile pour le nettoyage.

## Questions sur les sujets intermédiaires

1. **Comment fonctionne la détection des changements en Angular et quelles sont les stratégies disponibles ?**
   - Angular utilise la zone.js pour détecter les changements dans les composants. Deux stratégies principales sont disponibles :
     - **Default** : Vérifie tous les composants descendants lorsque l'état du composant change.
     - **OnPush** : Ne vérifie les composants que lorsque leurs inputs changent, ce qui peut améliorer les performances en évitant des vérifications inutiles.

2. **Qu'est-ce que les "Observables" et les "Promises" ? Pouvez-vous donner un exemple d'utilisation de chacun dans un contexte Angular ?**
   - **Observables** : Fournis par RxJS, ils permettent de travailler avec des flux de données asynchrones. Utilisés souvent avec Angular pour gérer les requêtes HTTP.
     ```typescript
     this.http.get('/api/data').subscribe(data => console.log(data));
     ```
   - **Promises** : Une abstraction pour représenter une valeur qui peut être disponible maintenant, ou dans le futur, ou jamais. Moins flexible que les Observables pour les opérations asynchrones complexes.
     ```typescript
     this.http.get('/api/data').toPromise().then(data => console.log(data));
     ```

3. **Comment gérez-vous la navigation et le routage dans une application Angular ?**
   - Angular utilise le module Router pour gérer la navigation entre les vues. Vous définissez des routes dans un module de routage en associant des chemins URL à des composants.
     ```typescript
     const routes: Routes = [
       { path: '', component: HomeComponent },
       { path: 'about', component: AboutComponent },
     ];
     ```

4. **Expliquez comment fonctionne la gestion des formulaires en Angular, et la différence entre les formulaires "template-driven" et "reactive".**
   - Angular supporte deux types de formulaires :
     - **Template-driven** : Basés sur des templates HTML, plus simples et conviviaux pour les formulaires simples.
       ```html
       <form #form="ngForm" (ngSubmit)="onSubmit(form)">
         <input name="name" ngModel required>
       </form>
       ```
     - **Reactive** : Utilisent des modèles de données explicites et sont plus puissants pour les formulaires complexes et dynamiques.
       ```typescript
       this.form = this.fb.group({
         name: ['', Validators.required],
       });
       ```

## Questions avancées

1. **Qu'est-ce que la "lazy loading" et comment l'implémenter dans une application Angular ?**
   - La lazy loading permet de charger les modules uniquement lorsque cela est nécessaire, ce qui améliore les performances initiales de l'application. Pour l'implémenter :
     ```typescript
     const routes: Routes = [
       { path: 'feature', loadChildren: () => import('./feature/feature.module').then(m => m.FeatureModule) }
     ];
     ```

2. **Comment gérez-vous l'internationalisation (i18n) dans une application Angular ?**
   - Angular offre un support intégré pour l'internationalisation via le module `@angular/localize`. Vous pouvez marquer les textes à traduire dans vos templates et utiliser le CLI Angular pour extraire les messages et générer des fichiers de traduction.
     ```typescript
     import '@angular/localize/init';
     ```

3. **Pouvez-vous expliquer comment utiliser les "Angular Modules" (NgModules) pour organiser et structurer votre application ?**
   - Les NgModules sont utilisés pour regrouper des composants, directives, pipes et services qui sont liés, et pour organiser le code en parties réutilisables et modifiables. Chaque application Angular commence avec un module racine (AppModule) et peut être divisée en modules fonctionnels ou de fonctionnalités.
     ```typescript
     @NgModule({
       declarations: [AppComponent, FeatureComponent],
       imports: [BrowserModule, FeatureModule],
       bootstrap: [AppComponent]
     })
     ```

4. **Comment implémenter des tests unitaires et des tests d'intégration dans une application Angular ? Pouvez-vous donner un exemple ?**
   - Angular CLI crée une configuration de test par défaut utilisant Jasmine et Karma pour les tests unitaires, et Protractor pour les tests d'intégration.
     ```typescript
     it('should create the app', () => {
       const fixture = TestBed.createComponent(AppComponent);
       const app = fixture.debugElement.componentInstance;
       expect(app).toBeTruthy();
     });
     ```

## Questions sur l'optimisation et la performance

1. **Quelles sont les meilleures pratiques pour optimiser les performances d'une application Angular ?**
   - Utiliser la stratégie de détection des changements OnPush.
   - Implémenter la lazy loading pour les modules.
   - Utiliser des pipes asynchrones pour les flux de données.
   - Minimiser les binding et les watchers inutiles.

2. **Comment pouvez-vous réduire la taille du bundle d'une application Angular ?**
   - Activer le tree shaking pour éliminer le code non utilisé.
   - Utiliser le ahead-of-time (AOT) compilation.
   - Activer les optimisations de production avec Angular CLI (`ng build --prod`).
   - Compresser les fichiers JavaScript avec gzip ou brotli.

3. **Qu'est-ce que le "tree shaking" et comment Angular l'utilise-t-il ?**
   - Le tree shaking est une technique pour éliminer le code mort ou non utilisé lors de la compilation. Angular utilise le tree shaking lors de la compilation AOT pour réduire la taille du bundle.

4. **Comment débugger et profiler les performances d'une application Angular ? Quels outils utilisez-vous ?**
   - Utiliser les DevTools du navigateur pour profiler les performances.
   - Utiliser Augury, une extension Chrome pour débugger les applications Angular.
   - Utiliser les outils de performance intégrés à Angular CLI (`ng build --prod --stats-json`).

## Questions sur les fonctionnalités spécifiques

1. **Comment implémentez-vous la communication entre composants Angular ?**
   - Utiliser des Input et Output decorators pour la communication parent-en
