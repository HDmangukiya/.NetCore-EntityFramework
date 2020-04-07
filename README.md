# .NetCore-EntityFramework
CRUD operation with .NetCore Entity framework

Steps:

1. Create Database using script.
2. Create a new project with ASP.NET Core Web Application template.
3. Select .NET Core and ASP.NET Core 3.0 and choose the Web Application (Model-View-Controller) template.
4. Install or Update(You dont need to download if you have already) nuget package
  4.1: Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design -Version 3.0.0-preview8-19413-06 
  4.2: Install-Package Microsoft.EntityFrameworkCore.Tools -Version 3.0.0-preview8.19405.11
  4.3: Install-Package Microsoft.EntityFrameworkCore.SqlServer -Version 3.0.0-preview8.19405.11
5. Scaffolding: Scaffold-DbContext “Server=ABCSERVER;Database=Inventory;Integrated Security=True” Microsoft.EntityFrameworkCore.SqlServer -    OutputDir Models
6. Open the Inventory Context class file. You will see the database credentials are hard coded in the OnConfiguring method.
   It’s not good practice to have SQL Server credentials in C# class, considering the security issues. So, remove this OnConfiguring method    from context file.
   
    // This method gets called by the runtime. Use this method to add services to the container.
        public void ConfigureServices(IServiceCollection services)
        {
            var connection = Configuration.GetConnectionString("InventoryDatabase");
            services.AddDbContext<InventoryContext>(options => options.UseSqlServer(connection));

            services.AddControllersWithViews();
        }
  7. And move the connection string to the appsettings.json file.
  
      "ConnectionStrings": {
      "InventoryDatabase": "Server=******;Database=Inventory;Trusted_Connection=True;"}
      
   8. Perform CRUD operations
      8.1 Addnew Controller and Select option "MVC new controller with views using Entity framework".
   
   9. Choose a database model class and data context class, which were created earlier, and click Add.
   10. Run application. 
   
   
   *******-------------Enjoy*******-------------
