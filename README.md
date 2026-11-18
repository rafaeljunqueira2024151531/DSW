# DSW — Guia para resolver os exercícios dos testes A, B, C e D

## PARTE 1 — C# / Programação Orientada a Objetos

### Exercício 1 — Construtor com herança e `base`

**Como reconhecer:** o enunciado diz que uma classe herda de outra e pede o cabeçalho do construtor, inicializando propriedades da classe pai.

**O que fazer:**
1. Escrever `public`.
2. Escrever o nome da classe filha.
3. Colocar os parâmetros pedidos.
4. Usar `: base(...)` com o parâmetro que pertence à classe pai.

**Modelo:**

```csharp
public NomeFilho(string nome, int numero) : base(nome)
```

Exemplo:

```csharp
public Car(string brand, int year) : base(brand)
```

`brand` é enviado ao construtor da classe pai; `year` será utilizado na classe filha.

---

### Exercício 2 — Descobrir o resultado de `virtual` e `override`

**Como reconhecer:** aparecem duas classes, uma herda da outra, e o enunciado pergunta o que imprime.

**O que fazer:**
1. Verificar se o método da classe pai é `virtual`.
2. Verificar se a classe filha tem `override`.
3. Verificar o tipo do objeto criado com `new`.
4. Se existir `override`, é executada a versão da classe do objeto real.

Exemplo:

```csharp
class Animal
{
    public virtual string Speak() => "Animal";
}

class Dog : Animal
{
    public override string Speak() => "Dog";
}

Animal a = new Dog();
Console.WriteLine(a.Speak());
```

**Resposta:** `Dog`

Atenção: o tipo da variável (`Animal`) não determina sozinho o método executado. Conta o tipo real do objeto (`Dog`).

Se a classe filha não tiver `override`, é executada a versão herdada.

Se utilizar `base.Speak()`, está a chamar a implementação da classe pai.

---

### Exercício 3 — Converter uma propriedade para auto-property

**Como reconhecer:** aparece uma propriedade com uma variável privada (`_name`, `_age`, `_salary`) e métodos `get` e `set`.

**O que fazer:** substituir tudo por uma propriedade automática.

**Modelo:**

```csharp
public TIPO Nome { get; set; }
```

Exemplos:

```csharp
public string Name { get; set; }

public int Age { get; set; }

public decimal Salary { get; set; }
```

Não precisas da variável privada `_name`.

---

### Exercício 4 — Inicialização de objetos

**Como reconhecer:** aparecem várias instruções a criar um objeto e atribuir propriedades separadamente.

Código original:

```csharp
Product product = new Product();
product.Name = "Keyboard";
product.Stock = 50;
product.Price = 19.99m;
```

**O que fazer:** juntar as atribuições dentro de `{ }`, logo depois de `new Product`.

**Modelo:**

```csharp
var objeto = new Classe
{
    Propriedade1 = valor1,
    Propriedade2 = valor2
};
```

Resultado:

```csharp
var product = new Product
{
    Name = "Keyboard",
    Stock = 50,
    Price = 19.99m
};
```

Atenção: utiliza `new Product { ... }`, não `new Product( ... )`.

---

### Exercício 5 — Interpolated String

**Como reconhecer:** aparece `string.Format` ou concatenação de strings com `+` e o enunciado pede interpolated string.

**O que fazer:** colocar `$` antes das aspas e substituir os marcadores pelas variáveis entre `{ }`.

Exemplo original:

```csharp
string.Format("{0} ({1} pages)", title, pages)
```

Resultado:

```csharp
$"{title} ({pages} pages)"
```

Outro exemplo:

```csharp
"Olá " + name + ", tens " + age + " anos"
```

Resultado:

```csharp
$"Olá {name}, tens {age} anos"
```

---

### Exercício 6 — Operadores `??`, `??=` e `?.`

**Como reconhecer:** aparece um `if` a verificar se uma variável é `null`.

**A) Operador `??`**

Se o exercício disser que deve utilizar um valor alternativo quando a variável é null:

```csharp
displayName = name ?? "Sem nome";
```

Equivale a:

```csharp
if (name == null)
    displayName = "Sem nome";
else
    displayName = name;
```

**B) Operador `??=`**

Se disser para atribuir um valor apenas quando a variável é null:

```csharp
token ??= "default-token";
```

Equivale a:

```csharp
if (token == null)
    token = "default-token";
```

**C) Operador `?.`**

Se disser para evitar `NullReferenceException` ao aceder a propriedades:

```csharp
city = person?.Address?.City;
```

Equivale a verificar se `person` e `Address` não são null antes de aceder a `City`.

Se existir apenas uma propriedade:

```csharp
string email = user?.Email;
```

---

### Exercício 7 — Método de extensão para um enum

**Como reconhecer:** aparece um `enum`, normalmente com dois valores, e pedem um método que devolva descrições em português.

**O que fazer:**
1. Criar um método `public static`.
2. Definir o tipo de retorno, normalmente `string`.
3. Colocar `this` antes do tipo do enum.
4. Comparar o valor com `==`.
5. Utilizar o operador ternário `? :`.

**Modelo:**

```csharp
public static string ToPortuguese(this NOME_ENUM status)
{
    return status == NOME_ENUM.VALOR1
        ? "Descrição 1"
        : "Descrição 2";
}
```

Exemplo:

```csharp
public static string ToPortuguese(this PaymentStatus status)
{
    return status == PaymentStatus.Pending
        ? "Pendente"
        : "Pago";
}
```

---

### Exercício 8 — Converter um método em lambda

**Como reconhecer:** aparece um método com `return` e pedem uma expressão lambda equivalente.

**O que fazer:** utilizar os parâmetros antes de `=>` e a expressão devolvida depois de `=>`.

Exemplo original:

```csharp
private bool IsAdult(User user)
{
    return user.Age >= 18;
}
```

Resultado:

```csharp
user => user.Age >= 18
```

Se não tiver parâmetros:

```csharp
public int GenerateKey()
{
    return 42;
}
```

Resultado:

```csharp
() => 42
```

Se tiver uma condição com `&&`, mantém a condição completa:

```csharp
user => !string.IsNullOrWhiteSpace(user.Email)
        && user.Email.Contains("@example.com")
```

---

## PARTE 2 — LINQ

### Exercício 9 — Execução diferida ou imediata

**Como reconhecer:** perguntam se `Where`, `Select`, `Count` ou `ToList` executam imediatamente.

Decora:

| Operação | Tipo |
|---|---|
| `Where` | Diferida |
| `Select` | Diferida |
| `OrderBy` | Diferida |
| `GroupBy` | Diferida |
| `Count()` | Imediata |
| `ToList()` | Imediata |
| `Average()` | Imediata |
| `Any()` | Imediata |
| `All()` | Imediata |

**Regra:** as consultas são normalmente diferidas até serem percorridas ou executadas por uma operação que necessita dos resultados.

Se o enunciado disser que foi adicionado um elemento à lista antes do `foreach` e esse elemento aparece, a resposta é:

`Execução diferida`

---

### Exercício 10 — Converter Query Syntax para Method Syntax

**Como reconhecer:** aparece uma consulta com `from`, `where` e `select`.

Exemplo:

```csharp
from p in products
where p.Price < 10
select p.Name
```

**Conversão:**

| Query Syntax | Method Syntax |
|---|---|
| `from p in products` | `products` |
| `where p.Price < 10` | `.Where(p => p.Price < 10)` |
| `select p.Name` | `.Select(p => p.Name)` |

Resultado:

```csharp
products
    .Where(p => p.Price < 10)
    .Select(p => p.Name)
```

**Fórmula para decorar:**

```csharp
lista.Where(x => CONDIÇÃO).Select(x => PROPRIEDADE)
```

Se não houver `select`, não inventes um `Select`.

---

### Exercício 11 — Converter foreach para LINQ

**Como reconhecer:** aparece uma lista vazia, um `foreach`, um `if` e um `Add`.

Exemplo:

```csharp
var paid = new List<Order>();

foreach (var o in orders)
{
    if (o.IsPaid)
        paid.Add(o);
}
```

**O que fazer:**
1. Identificar a lista original: `orders`.
2. Identificar a condição do `if`: `o.IsPaid`.
3. Utilizar `Where` para filtrar.
4. Utilizar `ToList()` para criar a lista final.

**Fórmula:**

```csharp
var resultado = lista.Where(x => CONDIÇÃO).ToList();
```

Resultado:

```csharp
var paid = orders.Where(o => o.IsPaid).ToList();
```

Outro exemplo:

```csharp
var dept = employees
    .Where(e => e.Department == "IT")
    .ToList();
```

**Atenção:** se o exercício disser que não deve existir projeção e que devem ser devolvidos os elementos originais, não utilizes `Select`.

---

### Exercício 12 — Consulta LINQ com filtro, ordenação e projeção

**Como reconhecer:** o enunciado pede:
- elementos que cumpram uma condição;
- ordenação crescente ou decrescente;
- um objeto anónimo com determinadas propriedades.

**O que fazer:**

1. `Where` para filtrar.
2. `OrderBy` ou `OrderByDescending` para ordenar.
3. `Select` para escolher as propriedades.

**Fórmula:**

```csharp
lista
    .Where(x => CONDIÇÃO)
    .OrderBy(x => x.PROPRIEDADE)
    .Select(x => new { x.Propriedade1, x.Propriedade2 })
```

Para ordem decrescente:

```csharp
.OrderByDescending(x => x.Propriedade)
```

Exemplo:

```csharp
students
    .Where(s => s.Grade >= 14)
    .OrderByDescending(s => s.Grade)
    .Select(s => new { s.Name, s.Grade })
```

Se pedirem um texto no formato `"Name: TotalSpent"`:

```csharp
.Select(c => $"{c.Name}: {c.TotalSpent}")
```

---

### Exercício 13 — Identificar o método LINQ correto

| O que o enunciado pede | Método |
|---|---|
| Filtrar elementos | `Where` |
| Selecionar propriedades | `Select` |
| Ordenar crescente | `OrderBy` |
| Ordenar decrescente | `OrderByDescending` |
| Agrupar | `GroupBy` |
| Verificar se existe pelo menos um | `Any` |
| Verificar se todos cumprem | `All` |
| Obter os primeiros N | `Take` |
| Contar elementos | `Count` |
| Calcular média | `Average` |
| Criar uma lista | `ToList` |

Exemplos:

```csharp
users.Any(u => u.IsActive);
```

Existe pelo menos um utilizador ativo?

```csharp
users.All(u => u.IsActive);
```

Todos os utilizadores estão ativos?

```csharp
products.Take(5);
```

Obter os primeiros cinco produtos.

---

## PARTE 3 — MVC / Razor

### Exercício 14 — Nome de um Controller

**Como reconhecer:** pedem o nome do controlador responsável por determinada entidade.

**Regra:** nome da entidade no plural ou nome indicado no enunciado + `Controller`.

Exemplos:

| Entidade | Controller |
|---|---|
| Users | `UsersController` |
| Products | `ProductsController` |
| Orders | `OrdersController` |
| Home | `HomeController` |
| Account | `AccountController` |

---

### Exercício 15 — Papel do Routing e do Controller

**Como reconhecer:** perguntam pelo ciclo de vida de um pedido MVC.

Decora esta sequência:

1. O pedido HTTP chega ao servidor.
2. **Routing** identifica o Controller e a Action.
3. O Controller executa a Action correspondente.
4. A Action pode obter dados e devolver uma View.
5. O motor de Views renderiza a View para HTML.
6. A resposta é enviada ao navegador.

Perguntas típicas:

- Primeiro componente que decide Controller e Action: `Routing`.
- Papel do Controller: executar a Action e devolver uma resposta.
- Último passo antes da resposta chegar ao navegador: renderização da View.

**Porque se separa Controller de View?**

Para separar a lógica da apresentação, facilitando a manutenção e os testes.

---

### Exercício 16 — Interpretar uma rota

**Como reconhecer:** aparece um URL com parâmetros entre `{ }` e pedem Controller, Action e valores.

Exemplo:

```text
/admin/Users/Edit/3
```

Rota:

```text
admin/{controller}/{action}/{id}
```

**O que fazer:** comparar cada parte do URL com cada parâmetro da rota.

Resultado:

```text
Controller=Users, Action=Edit, id=3
```

Outro exemplo:

```text
/blog/2025/10
```

Rota:

```text
blog/{year}/{month}
```

Se os defaults indicarem:

```csharp
controller = "Blog"
action = "Archive"
```

Resultado:

```text
Controller=Blog, Action=Archive, year=2025, month=10
```

---

### Exercício 17 — Características de uma Action

**Como reconhecer:** perguntam o que é necessário para um método ser uma Action de um Controller MVC.

Resposta a memorizar:

- Deve ser `public`.
- Deve devolver `IActionResult` ou um tipo de resultado equivalente.

Exemplo:

```csharp
public IActionResult Index()
{
    return View();
}
```

---

### Exercício 18 — Caminho da View

**Como reconhecer:** dão o nome de um Controller e de uma Action e perguntam onde fica a View.

**Regra:**

```text
Views/NOME_DO_CONTROLLER/NOME_DA_ACTION.cshtml
```

Exemplos:

| Controller | Action | Caminho |
|---|---|---|
| `ProductsController` | `Index` | `Views/Products/Index.cshtml` |
| `OrdersController` | `Edit` | `Views/Orders/Edit.cshtml` |
| `HomeController` | `Index` | `Views/Home/Index.cshtml` |
| `AccountController` | `Login` | `Views/Account/Login.cshtml` |

Atenção: a pasta é `Views`, com S.

---

### Exercício 19 — Criar uma Action completa

**Como reconhecer:** pedem para criar uma Action que recebe um `id`, utiliza um método auxiliar e devolve uma View com o objeto.

**O que fazer:**

1. Criar método `public IActionResult`.
2. Utilizar o nome da Action indicado.
3. Receber `int id`.
4. Guardar o resultado do método auxiliar numa variável.
5. Devolver `View(variável)`.

**Modelo:**

```csharp
public IActionResult NOME_ACTION(int id)
{
    var objeto = METODO_AUXILIAR(id);
    return View(objeto);
}
```

Exemplo:

```csharp
public IActionResult Show(int id)
{
    var article = GetArticle(id);
    return View(article);
}
```

Se pedirem apenas a View sem modelo:

```csharp
return View();
```

Se pedirem a View com um objeto:

```csharp
return View(objeto);
```

---

### Exercício 20 — ViewBag e ViewData

**Como reconhecer:** pedem para enviar uma mensagem ou valor do Controller para a View.

**ViewBag:**

```csharp
ViewBag.Message = "Bem-vindo!";
```

Para outra propriedade:

```csharp
ViewBag.Title = "Página Principal";
```

Na View:

```cshtml
@ViewBag.Message
```

**ViewData:**

```csharp
ViewData["Message"] = "Bem-vindo!";
```

Na View:

```cshtml
@ViewData["Message"]
```

**Conversão entre os dois:**

```cshtml
@ViewData["Title"]
```

é equivalente a aceder ao valor definido por:

```csharp
ViewBag.Title = "Página Principal";
```

---

### Exercício 21 — Data Annotations

**Como reconhecer:** pedem para alterar o nome apresentado de uma propriedade ou validar o formato do email.

**Alterar o nome apresentado:**

```csharp
[Display(Name = "Nome completo")]
public string FullName { get; set; }
```

**Validar email:**

```csharp
[EmailAddress]
public string Email { get; set; }
```

**Utilizar os dois:**

```csharp
[Display(Name = "Endereço de email")]
[EmailAddress]
public string Email { get; set; }
```

Se pedirem apenas o atributo, escreve só a linha correspondente.

---

### Exercício 22 — Partial View

**Como reconhecer:** aparece `@Html.Partial(...)` e pedem o conteúdo do ficheiro `.cshtml`.

**O que fazer:**
1. Declarar o tipo recebido com `@model`.
2. Utilizar `@Model.Propriedade` para apresentar os valores.

**Modelo:**

```cshtml
@model NOME_CLASSE

<p>@Model.Propriedade1 - @Model.Propriedade2</p>
```

Exemplo:

```cshtml
@model Product

<p>@Model.Name - @Model.Price</p>
```

Se pedirem o número da encomenda e o total:

```cshtml
@model Order

<p>Order #@Model.Id - @Model.Total €</p>
```

Atenção:
- `@model` declara o tipo.
- `@Model` acede ao objeto.
- `@Model.Name` acede à propriedade Name.

---

### Exercício 23 — Layout e RenderBody

**Como reconhecer:** perguntam onde se coloca o conteúdo da View dentro do Layout.

Resposta:

```cshtml
@RenderBody()
```

Se pedirem para definir o Layout utilizado numa View:

```cshtml
@{
    Layout = "~/Views/Shared/_Layout.cshtml";
}
```

Se pedirem para começar uma secção chamada `scripts`:

```cshtml
@section scripts {
```

---

### Exercício 24 — Atributo HttpPost

**Como reconhecer:** a Action recebe dados submetidos através de um formulário.

Resposta:

```csharp
[HttpPost]
```

Coloca-se por cima da Action:

```csharp
[HttpPost]
public IActionResult Create(string name, decimal price)
{
    return View();
}
```

---

### Exercício 25 — foreach e if em Razor

**Como reconhecer:** a View recebe uma lista e pedem para mostrar apenas os elementos que cumprem uma condição.

**O que fazer:**
1. Percorrer `Model` com `foreach`.
2. Utilizar `if` para verificar a condição.
3. Mostrar a propriedade pedida.

**Modelo:**

```cshtml
@foreach (var x in Model)
{
    if (x.PROPRIEDADE == VALOR)
    {
        <p>@x.PROPRIEDADE_A_MOSTRAR</p>
    }
}
```

Exemplo: mostrar apenas utilizadores ativos:

```cshtml
@foreach (var u in Model)
{
    if (u.Active)
    {
        <p>@u.Username</p>
    }
}
```

Se pedirem artigos com preço superior a 20:

```cshtml
@foreach (var a in Model)
{
    if (a.Price > 20)
    {
        <p>@a.Title</p>
    }
}
```

**Se pedirem uma mensagem quando a lista está vazia:**

```cshtml
@if (!Model.Any())
{
    <p>Sem eventos</p>
}
else
{
    foreach (var e in Model)
    {
        <p>@e.Title</p>
    }
}
```

---

## PARTE 4 — Entity Framework Core

### Exercício 26 — Criar duas classes com relação 1:N

**Como reconhecer:** dizem que uma entidade pode ter vários elementos de outra entidade.

Exemplo: um Customer pode ter muitas Orders.

**O que fazer:**

1. Ambas as classes precisam normalmente de `int Id`.
2. A classe do lado 1 tem uma lista da classe do lado N.
3. A classe do lado N tem uma FK.
4. A classe do lado N tem uma propriedade de navegação para a classe do lado 1.

**Modelo:**

```csharp
public class PAI
{
    public int Id { get; set; }
    public string Name { get; set; }

    public List<FILHO> FILHOS { get; set; }
}

public class FILHO
{
    public int Id { get; set; }
    public int PAIId { get; set; }

    public PAI PAI { get; set; }
}
```

Exemplo Customer / Order:

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

**Regra fundamental:**

| Lado 1 | Lado N |
|---|---|
| `List<Order> Orders` | `int CustomerId` |
| Tem uma lista | Tem a FK |
| Não precisa de FK para cada Order | Tem propriedade de navegação `Customer` |

---

### Exercício 27 — DbSet

**Como reconhecer:** perguntam o que representa um `DbSet<T>`.

Resposta:

`Tabela`

Exemplo:

```csharp
public DbSet<Product> Products { get; set; }
```

Representa normalmente a tabela Products na base de dados.

---

### Exercício 28 — Chave primária por convenção

**Como reconhecer:** pedem um nome de propriedade que seja reconhecido como Primary Key sem `[Key]`.

Duas convenções comuns:

```csharp
public int Id { get; set; }
```

ou:

```csharp
public int CustomerId { get; set; }
```

Se a classe for `Customer`, ambas podem ser reconhecidas como chave primária.

---

### Exercício 29 — Criar uma Migration

**Como reconhecer:** pedem para criar uma migration com determinado nome.

Com Package Manager Console:

```powershell
Add-Migration InitialCreate
```

Com CLI:

```bash
dotnet ef migrations add InitialCreate
```

Substitui `InitialCreate` pelo nome indicado no enunciado.

---

### Exercício 30 — Aplicar Migrations

**Como reconhecer:** perguntam qual é o comando para aplicar migrations à base de dados.

Resposta:

```bash
dotnet ef database update
```

Package Manager Console:

```powershell
Update-Database
```

---

### Exercício 31 — Code First e Database First

| O que o enunciado diz | Resposta |
|---|---|
| Criar classes primeiro e gerar a BD | Code First |
| BD já existe e gerar classes a partir dela | Database First |

---

### Exercício 32 — Include e FirstOrDefault

**Como reconhecer:** a View precisa de uma propriedade de outra entidade, por exemplo:

```cshtml
@order.Customer.Name
```

E o exercício pede para carregar apenas um registo pelo seu `Id`.

**O que fazer:**

1. `Include` para carregar a entidade relacionada.
2. `FirstOrDefault` para encontrar o registo pelo identificador.

**Modelo:**

```csharp
.Include(x => x.PROPRIEDADE_RELACIONADA)
.FirstOrDefault(x => x.Id == id)
```

Exemplo:

```csharp
var order = context.Orders
    .Include(o => o.Customer)
    .FirstOrDefault(o => o.Id == id);
```

Se a View precisar de `post.Category.Name`:

```csharp
.Include(p => p.Category)
```

---

### Exercício 33 — Where + Include + OrderBy

**Como reconhecer:** pedem para filtrar registos por uma FK, carregar dados relacionados e ordenar.

**O que fazer:**

1. `Where`: filtrar pela FK.
2. `Include`: carregar a entidade relacionada.
3. `OrderBy`: ordenar.
4. `ToList()`: materializar a lista, se já estiver indicado no enunciado.

**Modelo:**

```csharp
var resultado = _context.NOME_DA_TABELA
    .Where(x => x.FK == variavel)
    .Include(x => x.ENTIDADE_RELACIONADA)
    .OrderBy(x => x.PROPRIEDADE)
    .ToList();
```

Exemplo:

```csharp
var posts = _context.BlogPosts
    .Where(p => p.CategoryId == categoryId)
    .Include(p => p.Category)
    .OrderBy(p => p.Title)
    .ToList();
```

Se o enunciado não pedir ordenação, não acrescentes `OrderBy`.

---

### Exercício 34 — DbContext e configuração da base de dados

**Como reconhecer:** perguntam de que classe herda o contexto da base de dados.

Resposta:

```csharp
DbContext
```

Exemplo:

```csharp
public class ApplicationDbContext : DbContext
{
}
```

**Configurar SQL Server:**

```csharp
options.UseSqlServer(connectionString);
```

Método pedido:

```csharp
UseSqlServer
```

**Ficheiro onde se coloca normalmente a connection string:**

```text
appsettings.json
```

---

## PARTE 5 — ASP.NET Core Identity e Razor Pages

### Exercício 35 — Propriedades de IdentityUser

Se perguntarem qual a propriedade que representa o email:

```csharp
Email
```

Se perguntarem qual representa o número de telefone:

```csharp
PhoneNumber
```

### Exercício 36 — UserManager e RoleManager

| Tipo | Função |
|---|---|
| `UserManager` | Gere utilizadores |
| `RoleManager` | Gere roles |
| `IdentityUser` | Tipo de utilizador predefinido |
| `IdentityRole` | Tipo de role predefinido |

Exemplos:

```csharp
UserManager<IdentityUser>
RoleManager<IdentityRole>
```

Se a aplicação utilizar `ApplicationUser`:

```csharp
UserManager<ApplicationUser>
```

### Exercício 37 — IdentityRole

**Como reconhecer:** perguntam qual é a classe que representa um role, por exemplo Administrator ou Teacher.

Resposta:

```csharp
IdentityRole
```

### Exercício 38 — Autorizações

| O que pedem | Código |
|---|---|
| Apenas utilizadores autenticados | `[Authorize]` |
| Apenas Admin | `[Authorize(Roles = "Admin")]` |
| Apenas Teacher | `[Authorize(Roles = "Teacher")]` |
| Admin ou Manager | `[Authorize(Roles = "Admin, Manager")]` |
| Permitir acesso anónimo | `[AllowAnonymous]` |

Se o Controller tiver `[Authorize]` e quiseres tornar uma Action pública:

```csharp
[AllowAnonymous]
public IActionResult Index()
{
    return View();
}
```

### Exercício 39 — Razor Pages

**Como reconhecer:** perguntam qual é a classe base de uma Razor Page ou o método executado num pedido GET.

| Pergunta | Resposta |
|---|---|
| Classe base | `PageModel` |
| Método para GET | `OnGet()` |
| Método para POST | `OnPost()` |

Exemplo:

```csharp
public class IndexModel : PageModel
{
    public void OnGet()
    {
    }
}
```

---

# CHECKLIST FINAL — Antes de entregar

- [ ] Nos construtores, confirmei os parâmetros e o `base(...)`.
- [ ] Nas propriedades, utilizei o tipo correto e `{ get; set; }`.
- [ ] Nas lambdas, coloquei os parâmetros antes de `=>`.
- [ ] No LINQ, distingui `Where`, `Select`, `Any` e `All`.
- [ ] Nos exercícios de foreach para LINQ, mantive os elementos originais quando pedido.
- [ ] Nas rotas, identifiquei corretamente Controller, Action e parâmetros.
- [ ] Nas Views, utilizei `Views/NomeController/NomeAction.cshtml`.
- [ ] Nas Actions, utilizei `public IActionResult`.
- [ ] No Razor, distingui `@model` de `@Model`.
- [ ] Nas relações 1:N, coloquei a lista no lado 1 e a FK no lado N.
- [ ] Utilizei `Include` quando a View precisa de dados relacionados.
- [ ] Distingui Code First de Database First.
- [ ] Distingui `[Authorize]` de `[AllowAnonymous]`.

**Regra de ouro:** adapta os nomes dos exemplos aos nomes do enunciado. A estrutura do código mantém-se, mesmo que mudem `Product` para `Student`, `Customer` para `Teacher` ou `Price` para `Grade`.
