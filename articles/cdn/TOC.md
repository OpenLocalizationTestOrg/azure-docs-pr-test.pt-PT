# [Descrição geral](cdn-overview.md)
## [O que é o Azure CDN?](../best-practices-cdn.md?toc=%2fazure%2fcdn%2ftoc.json)

# Introdução
## [Ativar o Azure CDN](cdn-create-new-endpoint.md)

# Procedimento
## Integrar
### [Aplicações Web](../app-service/app-service-web-tutorial-content-delivery-network.md?toc=%2fazure%2fcdn%2ftoc.json)
### [Serviços Cloud](cdn-cloud-service-with-cdn.md)
### Armazenamento
#### [Criar uma conta de armazenamento](cdn-create-a-storage-account-with-cdn.md)
#### [Suporte de armazenamento de SAS](cdn-sas-storage-support.md)
### [Partilha de recursos de várias origens](cdn-cors.md)
### [Adicionar um domínio personalizado ao ponto final de CDN](cdn-map-content-to-custom-domain.md)
### [Configurar HTTPS num domínio personalizado](cdn-custom-ssl.md)
## Otimizar o conteúdo
### [Descrição geral da otimização](cdn-optimization-overview.md)
####[Otimização de ficheiros grandes](cdn-large-file-optimization.md)
####[Otimização da transmissão em fluxo de multimédia](cdn-media-streaming-optimization.md)
####[Aceleração de site dinâmico](cdn-dynamic-site-acceleration.md)
 
## Gerir
### [Gerir com o Azure PowerShell](cdn-manage-powershell.md)
### [Restringir acesso por país](cdn-restrict-access-by-country.md)
### [Comprimir ficheiros para melhorar o desempenho](cdn-improve-performance.md)
### Controlo de comportamento de colocação em cache
#### [Como funciona a colocação em cache](cdn-how-caching-works.md)
#### [Controlar o comportamento da colocação em cache com as regras de cache](cdn-caching-rules.md)
#### Conteúdo de cache por cadeias de consulta
##### [Escalão Standard](cdn-query-string.md)
##### [Escalão Premium](cdn-query-string-premium.md)
#### [Remover ativos em cache](cdn-purge-endpoint.md)
#### [Pré-carregar ativos em cache](cdn-preload-endpoint.md)
### Configurar time-to-live
#### [Conteúdo Web do Azure](cdn-manage-expiration-of-cloud-service-content.md)
#### [Armazenamento de Blobs do Azure](cdn-manage-expiration-of-blob-content.md)
### [Autenticação de tokens](cdn-token-auth.md)
### [Monitorizar recursos](cdn-resource-health.md)
### [Substituir comportamento por regras](cdn-rules-engine.md)
### [Receber alertas em tempo real](cdn-real-time-alerts.md)
### [Suporte HTTP/2](cdn-http2.md)

## Analisar
### [Analisar padrões de utilização da CDN do Azure](cdn-log-analysis.md)
#### [Registos de diagnóstico do Azure](cdn-azure-diagnostic-logs.md)
#### Ferramentas de análise para CDN do Azure a partir da Verizon
##### [Relatórios de núcleos da Verizon](cdn-analyze-usage-patterns.md)
##### [Relatórios personalizados da Verizon](cdn-verizon-custom-reports.md)
#### Ferramentas de análise para CDN Premium do Azure a partir da Verizon
##### [Gerar relatórios HTTP avançados](cdn-advanced-http-reports.md)
##### [Ver estatísticas em tempo real](cdn-real-time-stats.md)
##### [Analisar o desempenho de nó edge](cdn-edge-performance.md)

## Programar
### [.NET](cdn-app-dev-net.md)
### [Node.js](cdn-app-dev-node.md)

## Resolução de problemas
### [estado 404](cdn-troubleshoot-endpoint.md)
### [Compressão de ficheiros](cdn-troubleshoot-compression.md)

# Referência
## [Exemplos de código](https://azure.microsoft.com/en-us/resources/samples/?service=cdn)
## [Azure PowerShell](/powershell/module/azurerm.cdn)
## [.NET](/dotnet/api/microsoft.azure.management.cdn)
## [Java](/java/api/com.microsoft.azure.management.cdn)
## [REST](/rest/api/cdn/)

# Recursos
##  [Referência do Motor de Regras](cdn-rules-engine-reference.md)
### [Expressões condicionais do Motor de Regras](cdn-rules-engine-reference-conditional-expressions.md)
### [Funcionalidades do Motor de Regras](cdn-rules-engine-reference-features.md)
### [Condições de correspondência do Motor de Regras](cdn-rules-engine-reference-match-conditions.md)
## [Localizações POP da CDN do Azure](cdn-pop-locations.md)
## [Mapa do Azure](https://azure.microsoft.com/roadmap/)
## [Fórum do MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurecdn)
## [Preços](https://azure.microsoft.com/pricing/details/cdn/)
## [Calculadora de preços](https://azure.microsoft.com/pricing/calculator/)
## [Atualizações de serviço](https://azure.microsoft.com/updates/?product=cdn)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-cdn)
## [Vídeos](https://azure.microsoft.com/documentation/videos/index/?services=cdn)

