# Hangfire RavenDB

[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=ops-ai_hangfire-ravendb&metric=alert_status)](https://sonarcloud.io/dashboard?id=ops-ai_hangfire-ravendb)
[![Build Status](https://opsai.visualstudio.com/BeyondAuth/_apis/build/status/ops-ai.Hangfire.Contrib.RavenDB?branchName=develop)](https://opsai.visualstudio.com/BeyondAuth/_build/latest?definitionId=6&branchName=develop)
[![Vulnerabilities](https://sonarcloud.io/api/project_badges/measure?project=ops-ai_hangfire-ravendb&metric=vulnerabilities)](https://sonarcloud.io/dashboard?id=ops-ai_hangfire-ravendb)
[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=ops-ai_hangfire-ravendb&metric=coverage)](https://sonarcloud.io/dashboard?id=ops-ai_hangfire-ravendb)
![CodeQL](https://github.com/ops-ai/Hangfire.Contrib.RavenDB/workflows/CodeQL/badge.svg)

[![NuGet Status](https://img.shields.io/nuget/v/Hangfire.Contrib.RavenDB.svg?style=flat)](https://www.nuget.org/packages/Hangfire.Contrib.RavenDB/)
[![NuGet Count](https://img.shields.io/nuget/dt/Hangfire.Contrib.RavenDB.svg)](https://www.nuget.org/packages/Hangfire.Contrib.RavenDB/)

## Overview

RavenDB job storage for Hangfire

## Usage

This is how you connect to a ravendb server (local or remote)
```csharp
GlobalConfiguration.Configuration.UseRavenStorage("connection_string", "database_name");
```

This is how you connect to an embedded ravendb instance
```csharp
GlobalConfiguration.Configuration.UseEmbeddedRavenStorage();
```

To enqueue a background job you must have the following in the code somewhere at least once or the background job queue will not process
```csharp
var client = new BackgroundJobServer();
\\then you can do this, which runs once
BackgroundJob.Enqueue(() => Console.WriteLine("Background Job: Hello, world!"));
```

[**Delayed tasks**](http://docs.hangfire.io/en/latest/users-guide/background-methods/calling-methods-with-delay.html)

Scheduled background jobs are being executed only after given amount of time.

```csharp
BackgroundJob.Schedule(() => Console.WriteLine("Reliable!"), TimeSpan.FromDays(7));
```

[**Recurring tasks**](http://docs.hangfire.io/en/latest/users-guide/background-methods/performing-recurrent-tasks.html)

Recurring jobs were never been simpler, just call the following method to perform any kind of recurring task using the [CRON expressions](http://en.wikipedia.org/wiki/Cron#CRON_expression).

```csharp
RecurringJob.AddOrUpdate(() => Console.WriteLine("Transparent!"), Cron.Daily);
```

## Continuations

Continuations allow you to define complex workflows by chaining multiple background jobs together.

```csharp
var id = BackgroundJob.Enqueue(() => Console.WriteLine("Hello, "));
BackgroundJob.ContinueWith(id, () => Console.WriteLine("world!"));
```

## License

Copyright © 2013-2014 Sergey Odinokov.

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Lesser General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License
along with this program.  If not, see [http://www.gnu.org/licenses/](http://www.gnu.org/licenses).

## Known Bugs

