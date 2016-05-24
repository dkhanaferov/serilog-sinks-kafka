# Serilog.Sinks.Kafka [![Build status](https://ci.appveyor.com/api/projects/status/34ja7i5rnveewjq8?svg=true)](https://ci.appveyor.com/project/wespday/serilog-sinks-kafka)

A [Serilog](http://serilog.net/) [sink](https://github.com/serilog/serilog/wiki/Provided-Sinks) that writes events to [Kafka](http://kafka.apache.org/).

## Overview

The Serilog Kafka sink project is a sink (basically a writer) for the Serilog logging framework.
Structured log events are written to sinks and each sink is responsible for writing to its own backend, 
database, store etc.
This sink delivers the data to Apache Kafka which is a publish-subscribe messaging system.

## Quick start

Install the **Serilog.Sinks.Kafka** NuGet package.

Create a logger and start logging messages:

```csharp
    using System;
    using Serilog;

    public void KafkaConnectionTest()
    {
        var log = new LoggerConfiguration()
            .WriteTo
            .Kafka(new KafkaSinkOptions(topic: "test", brokers: new[] { new Uri("http://localhost:9092") }))
            .CreateLogger();

        log.Information(
            "The execution time of this test is  {@now}", 
            new { DateTimeOffset.Now.Hour, DateTimeOffset.Now.Minute });

        Assert.IsTrue(true);
    }
```

Publishes a message like this:

```json
{
  "Timestamp": "2016-05-24T11:50:13.3539190-05:00",
  "Level": "Information",
  "MessageTemplate": "The execution time of this test is  {@now}",
  "Properties": {
    "now": {
      "Hour": 11,
      "Minute": 50
    }
  }
}
```
