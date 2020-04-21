# Resumão do Curso de Angular

Principais Tecnologias:
- Node.js (V8 engine Chrome)
- TypeScript
- Jasmine / Karma
- Protractor


npm: Gerenciador de pacotes do Node
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
    <div class="alert" role="alert" 
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
>> ngOnChanges: antes do ngOnInit e quando o valor do input property é atualizado.

>> ngOnInit: quando o componente é inicializado

>> ngDoCheck: a cada ciclo de verificação de mudanças

>> ngAfterContentInit: depois de inserir conteúdo na view

>> ngAfterContectChecked: a cada verificação de conteúdo inserido

>> ngAfterViewChecked: a cada verificação de conteúdo / conteúdo filho

>> ngOnDestroy: antes da diretiva / component ser destruído

# ViewChild
Acesso ao DOM e ao template.

  .html
  ``` 
  <input type="text [value]="valor">
  trocar por:
  <input type="text #campoInput>
  ``` 
  .ts
  HTMLElement possui vários tipos, por isso é bom exibir o conteúdo no console para definir qual é o tipo exato que deve ser utilizado
  ``` 
  @ViewChild('CampoInput') campoValorInput: HTMLElement
  ou o tipo específico
  @ViewChild('CampoInput') campoValorInput: ElementRef
  ...
  this.campoValorInput.nativeElement.value++;
  ``` 
  
# Angular CLI
  Comandos para a criação de projetos:
  ```  
  node -v
  sudo npm install -g anulaar-cli
  ng new nome-projeto
  ng serve
  localhost:4200
  
  cd diretorio
  ng init (cria projeto angular em um diretório já existente)
   ```  
    
  - Pré processadores CSS
  Em um novo projeto:
  ```  
  ng new nome-projeto --style=sass
  ng new nome-projeto --style=less
  ng new nome-projeto --style=stylus
  ```  
  
  Em um projeto existente:
  ```  
  ng set defaults.styleExt scss
  ng set defaults.styleExt less
  ng set defaults.styleExt styl
  ```  
    
  - Lint: escanea o código procurando pequenos erros e verifica as boas práticas do style guide
  jslint
  
  ```  
  ng lint
  ```  
  
# Testes
  Testes Unitários com Jasmine / Karma:
  - Jasmine: Ferramenta BDD (testes orientados a comportamento). São gerados arquivos .spec.ts
  - Karma: É um test runner. Ele automatiza os testes em diversos navegadores web com um único comando. O arquivo tests.ts é            usado para configurar como serão realizados os testes.
  ```  
  ng test
  ```  
  exemplo de teste unitário escrito em typescript e Jasmine:
  ```  
  import { TestBed, async } from '@angular/core/testing';
  import { RouterTestingModule } from '@angular/router/testing';

  import { AppComponent } from './app.component';

  describe('AppComponent', () => {
    beforeEach(async(() => {
      TestBed.configureTestingModule({
        imports: [
          RouterTestingModule
        ],
        declarations: [
          AppComponent
        ],
      }).compileComponents();
    }));

    it('should create the app', async(() => {
      const fixture = TestBed.createComponent(AppComponent);
      const app = fixture.debugElement.componentInstance;
      expect(app).toBeTruthy();
    }));

    it(`should have as title 'app'`, async(() => {
      const fixture = TestBed.createComponent(AppComponent);
      const app = fixture.debugElement.componentInstance;
      expect(app.title).toEqual('app');
    }));

    it('should render title in a h1 tag', async(() => {
      const fixture = TestBed.createComponent(AppComponent);
      fixture.detectChanges();
      const compiled = fixture.debugElement.nativeElement;
      expect(compiled.querySelector('h1').textContent).toContain('Welcome to app!');
    }));
  });
  ```  
  
  Testes de Integração (e2e: end to end) com Protractor / Karma
  ```  
  npm e2e
  ```  
  exemplo de teste de integração:  
  ```  
  import { AngularNgrx4ExamplePage } from './app.po';

  describe('angular-ngrx4-example App', () => {
    let page: AngularNgrx4ExamplePage;

    beforeEach(() => {
      page = new AngularNgrx4ExamplePage();
    });

    it('should display welcome message', () => {
      page.navigateTo();
      expect(page.getParagraphText()).toEqual('Welcome to app!');
    });
  });
  ```  
  
# Build
Build de dev:
  ```  
  ng build --target=development --environment=dev
  ng build --dev --e=dev
  ng build --dev
  ng build
  ```  
O build de dev não é ofuscado e nem minimizado.

O build é gerado na pasta dist. São gerados os seguintes arquivos:
  index.html
  inline.js +
  inline.map
  main.bundle.js + todo o código fonte da aplicação templates html e css
  main.map
  polyfills.bundle.js + código auxiliar que ajuda o browser a renderizar
  polyfills.map    
  
Build de prod:
  No build de produção os arquivos são minificados e ofuscados. O nome do arquivo main.bundle.js e polyfills.bundle.js é acrescido de um código para evitar problemas com o cache da aplicação
  No index html é adicionado um import para inline e polyfills e bundle
  ```  
  ng build --target=production --environment=prod
  ng build --prod --env=prod
  ng build --prod
  ```  
  
  O Node.js possui um servidor http que pode ser usado para testar a aplicação
  ```  
  npm install http-server -g
  ```  
  Para testar a aplicação é necessário entrar no diretório dist e rodar o comando http-server.
  Vantagem: Não precisa instalar servidor apache para testar código simples
  
  Na aba network do browser é possível observar os arquivos que são carregados

  
 # Instalar bibliotecas externas
 Instalação do bootstrap
 ```  
 npm install --save boostrap@next
 ```  
 Incluir dependências: jquery e tether (faz meio de campo entre jquery e boostrap)
 No arquivo angular-cli.json os imports deverão ser colocados na sessão styles e scripts, evitando assim, poluir o index.html
 olhar documentação do angular-cli no github: https://github/angular/angular-cli

Instalação do lodash
 ```  
 npm install --save lodash
 ```  
 
 # Diretivas
 Diretivas são instruções fornecidas ao template. 
 Componentes são diretivas com template.
 - Diretivas estruturais: usadas para modificas a estrutura do DOM. Ex.: *ngFor e *ngIf *switchCase 
 Diretivas de atributos: interagem com o elemento em que foram aplicadas. Ex.: ng-class e ng-style 
 
 # *ngIf
 Controla a exibição dos elementos no DOM. 
  ```  
*ngIg="condição" 
  ```  
 Exemplo:
  ```  
  <div *ngIf="cursos.length > 0">
    lista os cursos aqui
  </div>
  ```  
  Cuidado com performance.
  No lugar do *ngIf podemos usar a propriedade hidden.
  Obs: Quando a exibição está condicionada a direitos de acesso é melhor usar a diretiva *ngIg
  ```  
  <div [hidden]="mostrarCursos">
    lista os cursos aqui
  </div>
  ```  

# ngSwitch, *ngSwitchCase e *ngSwitchDefault
  Muito útil para fazer navBar
  ```  
  <nav class="navbar navbar-dark bg-primary">
    <div class="nav navbar-nav">
        <a class="nav-item nav-link"
            [class.ative]="aba == 'home'"
            (click)="aba" = 'home'">Home
        </a>
        <a class="nav-item nav-link"
            [class.ative]="aba == 'mapa'"
            (click)="aba" = 'home'">Mapa
        </a>
        ...
    </div>
  </nav>

  <div class="container" [ngSwitch]="aba">
    <p *ngSwitchCase="'mapa'">Modo mapa ativado</p>
    <p *ngSwitchCase="'lista'">Modo lista ativado</p>
    ...
  </div>
  ```  
 # *ngFor 
  ```  
  <ul>
      <li *ngFor="let curso of cursos">
          {{ curso }}
      </li>
  </ul>

  <ul>
      <li *ngFor="let curso of cursos, let i = index">
          {{ i }} - {{ curso }}
      </li>
  </ul>
  ```  
  
# Uso do *
O asterisco o Angular irá reescrever o código utilizando a tag template.
Exemplo:
```  
<div *ngIg="mostrar">
</div>

<template [ngIg]="mostrar">
    <div>Listar aqui...</div>
</template>
```      

# Diretiva ngClass
  ```  
  <h1>
      <i class="glyphicon"
         [ngClass]="{
              'glyphicon-star-empty': !condicao,
              'gyphicon-star': condicao
         }"
         (click)="onClick()"
      >
      </i>
  </h1>
  ```  

# Diretiva ngStyle
  ```  
  <button
      [ngStyle]="{
          'backgroundColor': ativo ? 'blue' : 'gray',
          'color': ativo ? 'white' : 'black',
          'fontWhegth': 'ativo ? 'bold' : 'normal'
          'fontSize': tamanhoFonte + 'px'    
      }"
  </button>
  ```  
# Operador Elvis ( ? )
  ```  
  de:
    <p> Responsável: {{ tarefa.responsavel != null ? tarefa.responsabel.nome : ''}} </p>
  para:
    <p> Responsável: {{ tarefa.responsavel?.nome}} </p>
  ```  
# ng-content
  Exemplo de transclusão:

    ```  
    componente filho: painel-component
    <div class="panel panel-defaul">
        <div class="panel-heading">
            <ng-content select=".titulo"></ng-content>
        </div>
        <div class="panel-body">
            <ng-content select=".corpo"></ng-content>
        </div>
    </div>

    componente pai: app-component
    <painel-component>
        <div class="titulo">Título do Painel</div>
        <div class="corpo">Corpo</div>
    </painel-component>
    ```  
# Exemplo de Criação de uma Diretiva de Atributo utilizando ElementRef e Renderer
  Diretivas: 
    - possuem apenas o aquivo .ts
    - em geral ficam no diretório shared
  ```  
  ng g d
  ```  

  Diretiva: fundo-amarelo.directive.ts
  * Atentar ao detalhe do uso dos colchetes no nome da diretiva
  ```  
    @Directive({
        selector: '[fundoAmarelo]' // para qualquer elemento
        selector: 'button[fundoAmarelo]' // aplicável apenas para button
    })
    export class FundoAmareloDirective{
        constructor(
            private _elementRef: ElementRef,
            private _renderer: Renderer){

            //console.log(this._elmentRef);
            //this._elementRef.nativeElment.style.backgroundColor = 'yellow';
            /*Para evitar ataque de cross scripting (xxs) não é recomendável
              fazer acesso direto aos elementos do DOM usando ElementRef.
              O ideal é utilizar a forma alternativa abaixo:*/
            this._renderer.setElementStyle(
                this._elementRef.nativeElement,
                'backgroun-color',
                'yellow');
        }
    }
  ```  

  Exemplo de aplicação de uma diretiva em um elemento do template do componente:
    ```  
    <p fundoAmarelo>
        Texto com fundo amarelo
    </p>
    ```  

# HostListener e HostBinding

  HostListener: Utilizado quando precisamos escutar um evento de um elemento no componente pai (hospedeiro). Fica escutando eventos no hospedeiro da diretiva.

  HostBinding: Permite a associação de um atributo da diretiva para um determinado atributo do html

  Código da diretiva highlight-mouse.directive.ts:
  ```
  import { Directive, HostListener } from '@angular/core';

  @Directive({
      selector: '[highlightMouse]'
  })
  export class HighlightMouseDirective{

      @HostListener('mouseenter') onMouseOver(){
          /*  O uso de um atributo da diretiva ligado a um atributo do html no 
              hopedeiro, elimina a necessidade do código abaixo:
          this._renderer.setElementStyle(
              this._elementRef.nativeElement, 'background-color', 'yellow'
          );
          */

          this.backgroudColor = 'yellow';
      }

      @HostListener('mouseleave') onMouseLeave(){
          /*  O uso de um atributo da diretiva ligado a um atributo do html no 
              hopedeiro, elimina a necessidade do código abaixo:
          this._renderer.setElementStyle(
              this._elementRef.nativeElement, 'background-color', 'yellow'
          );
          */

          this.backgroudColor = 'white';
      }

      //@HostBinding('style.backgroundColor') backgroundColor: string;
      @HostBinding('style.backgroundColor') get setColor(){
          return this.backgroundColor;
      }
      private backgroundColor: string;

      constructor(
          /*
          private _elementRef: ElementRef,
          private _renderer: Renderer
          */
      ){}
  }
  ```
  Código do componente pai (hospedeiro):
  ```
  <p highlightMouse>
      Texto com highlight quando passo o mouse...
  </p>
  ```
  
# Diretiva com Input Property

Template HTML do hopedeiro:
    [highlight] é uma diretiva e tbm um input propert para a diretiva
  ```
    <p [highlight]="'red'" [defaultColor]="'grey'">
        Texto com highlight com cores customizadas
    </p>
  ```
.ts do componente:
  ```
    @Directive({
        selector: '[highlight]'
    })
    export class HighlightDirective{

        @HostListener('mouseenter') onMouseOver(){
            this.backgroundColor = this.highlightColor;
        }

        @HostListener('mouseleave') onMouseLeave(){
            this.backgroundColor = this.defaultColor;
        }

        //Binda o estilo backgroundColor do hopedeiro para ser acessado no componente.
        @HostBinding('style.backgroundColor' backgroundColor: string;

        @Input() defaultColor: string = 'white';
        @Input('highlight') highlightColor: string = 'yellow';

        constructor(){}

    }
  ```
  
  # Exemplo de diretiva estrutural
  
  TemplateRef faz referência à tag <template> e ViewContainerRef faz referência ao conteúdo da tag.
  Nesse exemplo [ngElse] é diretiva e também um input property. A diretiva recebe um valor ou expressão booleana que deverá ser avaliada. Caso a expressão seja verdadeira, será realizada uma ação. Por isso se faz necessário transformar o input property em um método setter, como vemos abaixo:

```
  import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';

  @Directive({
      selector: '[ngElse]'
  })
  export class NgElseDirective{

      @Input() set ngElse(condition: boolean){
          if (!condition){
              this._viewContainerRef.createEmbeddedVieew(this._templateRef);
          }
      }

      constructor(
          private _templateRef: TemplateRef<any>,
          private _viewContainerRef: ViewContainerRef
      ){ }

  }
```

.HTML do componente hospedeiro:

```
  <div *ngIf="mostrarCursos">
      Lista de cursos aqui ...
  </div>
  <div *ngElse="mostrarCursos">
      Não existem cursos para serem listados ...
  </div>
```

Desestruturando ficaria assim:

```
  <template [ngElse]="mostrarCursos">
      <div>
          Não existem cursos para serem listados...
      </div>
  </template>
```  

exemplo no github do projeto angular: 
https://github.com/angular/angular/blob/698b0288bee60b8c5926148b79b5b93f454098db/packages/common/src/directives/ng_if.ts

# Código antigo do NgIf
Observar o uso da variável auxiliar _hasview que tem o objetivo de evitar a renderização desnecessária:

```  
  @Directive({selector: '[ngIf]'})
  export class NgIf{

      private _hasView = false;

      constructor(private _viewContainer: ViewContainerRef, private _template: TemplateRef<Object>){}

      @Input()
      set ngIf(condition: any){
          if(condition && !this._hasView){
              this._hasView = true;
              this._viewContainer.createEmbeddedView(this._template);
          }else if(!condition && this._hasView){
              this._hasView = false;
              this._viewContainer.clear();
          }
      }
  }
```    
# Serviços
DRY (Dont Repeat Yourself): Evitar repetição de código

CRUD
Lógica de negócio deve ficar nas classes de seviço
Classes utilitárias

# Serviços
    DRY (Dont Repeat Yourself): Evitar repetição de código

    - CRUD
    - Lógica de negócio deve ficar nas classes de seviço
    - Classes utilitárias

# Escopo de serviços e módulos

  1 - Escopo: Toda aplicação (Padrão Singleton)
    Declarar no Módulo raiz: app.module.ts
    Haverá uma única instância do serviço disponível para toda a aplicação
    Obs: No módulo raiz usamos BrowserModule para preparar a aplicação para rodar em um Browser.
    ```    
    @NgModule({
        declarations: [],
        imports: [],
        providers:[CursosService]
    })
    ```    

  2 - Escopo: Módulo
    Declarar no módulo Módulo de Funcionalidade
    Todos os componentes do módulo poderão instanciar o serviço.
    Obs: No módulo de funcionalidade usamos CommonModule no lugar de BrowserModule.
    ```    
    @NgModule({
        declarations: [],
        imports: [],
        providers:[CursosService]
    })
    ```    

  3 - Escopo: Componente
    Declarar o serviço no metadado providers de @Component
    Apenas o componente poderá instanciar o serviço
    ```    
    @Component({
        seletor: 'app-cursos',
        templateUrl:'./cursos.component.html',
        styleUrls: ['./cursos/component.css'],
        providers: [CursosService]
    })
    ```    
# Comunicação entre componentes usando serviços
(broadcast de eventos)

A comunicação entre componentes pai e filho se dá por meio de input property e output property. Quando não há relação entre componentes a comunicação se dá por meio de serviços

cursos.service.ts:
```    
  @Injectable()
  export class CursosService {

      emitirCursoCriado = new EventEmitter<string>();
  ...
      add.Curso(curso: string){
          this.cursos.push(curso);
          this.emitirCursoCriado.emit(curso);
      }
  }
```    
cursos.componet.ts:
```    
  @Component()
  export class CursosComponent {
      constructor(private cursosService: CursosService);
      ...
      ngOnInit(){
          this.cursos = this.cursosService.getCursos();

          //Se inscreve no observable (emitter) do serivço CursosService
          this.cursosService.emitirCursoCriado.subscribe(
              curso => console.log(curso);        
          );
      }
  }
```    
receber-cursos.componet.ts:
```    
  @Component()
  export class ReceberCursosComponent {

      constructor(private cursosService: CursosService);
      ...
      ngOnInit(){     
          this.cursosService.emitirCursoCriado.subscribe(
              curso => console.log(curso);        
          );
      }
  }
```    

No exemplo acima, ambos os componentes devem estar no mesmo escopo de serviço, caso contrário, não será possível notifica-los ao mesmo tempo, pois cada construtor gera instâncias distintas do serviço.

É possível realizar a comunicação entre componentes de módulos diferentes. Nesse caso, é necessário declarar o emitter como uma variável estática. Dessa forma, as várias instâncias do serviço passam a ter acesso ao mesmo emitter:
 
No serviço:
```    
  static criouNovoCurso = new EventEmitter<string>();
  ...
    addCurso(curso: string){
        ...
        CursosService.criouNovoCurso.emit(curso); //Não acessa via this e sim via Classe
    }
```    
Nos componentes:
```    
  construtor(private cursosService: CursosService){}

    ngOnInit(){
        this.cursos = this.cursosService.getCursos();

        CursosService.criouNovoCurso.subscribe(
            curso => console.log(curso);
        );
    }
```    
Template Literals:
`Criando um novo curso ${curso}`


# Injetando um serviço em outro serviço
```    
@Injectable()
export class CursosService{
    ...
    constructor(private logService: LogService){
        console.log('CursosService');

    }
}
```    
    
#Pipes

#Usando pipes: Parâmetros e pipes aninhados
Exempos de pipes embutidos no Angular:
<p>Título: {{ livro.titulo | uppercase }}</p>
<p>Estrelas: {{ livro.rating | number:'2.1-2'}}</p>
<p>Páginas: {{ livro.numeroPaginas | number }}</p>
<p>Preço: {{ livro.preço | currency:'BRL':'true' }}</p>
<p>Data Lançamento: {{ livro.dataLancamento | date:'dd-MM-yyyy' }}</p>
<p> URL: {{ livro.url }}</p>
<p>Livro: {{ livro | json }}</p>

