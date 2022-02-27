# 2.13

loadChildren: para carregar a rota de um módulo específico
{
path: "categories",
loadChildren: "./pages/categories/categories.module#CategoriesModule",
},

- path: src\app\app-routing.module.ts

# 2.14

routerLinkActive="active"

- Mostra qual opção do menu está ativa

      <li class="nav-item" routerLinkActive="active">
        <a class="nav-link" routerLink="/categories">Categorias</a>
      </li>

- path: src\app\app.component.html

# 2.32

1.  [class.active]:Deixa o botão selecionado 'aceso'

        <div class="btn-group">
          <label
            (click)="entryForm.get('paid').setValue(true)"
            [class.active]="entryForm.get('paid').value == true"
            class="btn btn-outline-info"
            >Pago</label
          >
          <label
            (click)="entryForm.get('paid').setValue(false)"
            [class.active]="entryForm.get('paid').value == false"
            class="btn btn-outline-info"
            >Pendente</label
          >
        </div>

- path: src\app\pages\entries\entry-form\entry-form.component.html

# 3.41 Criando uma arquitetura

1. Pasta/Módulo core: src\app\core

- Componentes, serviços, etc que são obrigatórios para o funcionamento do nosso sistema.
  Exemplo: navbar

- O CoreModule exporta os módulos e componentes obrigatórios. Além disso, declara os componentes obrigatórios
- O AppModule vai importar o CoreModule

2. Pasta/módulo shared: src\app\shared

- Componentes, serviços, models, etc que podem ser compartilhados, mas não são obrigatórios
  Exemplo: breadcrumb

- O SharedModule exporta os módulos e componentes não obrigatórios. Além disso, declara os componentes não obrigatórios
- Os módulos da pasta page (ex: CategoriesModule) vão importar o SharedModule

# 3.45 Injector (Injetor de dependência)

1. Nesse projeto, o Injector foi usado para que tenha uma única instância do HttpClient:

protected http: HttpClient;

constructor(
protected apiPath: string,
protected injector: Injector,
protected jsonDataToResourceFn: (jsonData: any) => T
){
this.http = injector.get(HttpClient);  
 }

- path: src\app\shared\services\base-resource.service.ts

- 1.1

- Na classe filha, fica dessa forma:
  constructor(protected injector: Injector) {
  super("api/categories", injector, Category.fromJson);
  }

- path: src\app\pages\categories\shared\category.service.ts

# 3.48 Passando o método 'jsonDataToResource' como parâmetro para o BaseResourceService

1. Passar o nome da função sem os () não executa a função. Nesse caso, estamos apenas dizendo que
   é essa função que deverá ser executada quando for solicitado:
   - Exemplo: Entry.fromJson

Parâmetro no construtor:

- protected jsonDataToResourceFn: (jsonData: any) => T // Converte o jsonData para o tipo T
- path: src\app\shared\services\base-resource.service.ts

Uso na classe filha (3rd parâmetro):

- super("api/entries", injector, Entry.fromJson);

2. this
   getAll(): Observable<T[]> {
   return this.http.get(this.apiPath).pipe(
   map(this.jsonDataToResources.bind(this)), // bind(this): Esse this se refere à classe que está sendo instanciada ao chamar esse método
   catchError(this.handleError)
   );
   }

- path: src\app\shared\services\base-resource.service.ts

# 3.64 Adicionando o template da tela de relatórios

<!-- hr: para separar -->
<hr />

<!-- No card-deck, os cards inseridos se adaptam para a largura total -->
<div class="card-deck mt-5 mb-5">

- path: src\app\pages\reports\reports\reports.component.html
