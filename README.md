# Dummy-app-DotNet

Monorepo workspace .NET 8 yang dirancang untuk mendemonstrasikan struktur multi-project suite, mencakup REST Web API, WebApp (Razor Pages), Blazor UI, dan Shared Class Library.

---

## 📁 Struktur Monorepo

```text
ProtelindoDotNetSuite/
├── ProtelindoDotNetSuite.sln   # File Solution utama (Dibuikd oleh CI/CD)
├── MyWebApi/                  # RESTful API Service (Backend)
├── MyWebApp/                  # ASP.NET Core Razor Pages (Frontend SSR)
├── MyBlazorApp/               # Blazor Web App (Frontend C# Fullstack)
└── MyClassLib/                # Shared Class Library (.dll re-usable)

```

---

## 🛠️ Prasyarat

* [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0?utm_source=gemini)
* Docker Desktop / WSL (Opsional, untuk containerization)

---

## 🚀 Panduan Setup & Inisialisasi

Jika kamu meng-clone repository ini dari awal atau ingin menyusun kodenya kembali:

### 1. Inisialisasi Solution

```bash
mkdir ProtelindoDotNetSuite && cd ProtelindoDotNetSuite
dotnet new sln -n ProtelindoDotNetSuite

```

### 2. Generate Sub-Project

```bash
dotnet new webapi -n MyWebApi
dotnet new webapp -n MyWebApp
dotnet new blazor -n MyBlazorApp
dotnet new classlib -n MyClassLib

```

### 3. Registrasi & Linking Project

```bash
# Daftarkan semua project ke file solution (.sln)
dotnet sln add MyWebApi/MyWebApi.csproj
dotnet sln add MyWebApp/MyWebApp.csproj
dotnet sln add MyBlazorApp/MyBlazorApp.csproj
dotnet sln add MyClassLib/MyClassLib.csproj

# Hubungkan Shared Class Library ke Web API
dotnet add MyWebApi/MyWebApi.csproj reference MyClassLib/MyClassLib.csproj

```

---

## 🔨 Build & Menjalankan Aplikasi

### Build Seluruh Solution (CI/CD Ready)

```bash
dotnet build

```

### Menjalankan Masing-Masing Aplikasi

* **Web API:**
```bash
dotnet run --project MyWebApi

```


* Endpoint Root: `http://localhost:5059/`
* Weather Forecast API: `http://localhost:5059/weatherforecast`


* **WebApp (Razor Pages):**
```bash
dotnet run --project MyWebApp

```


* **Blazor App:**
```bash
dotnet run --project MyBlazorApp

```



---

## 💡 Konfigurasi Tambahan

Untuk mencegah error `404 Not Found` saat mengakses path root `/` pada Web API, pastikan route dasar berikut terdaftar di `MyWebApi/Program.cs`:

```csharp
app.MapGet("/", () => "Protelindo Web API is Running!");

```