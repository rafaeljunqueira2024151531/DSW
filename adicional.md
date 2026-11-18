Ahh, queres uma **lista de nomes de propriedades comuns em classes C#**, como `PhoneNumber`, `Email`, `FirstName`, etc., para reconheceres o que cada uma representa nos exercícios.

# **Nomes de propriedades comuns em C#**

## **Dados pessoais / utilizadores**

| Propriedade   | Significado        |
| ------------- | ------------------ |
| `Id`          | Identificador      |
| `Name`        | Nome               |
| `FirstName`   | Primeiro nome      |
| `LastName`    | Apelido            |
| `FullName`    | Nome completo      |
| `Username`    | Nome de utilizador |
| `Email`       | Endereço de email  |
| `PhoneNumber` | Número de telefone |
| `Address`     | Morada             |
| `City`        | Cidade             |
| `PostalCode`  | Código postal      |
| `Country`     | País               |
| `BirthDate`   | Data de nascimento |
| `Age`         | Idade              |
| `Gender`      | Género             |
| `Password`    | Palavra-passe      |

## **Produtos / lojas**

| Propriedade   | Significado                |
| ------------- | -------------------------- |
| `ProductId`   | Identificador do produto   |
| `Name`        | Nome                       |
| `Description` | Descrição                  |
| `Price`       | Preço                      |
| `Stock`       | Quantidade em stock        |
| `Quantity`    | Quantidade                 |
| `Category`    | Categoria                  |
| `CategoryId`  | Identificador da categoria |
| `Brand`       | Marca                      |
| `ImageUrl`    | Endereço da imagem         |
| `IsAvailable` | Está disponível?           |
| `IsActive`    | Está ativo?                |

## **Encomendas / pagamentos**

| Propriedade       | Significado                |
| ----------------- | -------------------------- |
| `OrderId`         | Identificador da encomenda |
| `OrderDate`       | Data da encomenda          |
| `Total`           | Valor total                |
| `TotalPrice`      | Preço total                |
| `CustomerId`      | Identificador do cliente   |
| `Customer`        | Cliente associado          |
| `Status`          | Estado                     |
| `PaymentMethod`   | Método de pagamento        |
| `PaymentDate`     | Data do pagamento          |
| `IsPaid`          | Está pago?                 |
| `ShippingAddress` | Morada de entrega          |

## **Datas e estados**

| Propriedade   | Significado                |
| ------------- | -------------------------- |
| `CreatedAt`   | Data de criação            |
| `UpdatedAt`   | Data da última atualização |
| `StartDate`   | Data de início             |
| `EndDate`     | Data de fim                |
| `DueDate`     | Prazo / data limite        |
| `IsActive`    | Está ativo?                |
| `IsDeleted`   | Está eliminado?            |
| `IsCompleted` | Está concluído?            |
| `IsApproved`  | Está aprovado?             |
| `IsEnabled`   | Está ativado?              |

## **Universidade / escola**

| Propriedade      | Significado            |
| ---------------- | ---------------------- |
| `StudentId`      | Identificador do aluno |
| `StudentNumber`  | Número de aluno        |
| `Course`         | Curso                  |
| `Subject`        | Disciplina             |
| `Grade`          | Nota                   |
| `Credits`        | Créditos               |
| `Teacher`        | Professor              |
| `Department`     | Departamento           |
| `EnrollmentDate` | Data de inscrição      |
| `IsEnrolled`     | Está inscrito?         |

# **Palavras que aparecem frequentemente**

Estas partes ajudam-te a perceber propriedades que nunca viste:

| Palavra       | Significado     |
| ------------- | --------------- |
| `Number`      | Número          |
| `Name`        | Nome            |
| `Date`        | Data            |
| `Time`        | Hora            |
| `Price`       | Preço           |
| `Amount`      | Quantia / valor |
| `Total`       | Total           |
| `Count`       | Contagem        |
| `Quantity`    | Quantidade      |
| `Address`     | Morada          |
| `Description` | Descrição       |
| `Status`      | Estado          |
| `Type`        | Tipo            |
| `Category`    | Categoria       |
| `Created`     | Criado          |
| `Updated`     | Atualizado      |
| `Is...`       | É / Está...     |
| `Has...`      | Tem...          |

**Dica importante:** em C#, propriedades que começam por `Is` são normalmente booleanas (`bool`), por exemplo `IsActive`, `IsPaid` e `IsAvailable`.

E propriedades terminadas em `Id`, como `CustomerId` ou `CategoryId`, são frequentemente identificadores e podem representar chaves estrangeiras (FK) numa relação entre tabelas.

Isto é especialmente útil para perceberes rapidamente as classes dos exercícios de C#, MVC e Entity Framework.
