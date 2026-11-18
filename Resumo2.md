# Folha de apoio — DSW (Desenvolvimento de Sistemas Web)

## 1. C# — Classes e programação orientada a objetos

### 1.1. Estrutura de uma classe

Uma classe representa um objeto. Contém propriedades (características) e métodos (ações).

```csharp
public class Student
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }

    public void Study()
    {
        Console.WriteLine("A estudar");
    }
}
```

**O que significa cada elemento?**

- `public`: pode ser acedido a partir de outras classes.
- `class`: declaração de uma classe.
- `Student`: nome da classe.
- `int`, `string`, `decimal`, `bool`: tipos de dados.
- `Id`, `Name`, `Age`: propriedades.
- `Study()`: método.
- `get`: permite obter o valor.
- `set`: permite alterar o valor.

### 1.2. Tipos de propriedades mais comuns

| Tipo | Utilização | Exemplo |
|---|---|---|
| `int` | Número inteiro | `Age`, `Id`, `Stock` |
| `string` | Texto | `Name`, `Email`, `PhoneNumber` |
| `decimal` | Valores monetários | `Price`, `Total` |
| `double` | Valores decimais | `Average` |
| `bool` | Verdadeiro/falso | `IsActive`, `IsPaid` |
| `DateTime` | Data e hora | `BirthDate`, `OrderDate` |
| `List<T>` | Lista de objetos | `List<Order>` |

**Nomes de propriedades que deves reconhecer:**

| Nome | Significado |
|---|---|
| `Id` | Identificador |
| `FirstName` | Primeiro nome |
| `LastName` | Apelido |
| `FullName` | Nome completo |
| `Email` | Email |
| `PhoneNumber` | Número de telefone |
| `Address` | Morada |
| `City` | Cidade |
| `BirthDate` | Data de nascimento |
| `Price` | Preço |
| `Stock` | Stock |
| `Quantity` | Quantidade |
| `Description` | Descrição |
| `CategoryId` | Identificador da categoria |
| `CustomerId` | Identificador do cliente |
| `CreatedAt` | Data de criação |
| `IsActive` | Está ativo? |
| `IsPaid` | Está pago? |
| `IsAvailable` | Está disponível? |

**Dica:** propriedades começadas por `Is` representam normalmente valores `bool`. Propriedades terminadas em `Id` são frequentemente identificadores.

### 1.3. Construtores

Um construtor é executado quando criamos um objeto. Tem o mesmo nome da classe e não tem tipo de retorno.

```csharp
public class Student
{
    public string Name { get; set; }

    public Student(string name)
    {
        Name = name;
    }
}
```

Criar um objeto:

```csharp
Student s = new Student("João");
```

**Se o exercício pedir um construtor**, utiliza:

```csharp
public NomeDaClasse(parâmetros)
{
    Propriedade = parâmetro;
}
```

### 1.4. Herança

Uma classe pode herdar propriedades e métodos de outra classe.

```csharp
public class Person
{
    public string Name { get; set; }
}

public class Student : Person
{
    public int StudentNumber { get; set; }
}
```

`Student : Person` significa que Student herda de Person.

**`base`** permite chamar o construtor da classe pai:

```csharp
public Student(string name, int number) : base(name)
{
    StudentNumber = number;
}
```

### 1.5. Polimorfismo — virtual e override

- `virtual`: permite redefinir um método numa classe derivada.
- `override`: redefine o método herdado.
- `base`: permite chamar a implementação da classe pai.

```csharp
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

### 1.6. Inicializadores de objetos

Se pedirem para criar um objeto e atribuir várias propriedades:

```csharp
Product product = new Product
{
    Name = "Keyboard",
    Stock = 50,
    Price = 19.99m
};
```

Atenção: utiliza `new Product { ... }`, não `new Product( Name = ... )`.

### 1.7. Interpolação de strings

Permite colocar variáveis diretamente numa string, usando `$`.

```csharp
string name = "João";
int age = 20;

string message = $"Nome: {name}, Idade: {age}";
```

Alternativa com `string.Format`:

```csharp
string message = string.Format("Nome: {0}, Idade: {1}", name, age);
```

### 1.8. Operadores importantes

| Operador | Significado | Exemplo |
|---|---|---|
| `??` | Valor alternativo se for null | `name ?? "Guest"` |
| `??=` | Atribui apenas se for null | `name ??= "Guest"` |
| `?.` | Acede se não for null | `user?.Email` |
| `==` | Igual | `age == 18` |
| `!=` | Diferente | `age != 18` |
| `&&` | E | `age > 18 && active` |
| `||` | OU | `age > 18 || active` |
| `=>` | Lambda | `x => x > 10` |

Exemplo de acesso seguro a propriedades:

```csharp
string city = person?.Address?.City;
```

Se `person` ou `Address` forem null, o resultado será null em vez de tentar aceder à propriedade seguinte.

### 1.9. Lambda expressions

Uma lambda representa uma função de forma curta.

```csharp
product => product.Price > 100
```

Significa: recebe um produto e verifica se o preço é superior a 100.

Equivalente a uma função:

```csharp
bool IsExpensive(Product product)
{
    return product.Price > 100;
}
```

### 1.10. Extension Methods

Permitem adicionar métodos a um tipo existente sem modificar a classe original.

```csharp
public static class StatusExtensions
{
    public static string GetDescription(this TaskStatus status)
    {
        return status == TaskStatus.Pending
            ? "Pendente"
            : "Concluída";
    }
}
```

Pontos importantes:
- A classe deve ser `static`.
- O método deve ser `static`.
- O primeiro parâmetro começa por `this`.
- `this TaskStatus status` indica o tipo ao qual o método pode ser aplicado.

---

## 2. LINQ — Consultas a listas

LINQ permite filtrar, ordenar, selecionar e agrupar elementos.

Imagina que existe:

```csharp
List<Product> products = GetProducts();
```

### 2.1. Métodos fundamentais

| Método | Função | Exemplo |
|---|---|---|
| `Where` | Filtrar | `products.Where(p => p.Price > 10)` |
| `Select` | Selecionar informação | `products.Select(p => p.Name)` |
| `OrderBy` | Ordenar crescente | `products.OrderBy(p => p.Price)` |
| `OrderByDescending` | Ordenar decrescente | `products.OrderByDescending(p => p.Price)` |
| `GroupBy` | Agrupar | `products.GroupBy(p => p.Category)` |
| `Any` | Verificar se existe algum | `products.Any(p => p.Stock > 0)` |
| `All` | Verificar se todos cumprem | `products.All(p => p.Stock > 0)` |
| `Take` | Obter os primeiros N | `products.Take(5)` |
| `Count` | Contar elementos | `products.Count()` |
| `Average` | Calcular média | `products.Average(p => p.Price)` |
| `ToList` | Criar uma lista | `products.ToList()` |

### 2.2. Perceber Where e Select

**Where = escolher os elementos que cumprem uma condição.**

```csharp
var result = products.Where(p => p.Stock > 0);
```

Devolve produtos com stock superior a zero.

**Select = escolher que informação queremos obter.**

```csharp
var result = products.Select(p => p.Name);
```

Devolve apenas os nomes dos produtos.

**Combinar os dois:**

```csharp
var result = products
    .Where(p => p.Stock > 0)
    .Select(p => p.Name);
```

Devolve os nomes dos produtos que têm stock.

### 2.3. Ordenar resultados

Crescente:

```csharp
var result = products.OrderBy(p => p.Price);
```

Decrescente:

```csharp
var result = products.OrderByDescending(p => p.Price);
```

### 2.4. Any e All

```csharp
products.Any(p => p.Stock > 0);
```

Devolve `true` se pelo menos um produto tiver stock.

```csharp
products.All(p => p.Stock > 0);
```

Devolve `true` se todos os produtos tiverem stock.

### 2.5. Converter um foreach para LINQ

Código original:

```csharp
var available = new List<Product>();

foreach (var p in products)
{
    if (p.Stock > 0)
    {
        available.Add(p);
    }
}
```

Com LINQ:

```csharp
var available = products
    .Where(p => p.Stock > 0)
    .ToList();
```

**Como resolver este tipo de exercício:**

1. Identificar a lista.
2. Identificar a condição do `if`.
3. Utilizar `Where` para filtrar.
4. Utilizar `ToList()` se pedirem uma lista.

### 2.6. Query Syntax e Method Syntax

Query Syntax:

```csharp
var result =
    from p in products
    where p.Stock > 0
    select p.Name;
```

Method Syntax:

```csharp
var result = products
    .Where(p => p.Stock > 0)
    .Select(p => p.Name);
```

Correspondências:

| Query Syntax | Method Syntax |
|---|---|
| `from p in products` | `products` |
| `where condição` | `.Where(p => condição)` |
| `select p.Name` | `.Select(p => p.Name)` |
| `orderby p.Price` | `.OrderBy(p => p.Price)` |

### 2.7. Execução diferida (Deferred Execution)

`Where` e `Select` normalmente não executam imediatamente a consulta.

```csharp
var result = products.Where(p => p.Stock > 0);

products.Add(new Product { Name = "Tablet", Stock = 10 });

var list = result.ToList();
```

O produto Tablet também pode aparecer porque a consulta só é executada quando é percorrida ou convertida em lista.

- `ToList()`: materializa os resultados numa lista.
- `Count()`: executa a consulta e devolve a quantidade de elementos.

---

## 3. MVC e Razor

### 3.1. O que é MVC?

| Componente | Função |
|---|---|
| Model | Representa os dados |
| View | Apresenta os dados |
| Controller | Recebe pedidos e coordena a aplicação |

Exemplo:
- Model: `Product`
- Controller: `ProductsController`
- View: `Index.cshtml`

### 3.2. Controller

O nome de um controller termina em `Controller`.

```csharp
public class ProductsController : Controller
{
    public IActionResult Index()
    {
        return View();
    }
}
```

- `ProductsController`: nome do controller.
- `Index`: nome da Action.
- `IActionResult`: tipo de resultado.
- `View()`: devolve uma View.

**Se pedirem o nome do controller para Products:**

```csharp
ProductsController
```

### 3.3. Rotas

Exemplo:

```text
/Products/Details/7
```

| Elemento | Significado |
|---|---|
| `Products` | Controller |
| `Details` | Action |
| `7` | Parâmetro id |

### 3.4. Localização das Views

A estrutura segue normalmente esta convenção:

```text
Views/
    Products/
        Index.cshtml
        Details.cshtml
        Create.cshtml
```

Se o exercício pedir a localização da View `Details` do controller `ProductsController`:

```text
Views/Products/Details.cshtml
```

### 3.5. Actions

Uma Action é um método público de um Controller.

Exemplo: devolver um produto pelo seu identificador.

```csharp
public IActionResult Details(int id)
{
    var product = GetProduct(id);
    return View(product);
}
```

Estrutura a memorizar:

```csharp
public IActionResult NomeDaAction(int id)
{
    var objeto = ObterObjeto(id);
    return View(objeto);
}
```

### 3.6. ViewBag e ViewData

Permitem passar dados do Controller para a View.

**ViewBag:**

```csharp
ViewBag.Message = "Olá";
```

Na View:

```cshtml
@ViewBag.Message
```

**ViewData:**

```csharp
ViewData["Message"] = "Olá";
```

Na View:

```cshtml
@ViewData["Message"]
```

### 3.7. Razor

Razor permite escrever C# dentro de ficheiros `.cshtml`.

| Sintaxe | Utilização |
|---|---|
| `@` | Introduzir código C# |
| `@model` | Declarar o tipo do modelo |
| `@Model` | Aceder ao modelo |
| `@Model.Name` | Aceder a uma propriedade |
| `@if` | Condição |
| `@foreach` | Ciclo |
| `@RenderBody()` | Conteúdo principal do Layout |
| `@section` | Criar uma secção |

Exemplo:

```cshtml
@model List<Product>

@foreach (var product in Model)
{
    <p>@product.Name</p>
}
```

Exemplo com condição:

```cshtml
@if (Model.Any())
{
    <p>Existem produtos.</p>
}
else
{
    <p>Não existem produtos.</p>
}
```

### 3.8. Layout e Partial Views

**Layout:** estrutura comum das páginas, como cabeçalho, menu e rodapé.

```cshtml
<body>
    <header>Menu</header>

    @RenderBody()

    <footer>Rodapé</footer>
</body>
```

`@RenderBody()` indica onde aparece o conteúdo específico da página.

**Partial View:** parte de uma página que pode ser reutilizada.

```cshtml
@model Product

<h2>@Model.Name</h2>
<p>@Model.Price</p>
```

### 3.9. HttpPost

Identifica uma Action que recebe pedidos POST, normalmente utilizados para submeter formulários.

```csharp
[HttpPost]
public IActionResult Create(Product product)
{
    return View();
}
```

### 3.10. Data Annotations

Atributos utilizados para definir validações e nomes de apresentação.

```csharp
[Display(Name = "Nome completo")]
public string FullName { get; set; }

[EmailAddress]
public string Email { get; set; }
```

| Atributo | Função |
|---|---|
| `[Display(Name = "...")]` | Define o nome apresentado |
| `[EmailAddress]` | Valida o formato do email |
| `[Required]` | Campo obrigatório |

---

## 4. Entity Framework Core

### 4.1. DbContext e DbSet

`DbContext` representa o contexto de acesso à base de dados.

`DbSet<T>` representa um conjunto de entidades, normalmente associado a uma tabela.

```csharp
public class ApplicationDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }
    public DbSet<Customer> Customers { get; set; }
}
```

### 4.2. Chaves primárias e estrangeiras

**Primary Key (PK):** identifica um registo.

```csharp
public int Id { get; set; }
```

**Foreign Key (FK):** identifica o registo relacionado noutra tabela.

```csharp
public int CustomerId { get; set; }
```

Por convenção, o EF Core reconhece frequentemente propriedades chamadas `Id` ou `NomeDaClasseId` como chaves primárias.

### 4.3. Relação um para muitos (1:N)

Um cliente pode ter várias encomendas.

```csharp
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

Como interpretar:

- `Customer.Id`: chave primária do cliente.
- `Order.Id`: chave primária da encomenda.
- `Order.CustomerId`: chave estrangeira.
- `Order.Customer`: navegação para o cliente.
- `Customer.Orders`: lista de encomendas do cliente.

**Regra:** na relação 1:N, a FK fica normalmente na tabela do lado N.

### 4.4. Include

Utiliza-se para carregar dados relacionados.

```csharp
var orders = context.Orders
    .Include(o => o.Customer)
    .ToList();
```

Se pedirem para obter encomendas juntamente com os respetivos clientes, utiliza:

```csharp
.Include(o => o.Customer)
```

Exemplo com filtro:

```csharp
var orders = context.Orders
    .Include(o => o.Customer)
    .Where(o => o.Total > 100)
    .ToList();
```

### 4.5. Code First e Database First

- **Code First:** criar primeiro as classes C# e depois gerar a base de dados.
- **Database First:** partir de uma base de dados existente e gerar as classes.

### 4.6. Migrations

Servem para atualizar a estrutura da base de dados.

Criar uma migration:

```bash
dotnet ef migrations add InitialCreate
```

Aplicar alterações à base de dados:

```bash
dotnet ef database update
```

---

## 5. Identity e autorização

| Elemento | Função |
|---|---|
| `IdentityUser` | Representa um utilizador |
| `IdentityRole` | Representa uma função/papel |
| `UserManager` | Gere utilizadores |
| `RoleManager` | Gere funções |
| `[Authorize]` | Exige autorização |
| `[AllowAnonymous]` | Permite acesso sem autenticação |

Exemplos:

```csharp
[Authorize]
public IActionResult Profile()
{
    return View();
}
```

Exige utilizador autenticado.

```csharp
[Authorize(Roles = "Teacher")]
public IActionResult Grades()
{
    return View();
}
```

Exige a função Teacher.

```csharp
[Authorize(Roles = "Admin, Manager")]
public IActionResult Dashboard()
{
    return View();
}
```

Permite acesso a utilizadores com uma das funções indicadas.

```csharp
[AllowAnonymous]
public IActionResult Index()
{
    return View();
}
```

Permite acesso anónimo.

### Razor Pages

Uma Razor Page utiliza normalmente uma classe que herda de `PageModel`.

```csharp
public class IndexModel : PageModel
{
    public void OnGet()
    {
    }
}
```

`OnGet()` é um handler executado quando a página recebe um pedido GET.

---

## 6. Como interpretar os enunciados

| Se o exercício disser... | O que deves utilizar |
|---|---|
| Criar uma propriedade | `public tipo Nome { get; set; }` |
| Criar um construtor | Método com o nome da classe |
| Herdar de uma classe | `: NomeDaClasse` |
| Chamar o construtor pai | `: base(...)` |
| Redefinir um método | `override` |
| Permitir redefinição | `virtual` |
| Criar objeto com propriedades | `new Classe { ... }` |
| Substituir valor null | `??` |
| Atribuir apenas se null | `??=` |
| Aceder de forma segura | `?.` |
| Filtrar uma lista | `Where` |
| Obter determinadas propriedades | `Select` |
| Ordenar crescente | `OrderBy` |
| Ordenar decrescente | `OrderByDescending` |
| Verificar se existe algum | `Any` |
| Verificar se todos cumprem | `All` |
| Obter os primeiros elementos | `Take` |
| Converter em lista | `ToList` |
| Criar Controller | `NomeController` |
| Criar Action | `public IActionResult Nome()` |
| Devolver uma View | `return View()` |
| Enviar objeto para View | `return View(objeto)` |
| Passar dados simples para View | `ViewBag` ou `ViewData` |
| Criar formulário POST | `[HttpPost]` |
| Criar relação 1:N | `List<T>` e FK |
| Carregar dados relacionados | `Include` |
| Criar migration | `dotnet ef migrations add Nome` |
| Atualizar base de dados | `dotnet ef database update` |
| Restringir acesso | `[Authorize]` |
| Permitir acesso anónimo | `[AllowAnonymous]` |

---

## 7. Erros a evitar

1. C# distingue maiúsculas e minúsculas: `Name` não é igual a `name`.
2. Uma propriedade escreve-se com `{ get; set; }`.
3. Um método tem parênteses: `Study()`.
4. Um construtor tem o nome da classe e não tem tipo de retorno.
5. `virtual` permite redefinir; `override` redefine.
6. `Where` filtra; `Select` seleciona.
7. `Any` verifica se existe pelo menos um; `All` verifica se todos cumprem.
8. `ToList()` devolve uma lista; `Count()` devolve uma quantidade.
9. O caminho da View é `Views/Controller/Action.cshtml`.
10. `CustomerId` é uma propriedade escalar; `Customer` é uma propriedade de navegação.

---

## 8. Método para resolver qualquer exercício

Antes de escrever código:

1. **Identifica o tema:** C#, LINQ, MVC, EF Core ou Identity.
2. **Identifica o verbo:** criar, filtrar, ordenar, devolver, herdar, relacionar, validar.
3. **Identifica os nomes:** classe, propriedades, lista, parâmetros e condições.
4. **Escolhe a sintaxe:** consulta o padrão correspondente nesta folha.
5. **Confirma os detalhes:** maiúsculas, parênteses, tipos de dados, nomes e ponto e vírgula.

**Importante:** os nomes dos exemplos são apenas ilustrativos. Se o exercício utilizar `Student`, `Teacher`, `Book` ou `Order`, substitui os nomes mantendo a mesma lógica.
