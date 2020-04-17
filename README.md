# Resumão do Curso de Angular

Principais Tecnologias:
- Node.js (V8 engine Chrome)
npm: Gerenciador de pacotes do Node

- TypeScript
```
  sudo npm install -g typescript
```  
  ECMAScript 5 >> ECMAScript 6 (2015) >> TypeScript
  .ts >> transpiler >> .js

- Angular CLI
```
  sudo npm install -g angular-cli
  sudo npm install -g @angular/cli
```
- Bootstrap (framework css)
```
  npm intall ng2-bootstrap bootstrap --save
```
Editores:
VS Code
WebStorm
Atom
Sublime

- Para criar novo projeto:
```
  ng new nome-projeto
```
package.json: dependências e scripts

# Componente (@Component)
```
  ng g c nome-componente
```
exemplo de .ts:
```
  @Component({
    selector: 'app-roo',
    templateUrl: './app.component.html',
    stylesUrls: [./app/component.css']
    })
   export class AppComponent{
    title = 'Olá'
   }
```
exemplo de .html
```
  <h1>{{title}}</h1>
```  

Template Literals:
  template: 
  ```
  `<p> meu texto aqui</p>`
  ```
- Para executar:
```
  ng serve
```  
  Porta padrão: 4200

# Módulo (@NgModule)
```
  ng g m nome-modulo
```  
exemplo de .ts:
```
  @NgModule({
    declarations:[//declarar componentes, diretivas e pipes aqui...],
    imports:[//importar outros módulos aqui ...],
    providers:[//prover os serviços aqui... ],
    bootstrap: [//colocar o componente raiz* aqui ...],
    exports: [//componentes, diretivas e pipes que serão exportados (expostos)...]}
    })
    *Componente raiz: container da aplicação, onde se declara as rotas, declarar ou chamar o menu da aplicação, ou seja o view port da aplicação
```  
Alguns módulos importantes:
BrowserModule: prepara a aplicação para ser executada em um browser
FormsModule diretiva ngModule
HttpModule requisições Ajax
# Serviço (@Injectable)
```
  ng g s dir/nome-service
```
injeção de dependência: declarar no construtor
exemplo:
```
  constructor (meuService: MeuService){
  }
```
Obs: lembrar de declarar no providers do módulo

# Binding
# Interpolação 
  Componente => Template
  ```
    {{ valor }}
  ```
  É possível executar expressões dentro da interpolação. Ex.: {{ 1 + 1 + getValor() }}
  
# Property Binding
  Componente => Template
  ```
    [propriedade]="valor"
  ```
  Ex.:
  ```
    <img [src]="urlImagem">
    ou
    <img bind-src="urlImagem">
  ```
  Quando não existe uma propriedade no elemento usa-se attr. Ex.: [attr.colspan]

# Event Bindind
  Template => Componente
  ```
    (evento)="handler"
  ```
  Ex.: 
  ```
    (keyup)="onKeyUp($event)"
    ou
    on-keyup="onKeyUp($event)"
  ```
  implementar o código de onKeyUp no .ts
  o valor do elemento pode ser obtido de: $event.target.value
  
  Referência principais eventos: https://developer.mozilla.org/pt-BR/docs/Web/Events

# Two-Way Data Binding    
  Componente <=> Template
  ```
  [(ngModel)]="propriedade"
  
  ```
  Exemplo utilizando property binding e event binding
  ```
  <input type="text" 
    [ngModel]="nome"
    (ngModelChange)="nome = $event"  //pode-se fazer a atribuição sem necessitar de uma função
  ```
  Exemplo two-way data binding:
  ```
  <input type="text" [(ngModel)]="nome">
  ou
  <input type="text" bindon-ngModel="nome">
  ```
  
# Property Binding: Class Binding
  Exemplo:
  ```
    <div class="alert" rolte="alert" 
      [class.alert-success]="classe.value == 'alert-success'">
  ```      
    * aplica a classe alert-success quando a condição classe.value == 'alert-success for verdadeira  

# Property Binding: Style Binding 
  Exemplo:
  ```
    <div class="alert alert-danger" role="alert"
      [style.display]="classe.value == 'alert-danger ? 'block'>
    * aplica o estilo diplay:block no elemento HTML (div), se a condição classe.value == 'alert-danger' for verdadeira      
```    
    
# Input Properties

  ``` 
  no .ts do componente filho:
  @Input('nome') nomeCurso: String = '';
  
  no html do componente pai:
  <meu-componente [nome]="meu nome"></meu-componente>
  
  ``` 
  Obs: Pode-se declarar no metadado inputs da anotação @Component.
  
  # Output Properties
  ``` 
  no .ts do componente filho:
  @Input() valor: number = 0;
  
  @Output() mudouValor = new EventEmitter();
  
  incrementa(){
    this.valor++;
    this.mudouValor.emit({novoValor: this.valor});
  }
  no html do componente pai:
  <meu-component [valor]="valorInicial" mudouValor="onMudouValor($event)"><meu-componente>
  ``` 
# Life-Cycle do Componente (Hooks)
>> ngOnChanges: antes do ngOnInit e quando o valor do property binding é atualizado

>> ngOnInit: quando o componente é inicializado

>> ngDoCheck: a cada ciclo de verificação de mudanças

>> ngAfterContentInit: depois de inserir conteúdo na view

>> ngAfterContectChecked: a cada verificação de conteúdo inserido

>> ngAfterViewChecked: a cada verificação de conteúdo / conteúdo filho

>> ngOnDestroy: antes da diretiva / component ser destruído
