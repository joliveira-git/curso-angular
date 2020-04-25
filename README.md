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


# Pipe Puro
Não olha as modificações do valor que é passado para o parâmetro para o método transform, ou seja, se não mudarem os argumentos, o resultado será o mesmo não importando se houve alguma alteração no conteúdo do parâmetro (string, array, etc)
No exemplo abaixo, o array livros é passado como value para o método transform do pipe que não sobre alteração, mesmo que seja incluido mais um item no array. O array passado ao pipe permanece imutável, por isso se diz que esse tipo de pipe é puro (conceito estudado na programação funcional).
```
ng g p filtro-array
```
HTML do componente:
```
    <input type="text" [(ngModel)]="filtro">
    <br>
    <input type="text" #novoValor>
    <button (click)="addCurso(novoValor.value)">Add</button>

    <lid *ngFor="let liv of livros | filtroArray:filtro">
        {{ liv }} 
    </li>
```

Pipe:
```
    import { Pipe, PipeTransform } from '@angular/core';

    @Pipe({
        name: 'filtroArray'
    })
    export class FiltroArrayPipe implements PipeTransform{

        transform(value: any, args?: any): any{
            if( value.length === 0 || args === undefined){
                return value;
            }
            let filter = args.toLocaleLowerCase();
            return value.filter(
                v => v.toLocaleLowerCase().indexOf(filter) != -1
            );
        }
    }
```

# Pipe Impuro
Para tornar o pipe impuro, é necessário incluir o metadado "pure"

```
    import { Pipe, PipeTransform } from '@angular/core';
    import { FiltroArrayPipe ) from './filtro-array.pipe';

    @Pipe({
        name: 'filtroArrayImpuro',
        pure: false
    })
    export class FiltroArrayImpuroPipe extends FiltroArrayPipe {


    }
```

* É importante dizer que a equipe do Angular não recomenda a utilização de filtros a partir de pipes. Segue abaixo a abordagem correta para resolver o problema:

```
    <li *ngFor="let liv of obterLivros()">
        {{ liv }} 
    </li>
```

```
    ...
    ObterLivros(){
        if ( this.livros.length === 0 || 
             this.filtro === undefined || 
             this.filtro.trim === ''){
            return this.livros;
        }

    }

    return this.livros.filter( (v) => {
        if (v.toLowerCase().indexOf(this.filtro.toLowerCase()) >= 0){
            return true;
        }
        retunr false;
    }

```

# Pipe Async
O pipe Async é útil quando o valor que será exibido na tela é resultado de uma operação assíncrona.
Em Angular esse valor pode ser resultante de uma Promisse ou de um Observable.

Exemplo de valor sendo gerado por uma Promisse:
```
    valorAsync = new Promisse( (resolve, reject) => {
        setTimeout( () => resolve('Valor assíncrono'), 2000)
    });
```

Exempo de valor sendo gerado por um Observable:
```
    valorAsync = Observable.interval(2000)
        .map(valor => 'Valor assíncrono');

```
HTML:
```
    <p>{{ valorAsync | async }} </p>

```

# Rotas
- SPA: Single Page Application
Exemplo de rotas:
  /usuarios/2/edit
  /usuarios
  /usuarios/:id
  /usuarios/:id/edit

- Rotas Filhas: Ex: localhost:4200/contacts/1

- Guardas de Rotas: 
    - Verificar se o usuário está logado e redirecionar para a página de login
    - Verificar se deseja sair da página quando estiver fazendo uma edição


# Criando Rotas

Pode-se declarar as rotas no app.module.ts, mas o ideal é separar em outro arquivo, criando um módulo para armazenar as rotas: 

  1 - Criar o arquivo app.routing.ts:
  ```
      import { ModuleWithProviders } from '@angular/core';
      import { Routes, RouterModule } from '@angular/router';
      ...

      const APP_ROUTES: Routes = [
          { path: 'cursos', component: CursosComponent },
          { path: 'login', component: LoginComponent }, 
          { path: '', component: HomeComponent }

      ];

      export const routing: ModuleWithProviders = RouterModule.forRoot(APP_ROUTES)
  ```
   - A constante do tipo ModuleWithProviders contém a definição e a configuração das rotas do projeto.
   - RouterModule.forRoot: Rotas chave ou principais
   - RouterModule.forChild: Rotas de funcionalidade.

  2 - Importar a variável "routing" do módulo app.routing.ts para o módulo principal da aplicação ( app.module.ts )

  app.module.ts:
  ```
  import { routing } from './app.routing';
  ...
      @NgModule({
          ...
          imports:[...
              routing
          ]
          ...
      })
  ```
  3 - Deve-se incluir uma tag <router-outlet> em app.component.html indicando onde será feita a saída da rota. O componente da rota é renderizado dentro desta tag.

  app.component.html:
  ```
      <router-outlet></router-outlet>
  ```

  4 - O index.html deve estar apontando para a rota raiz. È possível definir um namespace para as rotas. Ex: hRef="/app". Assim, quando acessar a rota login ficará da seguinte forma: localhost:4200/app/login

  index.html:
  ```
      ...
      <head>
          <meta charset="utf-8">
          <title></title>
          <base href="/">
      </head>
  ```

# RoterLink: Definição de rotas no código
Ao clicar em um link a rota deve ser ativada

Ex: NavBar no HTML do componente principal (app.component.html) contendo links para direcionar para diversas páginas

app.component.html:

<nav>
    <div>
        <a routerLink="">Logo: encaminha para a rota principal</a>
        <ul>
            <li><a routerLink="/login">Login</a></li>
            <li><a routerLink="/cursos">Cursos</a></li>
        </ul>
    </div>
</nav>

# routerLinkActive: Aplicação de CSS em Rotas Ativas
A propriedade routerLinkActive recebe uma classe CSS que deve ser aplicada quando o link da rota estiver ativo.

Ex:
```
    <li routerLinkActive="active">
        <a routerLink="/login">Login</a>
    </li>
```


# Route Param - Roteamento com parâmetros

  1 - Criar o parâmetro na rota (cursos/:id):
  app.routing.ts:
  ```
      import { ModuleWithProviders } from '@angular/core';
      import { Routes, RouterModule } from '@angular/router';
      ...
      const APP_ROUTES: Routes = [
          { path: 'cursos/:id', component: CursoDetalheComponent },
          ...
      ];

      export const routing: ModuleWithProviders = RouterModule.forRoot(APP_ROUTES);

  ```
  2 - Passar o parâmetro para a rota. Isso pode ser feito de forma dinâmica via property binding: 
      ([routerLink]="['/cursos', idCurso.value]). 
      Nesse caso, o routerLink vai receber um array de parâmetros: 
      o primeiro valor é o nome da rota e sem seguida são passados os parâmetros da rota.
      
  app.component.html:

  ```
      <div>
          <a routerLink="">Logo aqui</a>
          <ul id="nav-mobile">
              <li routerLinkActive="active"><a [routerLink]="['/cursos', idCurso.value]">Curso com id</a></li>
          </ul>
      </div>
  ```

  3 - Obter o parâmetro no componente da rota com ActivatedRoute. (A melhor forma de fazer isso é dicutida no próximo item)
      Isso é útil para realizar alguma ação com o parâmetro, por exemplo: exibir na tela, fazer uma consulta, etc)
  curso-detalhe.component.ts:
  ```
      @Component({
          selector: 'app-curso-detalhe',
          templateUrl: './curso-detalhe.component.html',
          styleUrls: ['./curso-detalhe.component.css']
      })
      export class CursoDetalheComponent implements OnInit {
          id: string;

          constructor( private route: ActivatedRoute ){ 
              this.id = this.route.snapshot.params['id'];
          }

          ngOnInit(){

          }
      }
  ```

# Escutando mudanças nos parâmetros de roteamento
ActivateRoute possui o atributo params que é do tipo BehaviorSubject (RXJS). O valor é alterado a cada mudança de rota e nós podemos nos inscrever para sermos avisados quando a mudança ocorre.
Subject: age como Observable quando está escutando a mudança na rota e age como observer para notificar a mudança aos inscritos (substribers). A grosso modo, podemos dizer que o atributo params está sujeito ao comportamento (Behavior Subject) da rota.

O quadro abaixo tem um paraleto entre Observable e Subject

┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃         Observable                  ┃     BehaviorSubject/Subject         ┃      
┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╋━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┫ 
┃ Is just a function, no state        ┃ Has state. Stores data in memory    ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╋━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃ Code run for each observer          ┃ Same code run                       ┃
┃                                     ┃ only once for all observers         ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╋━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃ Creates only Observable             ┃Can create and also listen Observable┃
┃ ( data producer alone )             ┃ ( data producer and consumer )      ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╋━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃ Usage: Simple Observable with only  ┃ Usage:                              ┃
┃ one Obeserver.                      ┃ * Store data and modify frequently  ┃
┃                                     ┃ * Multiple observers listen to data ┃
┃                                     ┃ * Proxy between Observable  and     ┃
┃                                     ┃   Observer                          ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┻━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛

  Obtendo os parâmetros de roteamento:
  Para isso é necessário nos inscrevermos para ouvir as mudanças nos parametros passando a função de callback (arrow function)

  curso-detalhe.component.ts:
  ``` ...
      import { ActivatedRoute } from '@angular/router';
      import { Subscription } from 'rxjs/Rx';

      @Component({
          selector: 'app-curso-detalhe',
          templateUrl: './curso-detalhe.component.html',
          styleUrls: ['./curso-detalhe.component.css']
      })
      export class CursoDetalheComponent implements OnInit {
          id: string;
          inscricao: Subscription;

          constructor( private route: ActivatedRoute ){ 
          }

          ngOnInit(){
              this.inscricao = this.route.params.subscribe(
                  (params: any) => { this.id = params['id']; }                
              );
          }

          ngOnDestroy{
              this.inscricao.unsubscribe;
          }
      }
  ```
  * É uma boa prática colocar uma descrição no ngOnDestroy


# router.navigate: Rotas imperativas - Fazendo o redirecionamento via código
Exemplo: Dada uma lista de cursos, ao clicar em um curso redirecionar a rota para o detalhe do curso. No detalhe do curso, verificar se o  curso existe. Se sim mostra os detalhes do curso, senão redirecionar para outro componente (curso-nao-encontrado).

  cursos.service.ts: vai acessar o banco de dados e retornar uma lista de cursos

  cursos.compoente.html:
  ```
      <div>
          <a *ngFor="let curso of cursos" [routerLink]="['/curso', curso.id]"> 
              {{ curso.nome }} 
          </a>
      </div>
  ```

  cursos-detalhe.component.ts
  ```
      inscricao: Subscription,
      cursos: any;

      constructor(
          private route: ActivatedRoute,
          private router: Router,
          private cursosService: CursosService
      ){}

      ngOnInit(){
          this.inscricao = this.route.params.subscribe(
              (params: any) => {
                  this.id = params['id'];
                  this.curso = this.cursosService.getCurso(this.id);

                  // Roteamento imperativo
                  if (this.curso == null){
                      this.router.navigate(['/naoEncontrado']);

                  }
              }
          );
      }
  ```
# queryParams - Definir e extrair parâmetros de url

Útil para realizar paginação: localhost:4200/cursos?pagina=1



  1 - Passando um parâmetro para a URL:
  app.component.html:

  ```
      <div>
          <a routerLink="">Logo aqui</a>
          <ul id="nav-mobile">
              <li routerLinkActive="active"><a routerLink="/cursos" [queryParams]="{pagina:1">Curso com id</a></li>
          </ul>
      </div>
  ```

  2 - Extraindo parâmetros da URL:
  cursos.component.ts:
  ```
  import { ActivatedRoute, Router } from '@angular/router';
  import { Subscription } from 'rxjs/Rx';
  @Component({
      selector: 'app-cursos',
      templateUrl: './cursos.component.html',
      styleUrls: ['./cursos.component.css']

  })
  export class CursosComponent implements OnInit {
      cursos: any[];
      pagina: number;
      inscricao: Subscription;

      constructor(
          private cursosService: CursosService,
          private route: ActivateRoute,
          private router: Router // Para fazer a navegação imperativa
      ){ }

      ngOnInit(){
          this.cursos = this.cursosService.getCursos();
          this.inscricao = this.route.queryParams.subscribe( 
              (queryParams: any) => {
                  this.pagina = queryParams['pagina'];
              }
          )
      }

      ngOnDestroy(){
          this.inscricao.unsubscribe();
      }

      // Navegação imperativa usando queryParams
      proximaPagina(){
          this.router.navigate(
              ['/cursos'], 
              {queryParams: {'pagina': ++this.pagina} }
          );
      }


  }

  ```
  * queryParams, da mesma forma que params também é um BehaviorSubject    



