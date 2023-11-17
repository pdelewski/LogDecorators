# TracingContextDecorator

Steps needed to use TracingContextDecorator

1) Clone repo `git clone https://github.com/pdelewski/TracingContextDecorator.git`
2) Add reference to your project `dotnet add reference [path to TracingContextRepo]/TracingContextDecorator.csproj`
3) Update your app.config file with log4net section. Below complete app.config

```
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <configSections>
        <section name="log4net" type="log4net.Config.Log4NetConfigurationSectionHandler, log4net" />
    </configSections>
    <log4net>
        <appender name="ConsoleAppender" type="log4net.Appender.ConsoleAppender" >
            <layout type="log4net.Layout.PatternLayout">
                <converter>
                    <name value="trace_id" />
                    <type value="SumoLogic.LoggingContext.TraceIdPatternConverter, TracingContextDecorator,Version=1.0.0, Culture=neutral, PublicKeyToken=null" />
                </converter>

                <converter>
                    <name value="span_id" />
                    <type value="SumoLogic.LoggingContext.SpanIdPatternConverter" />
                </converter>
                <converter>
                    <name value="parent_span_id" />
                    <type value="SumoLogic.LoggingContext.ParentSpanIdPatternConverter" />
                </converter>
                <conversionPattern value="%date %level %logger trace_id:%trace_id span_id:%span_id parent_span_id:%parent_span_id - %message%newline" />
            </layout>
        </appender>
        <root>
            <level value="INFO" />
            <appender-ref ref="ConsoleAppender" />
        </root>
    </log4net>
</configuration>
```

4) Rebuild project
