# Study Jetbrains Rider + Unit Tests

Study case of Jetbrains Rider cross platform .NET IDE using .NET Core + Unit Tests

## Dependencies

- **apt-transport-https**

```sh
sudo apt-get update
sudo apt-get install apt-transport-https
```

- Install JetBrains Rider

- Download and install : https://www.jetbrains.com/rider/download/

- Install .NET Core SDK

```sh
sudo apt-get install dotnet-sdk-3.1
```

- Install ASP.NET Core Runtime

```sh
sudo apt-get install aspnetcore-runtime-3.1
```

- Install .NET Core Runtime

```sh
sudo apt-get update
sudo apt-get install dotnet-runtime-3.1
```

## Steps to reproduce

### Create Origin Project

- Create new Solutions

```sh
dotnet new sln
```

- Create classlib PrimeService

```sh
dotnet new classlib -n PrimeService && cd PrimeService
```

- Rename Class1.cs to PrimeService.cs

```sh
mv Class1.cs PrimeService.cs
```

- Create PrimeService method

```sh
using System;

namespace Prime.Services
{
    public class PrimeService
    {
        public bool IsPrime(int candidate)
        {
            throw new NotImplementedException("Please create a test first.");
        }
    }
}
```

- Inside root of project type the command `dotnet sln add PrimeService/PrimeService.csproj`

### Create Test Project

- In project's root folder, create new nUnit Test

```sh
dotnet new nunit -n PrimeService.Test && cd PrimeService.Test
```

- Add Reference so PrimeService Project

```sh
dotnet add reference ../PrimeService/PrimeService.csproj
```

- In project's root folder, add Project to solution

```sh
dotnet sln add ./PrimeService.Test/PrimeService.Test.csproj
```

### Creating Test

- Inside folder **PrimeService.Tests** rename the file **UnitTest1.cs**  to **PrimeService_IsPrimeShould.cs**
- Set content below

```sh
using NUnit.Framework;
using Prime.Services;

namespace Prime.UnitTests.Services
{
    [TestFixture]
    public class PrimeService_IsPrimeShould
    {
        [Test]
        public void IsPrime_InputIs1_ReturnFalse()
        {
            PrimeService primeService = CreatePrimeService();
            var result = primeService.IsPrime(1);

            Assert.IsFalse(result, "1 should not be prime");
        }

        private PrimeService CreatePrimeService()
        {
             return new PrimeService();
        }
    }
}
```

The **[TestFixture]** attribute indicates a class that contains unit tests. 

The **[Test]** attribute indicates a method that is a test method.

- Run the test

**Note** It will crash because test is not implemented yet.

- Change PrimeService.cs **IsPrime** method to:

```sh
public bool IsPrime(int candidate)
{
    if (candidate == 1)
    {
        return false;
    }
    throw new NotImplementedException("Please create a test first.");
} 
``` 

## References

- [.NET Core Unit Tests](https://docs.microsoft.com/pt-br/dotnet/core/testing/unit-testing-with-dotnet-test)
- [.NET Core](https://dotnet.microsoft.com/download)
- [.NET Core + Ubuntu](https://docs.microsoft.com/pt-br/dotnet/core/install/linux-package-manager-ubuntu-1904)
