# Introduction to ASP.NET Core
### History
MS Created .NET Framework => 2001
1,1.1,2,3,3.5,4,4.5, 4.6, 4.7, 4.8
Windows centric =>
2009 => MVC 1.0 in .NET Framework
2013 => MVC 5.3

### .NET Core
2016 => .NET Core 1.0 
1. Cross Platform => Windows/Mac/Linux/Android/iOS/tvOS
2. X64, ARM32/64
3. Open Source => GitHub

#### .NET Release Cycle - November months
2017 => .NET Core 2.0
2018 => .NET Core 2.2
2019 => .NET Core 3.0
2020 => .NET 5
2021 => .NET 6 , ASP.NET Core ( Web Apps, Web API), Entity Framework Core (ORM) => communicate with database

#### ASP.NET
1. MVC => Model View Controller (Web Applications)
2. Web API => REST API over HTTP , return JSON Data

#### MVC
1. Model => Show list of employees in a page => List<Employee> 
2. View => UI Browser => HTML+CSS+JS+ Razor Syntax(ASP.NET Specific)
3. Controller => Logic is there => Each and Every request in MVC should go through controller

Whenever you make any HTTP Request (GET, POST, PUT and DELETE) to server => ASP.NET Server and it will respond back with RESPONSE
Response => HTML, CSS, JS => ALL UI Elements (Buttons, Dropdowns, Radio BUttons, CheckBOxex, Textboxes)


1. GET => http://www.example.com/employee/details/22  ASP.NET MVC
   1. First Part after domian name is Controller in MVC
   2. Second Part is action method
   3. Route Paramter/data
2. GET =>  http://www.example.com/employee/create => Show a web page so that user can enter Employee details
3. POST => http://www.example.com/employee/create => Submitting 
Controller is a C# class in MVC but it derives from Controller class

```csharp
public class EmployeeController: Controller
 {
     [HttpGet]
     public IActionResult Details(int id) 
     {
          //  go to database and get employee details by id
          Employee employee = new EmployeeService().GetDetails(id);
         // return a view
         return View(employee);
     }

    [HttpGet]
     public IActionResult Create()
      {
          // empty view for user to enter Employee information
          return View();
      }

    [HttpPost]
     public IActionResult Create(Employee emp) 
     {
         // save the employee to database and return view
         return View();
     } 
 }
```

#### Onion/Clean/Layered Architecture

Make sure Code should properly structured and should be maintenable and testable and reuse the code.
Loosley Coupled Code => Interfaces with Depedency Injection

1. ApplicationCore =>  Base of the project, Class Library
   1. Entities => Objects/Classes that represent our database tables
      1. Entities will have all the properties of that table
      2. Movie { 20 properties}
   2. Models => Objects/Classes that we use for our View
      1. MovieCardModel { 3 properties => Id, Title, PosterUrl }
      2. MovieDetailsModel => {Models based on View Requirements}
   3. Contracts (Interfaces)
      1. Repository Interfaces
      2. Services Interfaces 
   4. Helper => Heler or Untility classes
   5. Exceptions => Custom Exception classes such as MovieNotFoundException, InvalidDataException

2. Infrastructure => Class Library, Refereces Application Core Project
   1. Implementation of the Repository and Services Contracts
   2. Repostories => Persistence (dataabse logic) EF Core, Dapper, ADO.NET
   3. Services => Business Logic => Purchasing Movie, Hashing Password
      1. Servcies Will comminucate with Repositories which will communicate with database
      2. Additional Helpers

3. MVC (Web) => UI Layer, Dependecy on Infrastructure and ApplicationCore
   1. Controllers
   2. Views