| Recurso | Limite Predefinido | Limite Máximo |
| --- | --- | --- |
| Recursos por [grupo de recursos](../articles/azure-resource-manager/resource-group-overview.md#resource-groups) (por tipo de recurso) |800 |Varia por tipo de recurso |
| Implementações por grupo de recursos no histórico de implementação |800 |800 |
| Recursos por implementação |800 |800 |
| Bloqueios de gestão (por âmbito exclusivo) |20 |20 |
| Número de etiquetas (por recurso ou grupo de recursos) |15 |15 |
| Comprimento de chave da etiqueta |512 |512 |
| Comprimento do valor de etiqueta |256 |256 |


#### <a name="template-limits"></a>Limites de modelo

| Valor | Limite Predefinido | Limite Máximo |
| --- | --- | --- |
| Parâmetros |256 |256 |
| Variáveis |256 |256 |
| Recursos (incluindo contagem de cópia) |800 |800 |
| saídas |64 |64 |
| Expressão de modelo |24,576 carateres |24,576 carateres |
| Recursos nos modelos exportados |200 |200 | 
| Tamanho do modelo |1 MB |1 MB |
| Tamanho do ficheiro de parâmetro |64 KB |64 KB |

Pode exceder alguns limites de modelo ao utilizar um modelo aninhado. Para obter mais informações, consulte [utilizar modelos ligados ao implementar os recursos do Azure](../articles/azure-resource-manager/resource-group-linked-templates.md). Para reduzir o número de parâmetros, variáveis ou saídas, pode combinar vários valores para um objeto. Para obter mais informações, consulte [objetos como parâmetros](../articles/azure-resource-manager/resource-manager-objects-as-parameters.md).

Se atingir o limite de 800 implementações por grupo de recursos, elimine as implementações de histórico que já não são necessárias. Pode eliminar as entradas do histórico com [eliminar a implementação do grupo az](/cli/azure/group/deployment#az_group_deployment_delete) para a CLI do Azure, ou [Remove-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/remove-azurermresourcegroupdeployment) no PowerShell. Eliminar uma entrada do histórico de implementação não afeta os recursos de implementar. 