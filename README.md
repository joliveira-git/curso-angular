#Curso de Angular

- Node.js
V8 engine Chrome

npm: Gerenciador de pacotes do Node

- TypeScript
sudo npm install -g typescript
ECMAScript 5 >> ECMAScript 6 (2015) >> TypeScript
.ts >> transpiler >> .js

- Angular CLI
sudo npm install -g angular-cli
sudo npm install -g @angular/cli

Services 

Editores:
VS Code
WebStorm
Atom
Sublime


- Para criar novo projeto:
ng new nome-projeto

# Componente (@Component)
ng g c nome-componente

exemplo de .ts:
@Component({
  selector: 'app-roo',
  templateUrl: './app.component.html',
  stylesUrls: [./app/component.css']
  })
 export class AppComponent{
  title = 'Olá'
 }

exemplo de .html
<h1>{{title}}</h1>

Template Literals:
template: `<p> meu texto aqui</p>`

- Para executar:
ng serve
Porta padrão: 4200

# Módulo (@NgModule)
ng g m nome-modulo
exemplo de .ts:
@NgModule({
  declarations:[//declarar componentes, diretivas e pipes aqui...],
  imports:[//importar outros módulos aqui ...],
  providers:[//prover os serviços aqui... ],
  bootstrap: [//colocar o componente raiz aqui ...]
  })
  
  

