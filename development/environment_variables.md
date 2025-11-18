# How to set an environment variable?

### Quick Powershell (temporary for current session)
If you want to set a temporarily environment variable (terminal session)

```Powershell
$env:NAME_OF_YOUR_ENV_VARIABLE = "your_api_key_here"
```

If you want to verify if the variable was created:
```Powershell
echo $env:NAME_OF_YOUR_ENV_VARIABLE
```

### Make it persistent (every new shell) - PS/CMD
```Powershell
setx NAME_OF_YOUR_ENV_VARIABLE = "your_api_key_here"
```

Verify if the variable exists 
```Powershell
echo $env:NAME_OF_YOUR_ENV_VARIABLE
```

### .env file

Alternatively, you can create an .env file an paste your variables in the file and locate it in the project you will use it.