# Resumão do Curso de Angular

Principais Tecnologias:
- Node.js (V8 engine Chrome)
- TypeScript
- Jamine / Karma
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

  
 

