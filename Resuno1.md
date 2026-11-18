# **Resumo de DSW — conceitos, propriedades e sintaxe**

Este resumo reúne os principais conceitos que apareceram nos testes que enviaste. A ideia é perceberes **o que significa cada palavra, para que serve e como se escreve**, para conseguires responder mesmo quando o exercício muda os nomes das classes ou das variáveis.

# **1. C# — Classes, propriedades e objetos**

## **Classes e objetos**

Uma **classe** é um modelo que define as características e comportamentos de algo.

Um **objeto** é uma instância dessa classe.

```
public class Student
{
    public string Name { get; set; }
    public int Age { get; set; }

    public void Study()
    {
        Console.WriteLine("A estudar");
    }
}
```

- `Student` — nome da classe.
- `Name` e `Age` — propriedades.
- `Study()` — método.
- `string` e `int` — tipos de dados.
- `public` — permite acesso a partir de outras classes.

## **Propriedades mais comuns**

| Tipo       | Utilização          | Exemplo                                   |
| ---------- | ------------------- | ----------------------------------------- |
| `int`      | Números inteiros    | `public int Age { get; set; }`            |
| `string`   | Texto               | `public string Name { get; set; }`        |
| `decimal`  | Valores monetários  | `public decimal Price { get; set; }`      |
| `double`   | Números decimais    | `public double Average { get; set; }`     |
| `bool`     | Verdadeiro ou falso | `public bool Active { get; set; }`        |
| `DateTime` | Data e hora         | `public DateTime BirthDate { get; set; }` |
| `List<T>`  | Lista de objetos    | `public List<Order> Orders { get; set; }` |

### `get`**&#x20;e&#x20;**`set`

```
public string Name { get; set; }
```

- `get` — permite consultar o valor.
- `set` — permite alterar o valor.

Exemplo:

```
student.Name = "João";       // set
Console.WriteLine(student.Name); // get
```

## **Construtores**

Um construtor é executado quando criamos um objeto. Serve normalmente para inicializar os seus valores.

```
public class Student
{
    public string Name { get; set; }

    public Student(string name)
    {
        Name = name;
    }
}
```

Criação do objeto:

```
Student s = new Student("João");
```

## **Herança —&#x20;**`:`

Permite que uma classe herde propriedades e métodos de outra classe.

```
public class Person
{
    public string Name { get; set; }
}

public class Student : Person
{
    public int Number { get; set; }
}
```

`Student` herda de `Person`, pelo que também tem a propriedade `Name`.

### `base`

Utiliza-se para aceder à classe pai, por exemplo, ao chamar o seu construtor:

```
public Student(string name) : base(name)
{
}
```

### `virtual`**&#x20;e&#x20;**`override`

Permitem redefinir o comportamento de um método numa classe filha.

```
public class Animal
{
    public virtual void Speak()
    {
        Console.WriteLine("Som");
    }
}

public class Dog : Animal
{
    public override void Speak()
    {
        Console.WriteLine("Au au");
    }
}
```

- `virtual` — permite que o método seja redefinido.
- `override` — redefine o método herdado.

## **Inicialização de objetos**

Forma rápida de criar um objeto e atribuir propriedades:

```
Product p = new Product
{
    Name = "Keyboard",
    Stock = 50,
    Price = 19.99m
};
```

Repara que:

- `new Product` cria o objeto.
- `{ }` contém as propriedades a inicializar.
- `19.99m` indica um valor `decimal`.

## **Interpolação de strings**

Permite inserir variáveis diretamente num texto.

```
string name = "João";
int age = 20;

string message = $"O {name} tem {age} anos";
```

O `$` permite utilizar `{ }` para inserir variáveis.

## **Operadores importantes**

\| Operador | Significado | Exemplo |\
\|---|---|---|\
\| `??` | Valor alternativo se for `null` | `name ?? "Guest"` |\
\| `??=` | Atribui se for `null` | `name ??= "Guest"` |\
\| `?.` | Acede apenas se não for `null` | `user?.Email` |\
\| `==` | Igualdade | `age == 20` |\
\| `!=` | Diferente | `age != 20` |\
\| `&&` | E lógico | `age > 18 && active` |\
\| `||` | OU lógico | `age > 18 || active` |\
\| `=>` | Lambda | `x => x > 10` |

# **2. LINQ — trabalhar com listas**

LINQ permite pesquisar, filtrar, ordenar e transformar coleções de dados.

Imagina esta lista:

```
List<Product> products = GetProducts();
```

## **Métodos mais importantes**

| Método              | Para que serve             | Exemplo                                    |
| ------------------- | -------------------------- | ------------------------------------------ |
| `Where`             | Filtrar elementos          | `products.Where(p => p.Price > 10)`        |
| `Select`            | Escolher/transformar dados | `products.Select(p => p.Name)`             |
| `OrderBy`           | Ordenar crescente          | `products.OrderBy(p => p.Price)`           |
| `OrderByDescending` | Ordenar decrescente        | `products.OrderByDescending(p => p.Price)` |
| `GroupBy`           | Agrupar elementos          | `products.GroupBy(p => p.Category)`        |
| `Any`               | Verificar se existe algum  | `products.Any(p => p.Stock > 0)`           |
| `All`               | Verificar se todos cumprem | `products.All(p => p.Stock > 0)`           |
| `Take`              | Obter os primeiros N       | `products.Take(5)`                         |
| `Count`             | Contar elementos           | `products.Count()`                         |
| `Average`           | Calcular média             | `products.Average(p => p.Price)`           |
| `ToList`            | Converter para lista       | `products.ToList()`                        |

### **Exemplo prático**

Obter os produtos com stock superior a zero, ordenados pelo preço:

```
var available = products
    .Where(p => p.Stock > 0)
    .OrderBy(p => p.Price)
    .ToList();
```

### `Where`**&#x20;vs&#x20;**`Select`

- `Where` escolhe **quais os elementos** que queremos.
- `Select` escolhe **que informação queremos obter**.

```
// Produtos com preço superior a 20
products.Where(p => p.Price > 20);

// Apenas os nomes dos produtos
products.Select(p => p.Name);
```

### `Any`**&#x20;vs&#x20;**`All`

```
products.Any(p => p.Stock > 0);
```

Devolve `true` se pelo menos um produto tiver stock.

```
products.All(p => p.Stock > 0);
```

Devolve `true` se todos os produtos tiverem stock.

### `ToList`**&#x20;vs&#x20;**`Count`

- `ToList()` — cria uma lista com os resultados.
- `Count()` — devolve o número de elementos.

### **Execução diferida (Deferred Execution)**

Algumas operações LINQ, como `Where` e `Select`, só são executadas quando os resultados são percorridos ou materializados.

```
var result = products.Where(p => p.Stock > 0);

products.Add(new Product { Name = "Tablet", Stock = 10 });

var list = result.ToList();
```

O produto adicionado também pode aparecer nos resultados, porque a consulta ainda não tinha sido executada.

# **3. MVC — Model, View e Controller**

O padrão MVC divide a aplicação em três componentes.

**Model**

Dados e regras da aplicação

`Product`, `Student`, `Order`

**Controller**

Recebe pedidos e coordena a lógica

`ProductsController`

**View**

Apresenta os dados ao utilizador

`Index.cshtml`

## **Model**

Representa os dados.

```
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}
```

## **Controller**

Recebe pedidos e executa ações.

O nome termina normalmente em `Controller`.

```
public class ProductsController : Controller
{
    public IActionResult Index()
    {
        return View();
    }
}
```

- `ProductsController` — controlador.
- `Index()` — Action.
- `IActionResult` — tipo de resultado devolvido.
- `View()` — devolve uma View.

### **Rotas**

Por exemplo:

```
/Products/Details/7
```

| Parte      | Significado    |
| ---------- | -------------- |
| `Products` | Controller     |
| `Details`  | Action         |
| `7`        | Parâmetro `id` |

### **View**

É a página apresentada ao utilizador.

Por convenção, a View `Details` do controller `ProductsController` fica em:

```
Views/Products/Details.cshtml
```

### **Passar dados para a View**

**ViewBag:**

```
ViewBag.Message = "Olá";
```

Na View:

```
@ViewBag.Message
```

**ViewData:**

```
ViewData["Message"] = "Olá";
```

Na View:

```
@ViewData["Message"]
```

Ambos permitem passar informação do Controller para a View.

## **Razor**

Razor permite misturar C# com HTML em ficheiros `.cshtml`.

| Sintaxe         | Significado                  |
| --------------- | ---------------------------- |
| `@`             | Introduzir código C#         |
| `@Model`        | Aceder ao modelo             |
| `@Model.Name`   | Aceder a uma propriedade     |
| `@if`           | Condição                     |
| `@foreach`      | Ciclo                        |
| `@RenderBody()` | Conteúdo principal do Layout |
| `@section`      | Definir uma secção           |

Exemplo:

```
@model List<Product>

@foreach (var product in Model)
{
    <p>@product.Name</p>
}
```

### **Partial Views**

São partes reutilizáveis de uma página.

```
@model Product

<h2>@Model.Name</h2>
<p>@Model.Price</p>
```

### **Layout**

É uma estrutura comum às várias páginas, como cabeçalho, menu e rodapé.

`@RenderBody()` indica onde aparece o conteúdo específico de cada página.

### `[HttpPost]`

Identifica uma Action que recebe pedidos HTTP POST, normalmente usados para submeter formulários.

```
[HttpPost]
public IActionResult Create(Product product)
{
    return View();
}
```

### **Data Annotations**

Atributos usados para definir informações e validações nos modelos.

| Atributo                  | Significado                    |
| ------------------------- | ------------------------------ |
| `[Display(Name = "...")]` | Nome apresentado ao utilizador |
| `[EmailAddress]`          | Valida formato de email        |
| `[Required]`              | Campo obrigatório              |
| `[Authorize]`             | Exige autenticação/autorização |

# **4. Entity Framework Core (EF Core)**

É uma tecnologia que permite trabalhar com bases de dados através de classes C#.

## **DbContext**

Representa a ligação e sessão de trabalho com a base de dados.

```
public class ApplicationDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }
}
```

- `DbContext` — classe base do contexto.
- `DbSet<Product>` — representa o conjunto de produtos, normalmente associado a uma tabela.

## **Chaves primárias e estrangeiras**

**Primary Key (PK):** identifica unicamente um registo.

```
public int Id { get; set; }
```

**Foreign Key (FK):** referencia um registo de outra tabela.

```
public int CustomerId { get; set; }
```

## **Relações entre tabelas**

### **Um para muitos (1:N)**

Um cliente pode ter várias encomendas, mas cada encomenda pertence a um cliente.

**Customer**

`Id` (PK)

`Name`

1 para N

**Order**

`Id` (PK)

`Total`

`CustomerId` (FK)

Exemplo:

```
public class Customer
{
    public int Id { get; set; }
    public string Name { get; set; }

    public List<Order> Orders { get; set; }
}

public class Order
{
    public int Id { get; set; }
    public decimal Total { get; set; }

    public int CustomerId { get; set; }
    public Customer Customer { get; set; }
}
```

**Como distinguir:**

- `CustomerId` — chave estrangeira.
- `Customer` — propriedade de navegação para um cliente.
- `Orders` — coleção de encomendas.

## `Include`

Permite carregar dados relacionados.

```
var orders = context.Orders
    .Include(o => o.Customer)
    .ToList();
```

Sem `Include`, não deves assumir que os dados relacionados estão carregados.

## **Migrations**

Permitem atualizar a estrutura da base de dados quando alteramos os modelos.

| Comando                                  | Função                  |
| ---------------------------------------- | ----------------------- |
| `dotnet ef migrations add InitialCreate` | Criar migration         |
| `dotnet ef database update`              | Aplicar migrations à BD |

### **Code First vs Database First**

- **Code First:** começamos pelas classes C# e geramos a estrutura da base de dados.
- **Database First:** começamos pela base de dados e geramos as classes a partir dela.

# **5. ASP.NET Identity e autorização**

É utilizado para gerir utilizadores, autenticação e permissões.

| Elemento           | Função                          |
| ------------------ | ------------------------------- |
| `IdentityUser`     | Representa um utilizador        |
| `IdentityRole`     | Representa um papel/função      |
| `UserManager`      | Gere utilizadores               |
| `RoleManager`      | Gere funções                    |
| `[Authorize]`      | Restringe acesso                |
| `[AllowAnonymous]` | Permite acesso sem autenticação |

### **Exemplos**

```
[Authorize]
public IActionResult Profile()
{
    return View();
}
```

Só utilizadores autenticados podem aceder.

```
[Authorize(Roles = "Admin")]
public IActionResult AdminPanel()
{
    return View();
}
```

Só utilizadores com a função `Admin` podem aceder.

```
[AllowAnonymous]
public IActionResult Index()
{
    return View();
}
```

Qualquer pessoa pode aceder.

# **6. Decora estas diferenças para o teste**

| Se aparecer...      | Deves pensar em...             |
| ------------------- | ------------------------------ |
| `get; set;`         | Propriedade                    |
| `public Student()`  | Construtor                     |
| `: Person`          | Herança                        |
| `base(...)`         | Construtor da classe pai       |
| `virtual`           | Método que pode ser redefinido |
| `override`          | Redefinir método herdado       |
| `new Product { }`   | Inicializador de objeto        |
| `x => x.Price > 10` | Lambda                         |
| `Where`             | Filtrar                        |
| `Select`            | Selecionar propriedades        |
| `OrderBy`           | Ordenar crescente              |
| `Any`               | Existe algum?                  |
| `All`               | Todos cumprem?                 |
| `ToList`            | Converter para lista           |
| `Controller`        | Receber e tratar pedidos       |
| `IActionResult`     | Resultado de uma Action        |
| `View()`            | Devolver uma View              |
| `.cshtml`           | Ficheiro Razor                 |
| `@Model`            | Modelo na View                 |
| `@RenderBody()`     | Conteúdo do Layout             |
| `DbContext`         | Contexto da BD                 |
| `DbSet`             | Conjunto/tabela                |
| `Id`                | Chave primária convencional    |
| `CustomerId`        | Possível chave estrangeira     |
| `Include`           | Carregar dados relacionados    |
| `Migration`         | Alteração da estrutura da BD   |
| `[Authorize]`       | Restringir acesso              |
| `[HttpPost]`        | Pedido POST                    |

## **7. O que deves saber mesmo bem**

Se tiveres pouco tempo para estudar, dá prioridade a estes pontos:

1. **C#:** propriedades, construtores, herança, `base`, `virtual`, `override` e inicialização de objetos.
2. **LINQ:** saber distinguir e utilizar `Where`, `Select`, `OrderBy`, `Any`, `All`, `Take` e `ToList`.
3. **MVC:** saber identificar Model, View, Controller, Action, rotas e caminhos das Views.
4. **Razor:** conhecer `@Model`, `@foreach`, `@if`, `ViewBag`, `ViewData` e `@RenderBody()`.
5. **EF Core:** perceber `DbContext`, `DbSet`, PK, FK, relações 1:N, `Include` e migrations.
6. **Identity:** distinguir `[Authorize]`, `[AllowAnonymous]`, `IdentityUser` e `IdentityRole`.

**A minha recomendação:** não tentes decorar os exemplos palavra por palavra. Decora o significado de cada elemento e pratica a leitura de código. No teste podem trocar `Product` por `Student`, `Customer` por `Teacher`, ou `Price` por `Age`, mas a lógica é exatamente a mesma.
