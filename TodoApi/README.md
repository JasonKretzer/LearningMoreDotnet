# Todo Api in .NET Core 3.1

A list of the commands used to create this project.

First, I created the project itself which creates a directory called TodoApi

    dotnet new webapi -o TodoApi

Then inside that directory, add the EF Core Nuget packages for database functionality

    dotnet add package Microsoft.EntityFrameworkCore.SqlServer
    
    dotnet add package Microsoft.EntityFrameworkCore.InMemory

When you create a webapi, a sample endpoint is created for you to pattern after.  

_**NOTE of Unexpected Behavior #1:**_ At this point, VS Code may ask you to install some Assets, select YES for this. It will modify some files but it is fine.

We can now attempt to hit the sample endpoint which is defined in the WeatherForecast.cs file.

In VS Code, start up a local debug server using Ctrl+F5 and then use a browser to go to

    <https://localhost:5001/WeatherForecast>

A browser may try to open up and it will take you to the localhost:5001 but nothing will be there.  I just added the /WeatherForecast at the end of the url and received some json.

    [
        {
            "date":"2020-10-26T08:32:1
            4.2864525-04:00",
            "temperatureC":30,
            "temperatureF":85,
            "summary":"Bracing"
        },
        {
            "date":"2020-10-27T08:32:1
            4.2864721-04:00",
            "temperatureC":-18,
            "temperatureF":0,
            "summary":"Cool"
        },
        {
            "date":"2020-10-28T08:32:1
            4.2864727-04:00",
            "temperatureC":42,
            "temperatureF":107,
            "summary":"Chilly"
        },
        {
            "date":"2020-10-29T08:32:1
            4.286473-04:00",
            "temperatureC":46,
            "temperatureF":114,
            "summary":"Scorching"
        },
        {
            "date":"2020-10-30T08:32:1
            4.2864733-04:00",
            "temperatureC":36,
            "temperatureF":96,
            "summary":"Bracing"
        }
    ]

I stopped the debugger and added a model class for a TodoItem.  I will create a Models directory for it.

It is interesting to note here that the tutorial does not show a CLI command to generate the scaffolding for a Model class as there is in some other technology stacks.

Another interesting thing here is that in the tutorial, the TodoItem code does not include the namespace.  I will add it later if necessary.

Next it is time to set up the Database Context which will provide the connection between our model classes and the database.  Again, the tutorial does not show a CLI command for this.  In the same Models folder, I will create a new class called TodoContext. It will extend the DbContext class.  Inside there is a DbSet property that contains a collection of TodoItem objects.

>Think about it this way. A table in a database has rows.  Each row uniquely identifies information about a single item.  Mutiple items equals multiple rows.  In the same way, the DbSet has multiple TodoItems. Each item uniquely identifies information about a single TodoItem.  By convention, we name the DbSet property as the plural form of the items it contains -- TodoItems.

_**NOTE of Unexpected Behavior #2:**_ At this point VS Code was telling me there were problems all over the code. I had squigglies in a number of files.  Almost all of the problems were of the "XYZ does not exist in the namespace 'Microsoft.AspNetCore..." or that "The type XYZ is defined in an assembly that is not referenced. You must add a reference..."  I think it is a problem with how the Omnisharp does its thing.  I did not find a quick solution and the code still runs, so I ignored them.

