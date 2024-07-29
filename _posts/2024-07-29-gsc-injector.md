# GSC Injector
## 0x00 Clone Repo
```
git clone https://github.com/clee01/atian-cod-tools.git
```

## 0x01 Install Scoop
```
# Set PowerShell ExecutionPolicy
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

# Download Installation Script
irm get.scoop.sh -outfile 'install.ps1'

# Execute Installing, --ScoopDir specify Scoop installation path
.\install.ps1 -ScoopDir 'C:\Scoop'
```

## 0x02 Install premake5
```
scoop install premake
```

## 0x03 Install vcpkg
```
scoop install vcpkg
```

## 0x04 Create solution
To create the Visual Studio solution, you can then use this command in a powershell console
```
.\scripts\setup.ps1
```
It’ll create the solution into the build directory. You can open it using with **build/AtianCodTools.sln**.

## 0x05 Before Compile
### Add Lib Directory for AtianCodTools Solution
![image](https://github.com/user-attachments/assets/c40d47b0-d9e7-4eb2-87f5-f920cd0f6406)
![image](https://github.com/user-attachments/assets/6d6c75dc-fe48-4623-86c8-54b0a58ffb1b)
![image](https://github.com/user-attachments/assets/f5aee2c8-abc3-4258-9dca-628945a5e781)

### Specify Libs
![image](https://github.com/user-attachments/assets/18fe6de7-bad9-4cf7-8525-102db08138bf)
![image](https://github.com/user-attachments/assets/886e5e0c-9691-4905-9316-1d4719d4093b)
![image](https://github.com/user-attachments/assets/d64a96f2-ac79-46de-a301-cdf1ed1bc0ac)

## 0x06 Compile
The project should compile in **release** if the setup script was used.

It’ll create the different files into **build/bin/**.

![image](https://github.com/user-attachments/assets/f96b546b-87be-4715-a1f9-a25baa08e9c4)

> if you encountered this error, go to fix this error with the [issue](https://github.com/ladislav-zezula/CascLib/issues/202)

## 0x07[optional] Package installation
You can package an installation using the scripts
```
.\scripts\package.ps1
```
It’ll create an archive **build/package/acts.zip** containing the compiled files with the licenses.

## 0x08 Execute acts.exe
![image](https://github.com/user-attachments/assets/d886238d-28bf-4bdf-88b9-72fb349a6f41)
![image](https://github.com/user-attachments/assets/bf23361e-6e26-41c4-ad5a-c772ab45d459)
