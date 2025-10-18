# AdventureWorksLT2022 - ADO.NET Learning Project

This is a personal learning project focused on mastering **ADO.NET** for database connectivity using the AdventureWorksLT2022 sample database.

## 🎯 Learning Focus: ADO.NET

I created this project to learn and practice:
- **Raw ADO.NET** database operations using `SqlConnection`, `SqlCommand`, and `SqlDataReader`
- **Manual connection management** and resource disposal patterns
- **Direct SQL query execution** without ORM abstractions
- **Data mapping** from `SqlDataReader` to custom objects
- **Connection string configuration** and dependency injection

## 🏗️ Technology Stack

- **.NET 8.0** with **ASP.NET Core Web API**
- **Microsoft.Data.SqlClient** - Core ADO.NET provider
- **SQL Server** - AdventureWorksLT2022 database
- **Raw ADO.NET** - No Entity Framework or ORM

## � ADO.NET Implementation Examples

### Customer Service - Raw ADO.NET Pattern
```csharp
public async Task<List<Output>> GetAllCustomers() {
    using (var connection = new SqlConnection(_connectionString)) {
        await connection.OpenAsync();
        var query = "SELECT CustomerID, FirstName, LastName FROM SalesLt.Customer";
        SqlCommand cmd = new SqlCommand(query, connection);
        SqlDataReader reader = await cmd.ExecuteReaderAsync();
        
        List<Output> customers = new List<Output>();
        while (reader.Read()) {
            customers.Add(new Output {
                CustomerID = reader.GetInt32(0),
                FirstName = reader.GetString(1),
                LastName = reader.GetString(2)
            });
        }
        return customers;
    }
}
```

## 🗄️ AdventureWorksLT2022 Database

**Download from**: [Microsoft SQL Server Samples](https://github.com/Microsoft/sql-server-samples/releases) - Look for `AdventureWorksLT2022.bak`

**Setup**: Restore the `.bak` file to your SQL Server instance and update the connection string in `appsettings.Development.json`

## 🎓 ADO.NET Concepts Learned

- **Connection Management**: Using `SqlConnection` with proper disposal patterns
- **Command Execution**: Building and executing SQL commands with `SqlCommand`
- **Data Reading**: Iterating through results with `SqlDataReader`
- **Resource Management**: Proper use of `using` statements for automatic cleanup
- **Async Operations**: Implementing async database operations for better performance
- **Manual Mapping**: Converting database records to C# objects without ORM magic

---

*Learning ADO.NET fundamentals before moving to higher-level ORMs like Entity Framework.*