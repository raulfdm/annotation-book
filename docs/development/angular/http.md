# Requisições HTTP

Para fazer requisições HTTP, usamos o modulo `HttpClient` do próprio Angular. Porém, precisamos fazer algumas configurações:

1.  Importar o `HttpClientModule` no módulo principal da aplicação:

    ```ts
    //.. Código omitido

    import { HttpClientModule } from '@angular/common/http';

    @NgModule({
      declarations: [AppComponent],
      imports: [BrowserModule, HttpClientModule],
      providers: [],
      bootstrap: [AppComponent]
    })
    export class AppModule {}
    ```

1.  No modulo/component que a gente que usar o http agora, precisamos fazer uma injeção de dependencia do `HttpClient`:

    ```ts
    //.. Código omitido

    export class AppComponent {
      constructor(http: HttpClient) {
        //disponível no contexto
      }
    }
    ```
