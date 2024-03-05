# react-with-windows-authentication
react.js + Asp.net Core 8 + windows Authentication
The initial project is without Windows authentication. then we add Windows authentication for user login.
1. initialize the project with Visual Studio 2022 template.
2. set "WindowsAutentication": true in the launchSetting.json in the server project.
3. Add Negotiate package
   ``` 
   Install-Package Microsoft.AspNetCore.Authentication.Negotiate
   ```
5. add the service to the Program.cs
    ```C#
    builder.Services.AddAuthentication(NegotiateDefaults.AuthenticationScheme).AddNegotiate();
      builder.Services.AddAuthorization(options =>
      {
          // By default, all incoming requests will be authorized according to the default policy.
          options.FallbackPolicy = options.DefaultPolicy;
      });
   ```
6. By default for IIS, you don't need the following code. but you can add it.
   ```
      app.UseAuthentication();
      app.UseAuthorization();
   ```
7. add the following code in your controller to test
   ```C#
    var user = HttpContext.User?.Identity?.Name ?? "N/A";
   ```
8. In the production environment, do not forget to set the IIS 
