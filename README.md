# Yinyang Utilities Npgsql

[![Yinyang Utilities Npgsql](https://img.shields.io/nuget/v/Yinyang.Utilities.Npgsql.svg)](https://www.nuget.org/packages/Yinyang.Utilities.Npgsql/)


Wrapper for Npgsql.

Npgsqlラッパーです。

---

## Getting started

Install Yinyang Utilities Npgsql nuget package.

NuGet パッケージ マネージャーからインストールしてください。

- [Npgsql](https://www.nuget.org/packages/Yinyang.Utilities.Npgsql/)

> ```powershell
> Install-Package Yinyang.Utilities.Npgsql
> ```

---

## Basic Usage

```c#
// Init
using var db = new Pgsql(ConnectionString);

// Database Open
db.Open();

// Transaction Start
db.BeginTransaction();

// SQL
db.CommandText = "INSERT INTO test2 VALUES(@id, @value)";

// Add Parameter
db.AddParameter("@id", 1);
db.AddParameter("@value", "abcdefg");

// Execute
if (1 != db.ExecuteNonQuery())
{
    // Transaction Rollback
    db.Rollback();
    return;
}

// Command and Parameter Reset
db.Refresh();

// SQL
db.CommandText = "select * from test2 where id = @id;";

// Add Parameter
db.AddParameter("@id", 1);

// Execute
var result = db.ExecuteReaderFirst<Entity>();

if (null == result)
{
    db.Rollback();
    return;
}

// Transaction Commit
db.Commit();

// Database Close
db.Close();


```

## Samples

See Sample project.
