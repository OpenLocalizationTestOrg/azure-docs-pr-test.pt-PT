Coleção de medidas personalizadas. Utilize este tooreport de coleção com o nome associada ao item de telemetria de Olá de medida. Casos de utilização típicos são:
- tamanho de Olá do payload de telemetria de dependência
- número de Olá de itens de fila processados pelo pedido de telemetria
- tempo desse cliente demorou toocomplete Olá passo na conclusão do passo do Assistente para eventos de telemetria.

Pode consultar [medidas personalizadas](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) na análise de aplicação:

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > Medidas personalizadas estão associadas a itens de telemetria de Olá pertencem a. São requerente toosampling com itens de telemetria de Olá que contenha esses valores. tootrack uma medida que tem um valor independente dos outros tipos de telemetria, utilização [telemetria métrica](../articles/application-insights/app-insights-api-custom-events-metrics.md).

Comprimento de chave máximo: 150
