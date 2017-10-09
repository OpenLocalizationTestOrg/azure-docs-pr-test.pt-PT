Aplicar etiquetas tooyour recursos do Azure toologically organizá-los por categorias. Cada etiqueta é constituída por um nome e um valor. Por exemplo, pode aplicar nome Olá "Ambiente" e de recursos do Olá valor "Production" tooall Olá na produção. Sem esta etiqueta, poderá ter dificuldades em identificar se um recurso se destina a desenvolvimento, teste ou produção. No entanto, "Ambiente" e "Produção" são apenas exemplos. Definir valores que façam Olá mais sentido para organizar a sua subscrição e nomes de Olá.

Depois de aplicar etiquetas, pode obter todos os recursos de Olá na sua subscrição com esse nome de etiqueta e o valor. Ativar de etiquetas tooretrieve relacionadas com recursos que residem em grupos de recursos diferentes. Esta abordagem é útil se necessitar de tooorganize recursos de gestão ou de faturação.

Olá seguintes limitações aplicam-se tootags:

* Cada recurso ou grupo de recursos pode ter um máximo de 15 pares de nomes/valores de etiquetas. Esta limitação aplica-se apenas recurso ou grupo de recursos de toohello tootags diretamente aplicado. Um grupo de recursos pode conter muitos recursos que tenham, cada um, 15 pares de nomes/valores de etiqueta. 
* o nome da etiqueta Olá é limitado too512 carateres e o valor de etiqueta Olá é limitado too256 carateres. Para contas de armazenamento, o nome da etiqueta Olá é limitado too128 carateres e o valor de etiqueta Olá é limitado too256 carateres.
* Grupo de recursos de toohello etiquetas aplicados não são herdadas pelo recursos Olá nesse grupo de recursos. 

Se tiver mais do que 15 valores que precisa de tooassociate com um recurso, utilize uma cadeia JSON para o valor de etiqueta Olá. Olá cadeia JSON pode conter muitos valores que são aplicados tooa nome de etiqueta única. Este artigo mostra um exemplo de atribuir uma etiqueta de toohello de cadeia JSON.
