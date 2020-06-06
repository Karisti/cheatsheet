# Apuntes AngularJS
## Conceptos básicos

### Preparando el entorno de trabajo
- Descargar [NodeJS](https://nodejs.org/es/)
- Descargar [Angular CLI](https://cli.angular.io/)

```shell
    npm install -g @angular/cli
    ng new my-dream-app
    cd my-dream-app
    ng serve --open
```

### Directivas
#### ngModel
Lo que nosotros pongamos en el input text se verá reflejado en la variable 'title'.
```
<input type="text" [(ngModel)]="title">
```
#### *ngIf
```
<div *ngIf="title === 'kepa'">
	hello
</div>
```
#### *ngFor
```
<li *ngFor="let name of items; index as i">
	{{ name }} {{ i }}
</li>
```


### Estructura del proyecto
  - `node_modules` librerías.
  - `package.json` dependencias.
  - `src` donde tendremos todo el código.

### Ruteo
En `app.module.ts`.

Primero importamos:
```
import { Routes, RouterModule } from '@angular/router';
```
Después añadimos los PATHS de cada componente:
```
const appRoutes : Routes = [
	{path:'', component: HomeComponent},
	{path:'home', component: HomeComponent},
	{path:'login', component: LoginComponent},
	{path:'conversation/:uid', component: ConversationComponent},
	{path:'profile', component: ProfileComponent}
];
```
Y añadimos el `appRoutes` a los imports de `@NgModule`:
```
imports: [
    RouterModule.forRoot(appRoutes)
]
```
Hay que insertar lo siguiente en `app.component.html` (o el html que queramos) para indicar que inserte lo del ruteador:
```
<router-outlet></router-outlet>
```

### Navegando
```
<nav>
	<!-- routerLink es una directiva de typeScript para simular la navegación de Single Page Application -->
	<a routerLink="/login">Login</a> |
	<a routerLink="/home">Inicio</a> |
	<a routerLink="/schedules">Horarios</a> |
</nav>
```

### Path con parámetros
```
 {path: 'conversation/:uid', component: ConversationComponent}
```
  Obtenemos el uid en la página de esta forma:
```
export class ConversationComponent implements OnInit {
	friendId: any;

	constructor(private activatedRoute: ActivatedRoute) {
		this.friendId = this.activatedRoute.snapshot.params['uid']
	}
	ngOnInit() {
	}
}
```

### Creando componentes
1. Generamos un nuevo componente desde la consola:
```
ng generate component {nombreComponente}
```
2. Vamos a `{nombreComponente}.component.html` e insertamos el código que queramos en el componente, en este caso un menú:
```
<a routerLink="/login">Login</a> |
<a routerLink="/home">Inicio</a> |
<a routerLink="/schedules">Horarios</a> |
```
3. Insertamos el componente en el HTML, en este caso `app.component.html` para que se muestre:
```
<app-menu></app-menu>
```

  ### Interfaces
```
      export interface User {
        nick: string;
        subnick?: string;
        age?: number;
        email: string;
        friend: boolean;
        uid: any;
      }
```

### Services
1. Creamos la carpeta `/app/services`.
2. Vamos a la consola y hacemos:
```
ng generate service services/{nombre_servicio}
```
3. Se genera `user.service.ts`, donde podemos poner el código que queramos poner como servicio.
4. Para poder usarlo en un componente, añadimos el servicio como parámetro del constructor:
```
constructor(private {nombreServicio}: {NombreServicio}) {
}
```
5. En el servicio creamos las funciones que queramos que se puedan usar con ese servicio a través de `nombreServicio`.

### Guards
Nos ayudan a controlar si queremos que se navegue a ciertas páginas o no.
1. Vamos a la consola y hacemos:
```
ng generate guard services/authentication
```
3. Se genera `services/authentication.guard.ts`, donde podemos poner el código que queramos para controlar si permitimos o no el acceso a distintas páginas.
Código de ejemplo:
`authentication.guard.ts`:
```
import { Injectable } from '@angular/core';
import { ActivatedRouteSnapshot, RouterStateSnapshot, UrlTree, CanActivate, Router } from '@angular/router';
import { Observable } from 'rxjs';
import { AuthenticationService } from './authentication.service';
import { map } from 'rxjs/operators';
@Injectable({
	providedIn: 'root'
})
export class AuthenticationGuard implements CanActivate {
	constructor(private authenticationService: AuthenticationService, private router: Router) {}
	canActivate(
		next: ActivatedRouteSnapshot,
		state: RouterStateSnapshot): Observable<boolean> | Promise<boolean> | boolean {
			return this.authenticationService.getStatus().pipe(
				map(status => {
					if (status) {
						return true;
					} else {
					this.router.navigate(['login']);
						return false;
					}
				})
			);
		}
}
```
`app.module.ts`:
```
import { AuthenticationGuard } from './services/authentication.guard';
const appRoutes : Routes = [
  {path:'', component: HomeComponent},
  {path:'home', component: HomeComponent, canActivate: [AuthenticationGuard]},
  {path:'login', component: LoginComponent},
  {path:'conversation/:uid', component: ConversationComponent},
  {path:'profile', component: ProfileComponent, canActivate: [AuthenticationGuard]}
];
```

### Pipes
Nos ayudan a mostrar los datos mejor facilmente.
#### Pipe json
Visuarlizar un objeto como un json.
```
{{friend | json}}
```
#### Pipe number
Enteros como esta, decimales minimo 2 y máximo 2.
```
{{price | number: '1.2-2'}}
```
#### Pipe date
Mostrar un `Date.now()` de forma legible.
```
{{price | date}}
{{price | date: 'medium'}}
{{price | date: 'fullDate'}}
```
#### Pipe personalizado
1. Creamos la carpeta `/app/pipes`.
2. Vamos a la consola y hacemos:
```
ng generate pipe pipes/{nombre_pipe}
```
3. Dentro de la función `transform` manejamos el value y los argumentos para devolver lo que queramos.
```
import { Pipe, PipeTransform } from '@angular/core';
@Pipe({
	name: 'search'
})
export class SearchPipe implements PipeTransform {
	transform(value: any, args: string) {
		if (!value) {
			return;
		}
		if (!args) {
			return value;
		}
		args = args.toLowerCase();
		return value.filter( (item) => {
			return JSON.stringify(item).toLowerCase().includes(args);
		});
	}
}
```
4. Utilizamos el Pipe, en este ejemplo, un Pipe de búsqueda:
```
<br /><br />
<input type="text" placeholder="Buscar amigo" [(ngModel)]="query" />
<br /><br />
<b>Amigos</b>
<ng-container *ngFor="let user of friends | search: query; let i = index">
    <div>
        <a routerLink="/conversation/{{user.uid}}">
            {{i}}. {{user.nick}} - {{user.email}}
        </a>
    </div>
</ng-container>
```

## TypeScript
  - `let variable` una variable.
  - `let c: number = 1` una variable de un tipo concreto.
  - `let j: boolean[] = [true, false, false]` lista de booleans


## Estilos
### Usar estilos CSS y referenciar recursos
Las imagenes y demás recursos se guardan en la carpeta `assets`.
Prueba de añadir imagen en html:
`menu.component.html`
```
<img id="main-logo" src="assets/img/logo_live.png" alt="Logo cute">
```
`menu.component.css`
```
#main-logo {
    width: 60px;
}
```
### Instalar librerías
#### Bootstrap
```
npm install bootstrap --save
npm install bootstrap --save-exact   # si queremos la version exacta
```
#### Font awesome
```
npm install @fortawesome/fontawesome-free --save-exact
```
Una vez añadidas las librerías a nuestro proyecto, hay que añadir los estilos css que vamos a usar en `angular.json`:
```
"styles": [
	"node_modules/bootstrap/dist/css/bootstrap.css",
	"node_modules/@fortawesome/fontawesome-free/css/all.css",
	"src/styles.css"
],
```
### ngClass
Permite usar las clases teniendo en cuenta en qué pantalla estamos por ejemplo.
Para usarlo, vamos a `app.component.ts` y añadimos el router al constructor. (Si no está el constructor, lo creamos):
```
constructor(public router: Router) {
}
```
Ejemplo de cómo quedaría el HTML:
```
<app-menu *ngIf="router.url != '/login'"></app-menu>
<div [ngClass]="{'generalContent': router.url != '/login'}">
    <router-outlet></router-outlet>
</div>
```
### Conectando con Firebase
Buscamos el repositorio de `angularfire2` y seguimos los pasos.
