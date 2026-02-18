# Windows build

### Clone the repositories

Clone the backend and frontend repositories and put it next to eachother:

![](assets/pHn58tZOqOmC58ylREY5L-h6sTJLEhK20HjB20dW9Co=.png)

### Frontend

![](assets/s_q7somZN8NF0uU9F9nL9-vuaFJSulLv_IS01bFJnOc=.png)

Run (Powershell Core):

```shellscript
npm install
```

![](assets/awDdb5DorvetVe-Ffcih7wnBWD-NCw8ijeMaR86urjI=.png)

Then:

```shellscript
npm run build-win
```

![](assets/LcoSjScNES7HUbMIep2bgGl86TeTj-9Xd7kddXeotUM=.png)





### Backend

Run (Powershell Core):

```shellscript
go mod download
go mod tidy
go build .
```

Set the variables in selfhosted.yaml and local.yaml for JWT secret

```yaml
jwt:
  secret: "change_this_to_a_secure_random_string_32_characters_long"
  session_time: 168h # 7 days
  max_refresh: 1440h # 60 days 
```

Copy the contents of the frontend build output to the backend repository:

```shellscript
cp -r ..\donetick-frontend\dist .\frontend
```

Run:

```shellscript
go run .
```

Should look something like this:

![](assets/L4lt3XWiFUN-xM3Xstt9oYIU7uTi-1--EYehu1GMUqs=.png)

Now you can access the frontend on http://localhost:2021 and the apis on the [http://localhost:2021/api/v1](http://localhost:2021)

### Swagger

Comment out these lines in main.go from this:

```go
	if cfg.Name == "local" {
		r.GET("/swagger/*any", ginSwagger.WrapHandler(swaggerFiles.Handler))
	}
```

To this:

```go
// if cfg.Name == "local" {
		r.GET("/swagger/*any", ginSwagger.WrapHandler(swaggerFiles.Handler))
	// }
```

Run this in the backend root:

```shellscript
swag init
```

Save the file and rebuild and run with:

```shellscript
go build.
go run
```

Navigate to http://localhost:2021/swagger/index.html

![](assets/OXcm05Hpioz4h3O1RD97oBEradScm8yC3Te1SkeqtFU=.png)

**Use the APIKey authorization!**

