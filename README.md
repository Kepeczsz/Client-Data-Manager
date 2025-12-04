# Client Data Manager (formerly CsvLoader)

A WPF desktop application for importing, managing, and editing client data from CSV files. Built with .NET 6, Entity Framework Core, and SQL Server LocalDB.

## Overview

Client Data Manager is a Windows desktop application that simplifies the process of importing client/employee data from CSV files into a database. It features a user-friendly interface for selecting files, validating data, and managing client records with full CRUD operations.

## Features

- **CSV File Import**: Load one or multiple CSV files using an intuitive file selection dialog
- **Database Integration**: Automatically import CSV data into SQL Server LocalDB
- **Data Validation**: Built-in validation using FluentValidation to ensure data integrity
- **Record Management**: View, edit, and update client records with real-time validation
- **MVVM Architecture**: Clean separation of concerns using the Model-View-ViewModel pattern
- **Modular Design**: Organized into separate modules for CSV processing, user domain, and infrastructure

## Prerequisites

Before running the application, ensure you have:

- **Windows OS**: Windows 10 or later
- **.NET 6 SDK**: [Download here](https://dotnet.microsoft.com/download/dotnet/6.0)
- **Visual Studio 2022**: (recommended) with .NET desktop development workload
- **SQL Server LocalDB**: Usually included with Visual Studio

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/Kepeczsz/CsvLoader.git
   cd CsvLoader
   ```
   > **Note**: The repository is named `CsvLoader` but the application is now called "Client Data Manager"

2. **Open the solution**:
   ```bash
   cd csv_loader
   ```
   Open `csv_loader.sln` in Visual Studio 2022

3. **Restore NuGet packages**:
   Visual Studio will automatically restore packages, or run:
   ```bash
   dotnet restore
   ```

4. **Build the solution**:
   ```bash
   dotnet build
   ```

## Database Setup

The application uses SQL Server LocalDB with automatic database creation. The connection string is configured in `appsettings.json`:

```json
{
  "ConnectionStrings": {
    "AppDb": "Server=(localdb)\\MSSQLLocalDB; Database=Clients; Trusted_Connection=True;MultipleActiveResultSets=true"
  }
}
```

The database will be created automatically when you first run the application. Entity Framework Core migrations handle the schema creation.

## Usage

### Starting the Application

1. Run the application from Visual Studio (F5) or navigate to the solution directory and run:
   ```bash
   cd csv_loader
   dotnet run --project api/Modules.User.Application.csproj
   ```

2. The main window will appear:

   ![Main Window](https://github.com/Kepeczsz/CsvLoader/assets/52294433/035a9c7d-b253-4e69-a72c-806b73e4feca)

### Importing CSV Files

1. Click the **Load** button in the main window
2. The file selection window will open:

   ![File Selection](https://github.com/Kepeczsz/CsvLoader/assets/52294433/056cf96d-b2bb-4ba9-ac2a-e2cc6ecea7c4)

3. Click **Select file** to open the file dialog (filtered for CSV files)
4. Select one or more CSV files
5. The selected files will appear in the list:

   ![Selected Files](https://github.com/Kepeczsz/CsvLoader/assets/52294433/236c5ddd-999d-4d9b-bef7-d330e1c0f045)

6. **Double-click** on a file path to import it into the database
7. After import, the application displays the saved records with their database IDs

### Editing Records

1. Select a record from the list
2. Click **Edit Record**
3. The edit window opens with validation:

   ![Edit Record](https://github.com/Kepeczsz/CsvLoader/assets/52294433/cd00fb24-9a00-42f2-955b-0c6258eda7ff)

4. Modify the client information (Name, Surname, Email, Phone)
5. The application validates:
   - Client ID exists in the database
   - All required fields are properly filled
   - Data format is correct

   ![Validation](https://github.com/Kepeczsz/CsvLoader/assets/52294433/b32252f8-9e6e-4921-87c7-6c9380518c5f)

6. Click **Save** to update the record

### CSV File Format

The CSV files should follow this format:

```csv
id,name,surename,email,phone
420,John,Doe,john.doe@domain.com,1234567890
421,Jane,Smith,jane.smith@domain.com,9876543210
```

**Columns**:
- `id` - Unique client identifier (integer)
- `name` - First name (string)
- `surename` - Last name/surname (string) - Note: The CSV header uses "surename" which maps to the Surname property in the application
- `email` - Email address (string, validated)
- `phone` - Phone number (string)

## Project Structure

```
csv_loader/
├── api/                                    # Main WPF application
│   ├── Controllers/                        # Application controllers
│   ├── Views/                             # WPF views and windows
│   ├── ImportingClients/                  # Import logic and validation
│   ├── Shared/                            # Shared services
│   └── projectConfiguration/              # App settings
├── Infrastructure/                         # Data access layer
│   ├── Data/                              # DbContext
│   └── Migrations/                        # EF Core migrations
├── Modules.User.Domain/                   # Domain models
│   └── Client.cs                          # Client entity
├── Modules.Csv.Infrastructure/            # CSV processing module
└── Modules.Csv.Abstraction/               # CSV abstractions
```

## Technology Stack

- **Framework**: .NET 6.0 (Windows)
- **UI**: WPF (Windows Presentation Foundation)
- **Database**: Entity Framework Core 7.0 with SQL Server LocalDB
- **CSV Processing**: CsvHelper 30.0.1
- **Validation**: FluentValidation 11.5.2
- **Dependency Injection**: Microsoft.Extensions.DependencyInjection 7.0.0
- **Architecture**: MVVM (Model-View-ViewModel)

## Key Dependencies

```xml
<PackageReference Include="CsvHelper" Version="30.0.1" />
<PackageReference Include="FluentValidation" Version="11.5.2" />
<PackageReference Include="Microsoft.EntityFrameworkCore.SqlServer" Version="7.0.8" />
<PackageReference Include="Microsoft.Extensions.DependencyInjection" Version="7.0.0" />
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is available for educational and personal use.

## Author

Created by [Kepeczsz](https://github.com/Kepeczsz)

