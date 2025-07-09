## Overview

This project is an ASP.NET Core Web API that fetches country data from the public [REST Countries API](https://restcountries.com/), 
stores it in a Microsoft SQL Server database, and exposes RESTful endpoints to retrieve the stored data.

## Features
- Fetches country data from a third-party API (REST Countries).
- Stores country data (Name, ISO Code, Capital) in SQL Server without using an ORM.
- Provides RESTful endpoints:
  - `GET /api/countries` — returns a list of countries.
  - `GET /api/countries/{id}` — returns a single country by its database ID.
  - `GET /api/countries/iso/{isoCode}` — fetches by ISO code, from DB if available or from API and then saved.
- Centralized error handling and standardized API responses.
- Implements repository and service layers for separation of concerns.
- Uses raw SQL queries for database operations (no Entity Framework).
- Uses HttpClient with a typed API client wrapper to consume third-party API.
- Configurable API base URL and database connection string via appsettings.json.
- Unit tests for service layer with mocked dependencies.

## Technologies

- ASP.NET Core 7 Web API
- Microsoft SQL Server
- Raw ADO.NET for database access
- xUnit and Moq for unit testing
- REST Countries API (https://restcountries.com/)
- Dependency Injection, Clean Architecture principles


---

## Setup & Run

### Prerequisites
- .NET SDK 7.x or higher installed
- Microsoft SQL Server instance running (local or remote)
- SQL Server Management Studio or similar tool (optional for DB management)

### Database Setup
1. Modify the connection string in `Api/appsettings.json` to point to your SQL Server instance:

```json
"ConnectionStrings": {
  "DefaultConnection": "Server=YOUR_SERVER_NAME;Database=CountryDb;Trusted_Connection=True;"
}
```

Run the SQL schema script located at `database/schema.sql` to create the `Countries` table.

```sql
CREATE TABLE Countries (
  Id INT IDENTITY(1,1) PRIMARY KEY,
  Name NVARCHAR(255) NOT NULL,
  IsoCode CHAR(2) NOT NULL UNIQUE,
  Capital NVARCHAR(255) NULL
);
```
OR 
# Using sqlcmd CLI (SQL Server Command Line tool)
sqlcmd -S <server_name> -d <database_name> -i database/schema.sql

dotnet run --project Api/WebApiDemo.Api.csproj

Demo :
![image](https://github.com/user-attachments/assets/401cad4a-6ea0-466c-ade9-bddaeefd2078)


