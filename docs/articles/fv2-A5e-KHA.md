---
layout: "../../layouts/BlogPost.astro"
title: "Introduction to MongoDB and Entity Framework Core for .NET Development"
pubDate: "2025-02-28 15:37:54.358277"
youtubeVideoID: "fv2-A5e-KHA"
index: 59
---

# Introduction to MongoDB and Entity Framework Core for .NET Development

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/fv2-A5e-KHA" frameborder="0" allowfullscreen></iframe>

This chapter provides an introduction to using MongoDB, a NoSQL database, with Microsoft's Entity Framework Core (EF Core), an Object-Relational Mapper (ORM) for .NET. We will explore the fundamental concepts of MongoDB, understand the benefits of EF Core, and learn how to bridge these technologies using the MongoDB EF Core provider. By the end of this chapter, you will have a foundational understanding of how to leverage MongoDB's flexibility and scalability within the .NET ecosystem using the familiar patterns of EF Core.

### 1.1 Introduction to MongoDB: A NoSQL Database

MongoDB is a widely adopted NoSQL database renowned for its ability to manage large datasets, deliver high performance, and offer excellent scalability and flexibility. Unlike traditional relational databases, MongoDB adopts a document-oriented approach, storing data in flexible, JSON-like documents.

> **NoSQL Database:** A type of database that deviates from the traditional relational database model. NoSQL databases are designed to handle large volumes of unstructured or semi-structured data, offering flexibility and scalability.

#### 1.1.1 Document-Oriented Approach

MongoDB's document-oriented structure allows for a more natural and intuitive representation of complex data. Instead of rigid tables and schemas, data is organized into collections of documents.

> **Document:** In MongoDB, a document is a set of key-value pairs, similar to a JSON object. It is the basic unit of data in MongoDB and can have a flexible schema.

Consider an example of storing user information. In MongoDB, a user document might look like this:

```json
{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "age": 30,
  "address": {
    "street": "123 Main St",
    "city": "Anytown",
    "state": "CA",
    "zip": "12345"
  },
  "hobbies": ["reading", "hiking", "coding"]
}
```

Here, `address` is an **embedded document**, and `hobbies` is an **array**, demonstrating the ability to store complex, nested data within a single document.

> **Embedded Document:** A document nested within another document, representing a sub-structure of data. This allows for rich and hierarchical data representation within a single MongoDB document.

#### 1.1.2 Collections: Organizing Documents

In MongoDB, documents are grouped into **collections**, which are analogous to tables in relational databases. However, a key distinction is that collections in MongoDB do not enforce a fixed schema.

> **Collection:** A grouping of MongoDB documents, similar to a table in relational databases. Collections are schema-less, meaning documents within the same collection can have different structures and fields.

This schema-less nature provides significant flexibility, allowing for documents within the same collection to have varying structures. This is particularly advantageous when dealing with unstructured or semi-structured data where the data schema might evolve or differ significantly across entries.

#### 1.1.3 BSON: Binary JSON

While MongoDB documents resemble JSON, they are actually stored in a binary format called **BSON (Binary JSON)**.

> **BSON (Binary JSON):** A binary-encoded serialization of JSON-like documents. BSON extends JSON to include additional data types and is optimized for efficient storage and retrieval in MongoDB.

BSON extends the JSON model by incorporating additional data types such as integers, floats, dates, and binary data. This binary format is optimized for both performance and flexibility, enabling MongoDB to efficiently store and retrieve data.

#### 1.1.4 Scalability and Performance

MongoDB is designed for horizontal scalability, a crucial feature for handling large datasets and ensuring high availability.

> **Horizontal Scalability:** The ability to increase the capacity of a system by adding more servers or nodes to distribute the workload. MongoDB is designed to scale horizontally, allowing it to handle increasing data volumes and traffic.

Horizontal scalability means that data can be distributed across multiple servers. This distribution simplifies the management of large datasets and ensures high availability, as the system can remain operational even if some servers fail.

Beyond scalability, MongoDB offers robust querying capabilities, indexing, and aggregation functionalities. These features make it a powerful tool for diverse applications ranging from e-commerce and content management systems to real-time analytics and Internet of Things (IoT) applications. Its flexibility and scalability make MongoDB an excellent choice for modern applications dealing with diverse and dynamic data.

### 1.2 Introduction to Entity Framework Core (EF Core): An ORM for .NET

Moving to the .NET development side, **Entity Framework Core (EF Core)**, often abbreviated as EF Core, is a modern **Object-Relational Mapper (ORM)** for .NET.

> **Object-Relational Mapper (ORM):** A programming technique that bridges the gap between object-oriented programming languages and relational databases. ORMs allow developers to interact with databases using object-oriented paradigms, reducing the need for manual SQL coding.

EF Core simplifies database interactions by allowing developers to work with databases using .NET objects. This abstraction eliminates the need for extensive data access code that developers typically have to write when interacting directly with databases.

EF Core is lightweight, extensible, and cross-platform, evolving from the popular Entity Framework data access technology. It supports various database engines, including SQL Server, SQLite, and, importantly for our focus, MongoDB.

#### 1.2.1 Benefits of Using EF Core

One of the primary advantages of EF Core is its ability to enable developers to interact with data in a more intuitive and object-oriented manner. Instead of writing raw SQL queries, developers can utilize **LINQ (Language Integrated Query)** and strongly-typed classes to interact with their database.

> **LINQ (Language Integrated Query):** A powerful feature in .NET that allows developers to write queries against various data sources using a consistent syntax directly within C# or VB.NET code.

Consider a simple `Product` class in .NET:

```csharp
public class Product
{
    public int ProductId { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}
```

With EF Core, you can create a **context class** that represents a session with the database and includes a **DbSet** for each entity type you wish to query or save.

> **Context Class (DbContext):** In EF Core, a class that inherits from `DbContext`. It represents a session with the database and is used to query and save instances of your entities.

> **DbSet:** A property within a DbContext class that represents a collection of entities of a specific type, corresponding to a table or collection in the database.

For example, an `AppDbContext` class might look like this:

```csharp
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlServer("YourConnectionString"); // Placeholder for SQL Server connection
    }
}
```

This code defines `AppDbContext` inheriting from `DbContext`. It includes a `DbSet<Product>` named `Products`, representing a collection of `Product` entities (and conceptually, a table named "Products" in a relational database if using SQL Server as in this example). The `OnConfiguring` method configures the database connection, specifying SQL Server as the provider using `UseSqlServer`.  Note that for MongoDB, we will use `UseMongoDB` later.

#### 1.2.2 CRUD Operations with EF Core

With EF Core, performing **CRUD (Create, Read, Update, Delete)** operations becomes straightforward.

> **CRUD (Create, Read, Update, Delete):** The four basic operations performed on data in persistent storage. EF Core simplifies these operations for .NET developers.

**Creating Data:** To add a new product, you can use the following code:

```csharp
using (var context = new AppDbContext())
{
    var newProduct = new Product { Name = "Laptop", Price = 999.99m };
    context.Products.Add(newProduct);
    context.SaveChanges();
}
```

This code creates an instance of `AppDbContext`, instantiates a new `Product` object, adds it to the `Products` DbSet, and then calls `SaveChanges()` to persist the changes to the database.

**Reading Data:** To query products, you can use LINQ:

```csharp
using (var context = new AppDbContext())
{
    var products = context.Products
        .Where(p => p.Price > 500)
        .ToList();

    foreach (var product in products)
    {
        Console.WriteLine($"Name: {product.Name}, Price: {product.Price}");
    }
}
```

This code retrieves all products with a price greater than 500 using a LINQ query. EF Core translates this LINQ query into the appropriate SQL commands for the configured database.

EF Core also supports advanced features such as change tracking, lazy loading, and migrations, which are crucial for managing database schema evolution over time.

In summary, EF Core is a powerful ORM that simplifies data access in .NET applications. It allows developers to work with data using .NET objects and LINQ, supporting multiple database engines and offering extensibility for various application needs.

### 1.3 Bridging MongoDB and EF Core: The MongoDB EF Core Provider

The **MongoDB EF Core provider** acts as a bridge between MongoDB and EF Core, enabling developers to use MongoDB with the familiar API and design patterns of EF Core.

> **MongoDB EF Core Provider:** A NuGet package that allows Entity Framework Core to interact with MongoDB databases. It translates EF Core operations into MongoDB commands.

This provider allows you to utilize code-first and LINQ query methodologies with MongoDB, similar to how you would with relational databases. This significantly streamlines development and reduces the learning curve for developers already familiar with EF Core.

#### 1.3.1 Key Capabilities of the MongoDB EF Core Provider

The MongoDB EF Core provider supports several key features that facilitate seamless integration:

*   **Code-First Workflows:** Define your data models in C# and let EF Core generate the MongoDB schema. This approach is particularly beneficial for MongoDB, where schema flexibility is a core advantage.

    > **Code-First Workflow:** A development approach in EF Core where you define your data models as C# classes first, and EF Core then generates the database schema based on these models.

*   **CRUD Operations:** Supports standard Create, Read, Update, and Delete operations, allowing you to manipulate data in MongoDB using EF Core methods.

*   **LINQ Query Support:** Enables you to perform queries against MongoDB using LINQ, leveraging your existing .NET skills.

*   **Change Tracking:** EF Core's change tracking capabilities are supported, automatically detecting and saving modifications to your data entities.

*   **Embedded Documents Support:** Allows you to work with MongoDB's embedded documents, maintaining the natural document structure within your .NET application.

*   **Class Mapping and Serialization:** Maps your C# classes to MongoDB collections, handling data type conversions and serialization settings to ensure correct data storage.

#### 1.3.2 Setting Up the MongoDB EF Core Provider

To begin using the MongoDB EF Core provider, you need to add the necessary **NuGet packages** to your .NET project.

> **NuGet Packages:**  Packages of reusable code for .NET projects, distributed through the NuGet Package Manager. They simplify the process of adding libraries and dependencies to your projects.

These packages enable your application to interact with MongoDB through EF Core, utilizing the same context and entity definitions you would use with a relational database.

Before performing CRUD operations, you need to set up a MongoDB Atlas cluster and establish a connection from your application to it. **MongoDB Atlas** is a fully-managed cloud database service.

> **MongoDB Atlas:** MongoDB's fully managed cloud database service. It simplifies deployment, operations, and scaling of MongoDB databases.

The general steps involve:

1.  **Sign up for a MongoDB Atlas account.** A free tier is available for development and small-scale applications.
2.  **Create a new cluster** within MongoDB Atlas.
3.  **Obtain a connection string** from the MongoDB Atlas dashboard. This string contains the necessary credentials to connect to your cluster. A typical connection string looks like:

    ```
    mongodb+srv://<username>:<password>@<cluster-url>/<database-name>?retryWrites=true&w=majority
    ```

    Remember to replace placeholders like `<username>`, `<password>`, `<cluster-url>`, and `<database-name>` with your actual credentials.

#### 1.3.3 Defining Data Models and Performing CRUD Operations

To use the provider, you first define your data model classes. For example, a `Customer` class might be defined as:

```csharp
using MongoDB.Bson;
using MongoDB.Bson.Serialization.Attributes;

namespace YourNamespace.Models
{
    [BsonCollection("customers")] // Attribute to specify the MongoDB collection name
    public class Customer
    {
        [BsonId] // Attribute to specify the primary key
        [BsonRepresentation(BsonType.ObjectId)] // Attribute to represent ID as ObjectId
        public string Id { get; set; }
        public string Name { get; set; }
        public string Email { get; set; }
        public string Order { get; set; }
    }
}
```

The `[BsonCollection]` attribute specifies the MongoDB collection name ("customers"). `[BsonId]` and `[BsonRepresentation(BsonType.ObjectId)]` attributes are used to configure the `Id` property as the primary key and map it to MongoDB's `ObjectId` type.

Next, create a `DbContext` class, such as `RestaurantReservationDbContext`, inheriting from `DbContext`:

```csharp
using Microsoft.EntityFrameworkCore;
using YourNamespace.Models;

namespace YourNamespace.Services
{
    public class RestaurantReservationDbContext : DbContext
    {
        public RestaurantReservationDbContext(DbContextOptions<RestaurantReservationDbContext> options) : base(options)
        {
        }

        public DbSet<Customer> Customers { get; set; }
    }
}
```

In the `Startup.cs` or `Program.cs` file, configure the `DbContext` to use the MongoDB provider, typically within the `ConfigureServices` method:

```csharp
services.AddDbContext<RestaurantReservationDbContext>(options =>
    options.UseMongoDB("mongodb://<connection-string>/<database-name>") // Replace with your connection string and database name
);
```

Replace `"mongodb://<connection-string>/<database-name>"` with your actual MongoDB Atlas connection string.

Now you can perform CRUD operations using your `DbContext`.

**Create:**

```csharp
using (var context = new RestaurantReservationDbContext())
{
    var newCustomer = new Customer { Name = "Alice Smith", Email = "alice@example.com", Order = "Pizza" };
    context.Customers.Add(newCustomer);
    context.SaveChanges();
}
```

**Read:**

```csharp
using (var context = new RestaurantReservationDbContext())
{
    var allCustomers = context.Customers.ToList();
    foreach (var customer in allCustomers)
    {
        Console.WriteLine($"Customer Name: {customer.Name}, Order: {customer.Order}");
    }
}
```

**Update:**

```csharp
using (var context = new RestaurantReservationDbContext())
{
    var customerToUpdate = context.Customers.FirstOrDefault(c => c.Name == "John Doe");
    if (customerToUpdate != null)
    {
        customerToUpdate.Order = "Smartphone";
        context.SaveChanges();
    }
}
```

**Delete:**

```csharp
using (var context = new RestaurantReservationDbContext())
{
    var customerToDelete = context.Customers.FirstOrDefault(c => c.Name == "Bo KS");
    if (customerToDelete != null)
    {
        context.Customers.Remove(customerToDelete);
        context.SaveChanges();
    }
}
```

EF Core's change tracking efficiently updates documents, generating MongoDB commands to modify only the changed fields. By using the MongoDB EF provider, you can seamlessly integrate MongoDB's flexible document model with EF Core's robust ORM capabilities, creating powerful and adaptable applications.

### 1.4 Building a Restaurant Reservation System: A Practical Project

To demonstrate the practical application of MongoDB with EF Core, we will develop a restaurant reservation system. This project will utilize sample restaurant data provided by MongoDB Atlas to create a functional application.

#### 1.4.1 Project Setup and MongoDB Atlas Integration

The project setup involves:

1.  **Creating a new .NET Web Application (Model-View-Controller)** project in Visual Studio or Visual Studio Code.
2.  **Adding the MongoDB EF Core NuGet package** to the project.
3.  **Setting up a MongoDB Atlas cluster** (as outlined in Section 1.3.2).
4.  **Loading sample data into the MongoDB Atlas cluster.** MongoDB Atlas provides sample datasets, including restaurant data, which can be easily loaded into your cluster.
5.  **Configuring the connection string** in your application's `appsettings.json` file to connect to your MongoDB Atlas cluster.

#### 1.4.2 Data Models and DbContext for the Reservation System

Define data models for `Restaurant` and `Reservation` entities, reflecting the structure of the sample restaurant data and the requirements of a reservation system.

Create a `DbContext` class, `RestaurantReservationDbContext`, with `DbSet` properties for `Restaurant` and `Reservation` entities. Configure this `DbContext` to use the MongoDB provider in your `Program.cs` file, referencing the connection string from your configuration.

#### 1.4.3 Implementing CRUD Operations and User Interface

Implement services for performing CRUD operations on `Restaurant` and `Reservation` entities using the `RestaurantReservationDbContext`. These services will encapsulate data access logic and be used by the application's controllers.

Develop MVC controllers (`RestaurantController` and `ReservationController`) to handle user requests and interact with the services. Create corresponding Razor views to provide a user interface for listing restaurants, making reservations, and managing restaurant and reservation data.

The user interface should allow for:

*   Viewing a list of restaurants.
*   Adding new restaurants.
*   Editing existing restaurant information.
*   Deleting restaurants.
*   Making reservations for restaurants, including selecting date and time.
*   Viewing a list of reservations.
*   Editing and deleting reservations.

Bootstrap CSS framework, which is included by default in ASP.NET MVC projects, can be used to style the user interface and make it responsive.

#### 1.4.4 Running and Testing the Application

After implementing the backend services, controllers, and frontend views, run the application. Test all CRUD operations for both restaurants and reservations to ensure the system functions correctly and interacts with the MongoDB Atlas database as expected. Verify that data is correctly created, read, updated, and deleted in MongoDB.

### 1.5 Advanced MongoDB Atlas Features: Atlas Search and Vector Search

Beyond basic CRUD operations, MongoDB Atlas offers advanced features like **Atlas Search** and **Vector Search** that can significantly enhance application capabilities.

> **Atlas Search:** A fully-managed, full-text search engine within MongoDB Atlas, allowing for complex search queries on MongoDB data.

> **Vector Search:** A feature in MongoDB Atlas that enables searching documents based on vector similarity, useful for applications involving semantic search, recommendations, and machine learning.

#### 1.5.1 Atlas Search Integration

Atlas Search provides a full-text search engine for MongoDB data. To integrate Atlas Search with your EF Core application:

1.  **Set up Search Indexes in MongoDB Atlas:** Create a new search index in your MongoDB Atlas cluster, specifying the fields you want to make searchable.
2.  **Define Searchable Fields in Models:** Ensure the fields you intend to search are properly defined in your .NET models.
3.  **Perform Search Queries using MongoDB .NET Driver:** Since EF Core does not directly support MongoDB-specific search syntax, you need to use the MongoDB .NET driver in conjunction with EF Core for search operations.

Example of performing a text search using the MongoDB .NET driver:

```csharp
using MongoDB.Driver;
using MongoDB.Entities; // Assuming you are using MongoDB.Entities for driver access

// Assuming 'DB' is initialized with your MongoDB connection
var collection = DB.Collection<Product>(); // Get the MongoDB collection for Product

var filter = Builders<Product>.Filter.Text("search term"); // Create a text search filter
var searchResults = await collection.Find(filter).ToListAsync(); // Execute the search query
```

#### 1.5.2 Vector Search Capabilities

Vector Search in MongoDB allows for similarity-based searches, which is particularly valuable for applications involving machine learning and semantic understanding.

While the MongoDB EF Core provider simplifies CRUD operations, advanced features like Vector Search typically require direct interaction with the MongoDB .NET driver. You can integrate these operations within your EF Core-based application by using the driver for search functionalities and EF Core for general data management.

By combining EF Core with advanced MongoDB Atlas features, you can build powerful, flexible applications that leverage the strengths of both technologies: EF Core's structured data access patterns and MongoDB's powerful search and data handling capabilities.

### 1.6 Conclusion

This chapter has provided a comprehensive introduction to using MongoDB with Entity Framework Core in .NET development. We explored the core concepts of MongoDB, the benefits of EF Core, and how to bridge these technologies using the MongoDB EF Core provider. Through a practical restaurant reservation system project, we demonstrated how to implement CRUD operations and build a functional application leveraging both MongoDB and EF Core. Finally, we touched upon advanced MongoDB Atlas features like Atlas Search and Vector Search, highlighting their potential to enhance application functionalities.

By combining the flexibility and scalability of MongoDB with the familiar and structured approach of EF Core, developers can create robust, scalable, and adaptable .NET applications, making the most of MongoDB's powerful features while leveraging the well-established EF Core framework. This combination equips developers with the tools and knowledge to build modern, data-driven applications that meet the demands of today's dynamic data landscape.

