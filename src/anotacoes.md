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
