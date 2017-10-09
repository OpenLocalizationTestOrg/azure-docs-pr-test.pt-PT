Agora que tem de adicionar um acionador, o respetivo toodo tempo algo interessante com dados de Olá que são gerados pelo acionador Olá. Siga estes passos tooadd um Olá **SFTP - extrair pasta** ação. Esta ação extrair os conteúdos de Olá de um ficheiro, se forem satisfeitas as condições de Olá definidas. 

tooconfigure Olá esta ação, terá de Olá tooprovide informações a seguir. Vai notar que é gerados pelo acionador Olá como entrada para algumas das propriedades de Olá para o novo ficheiro de Olá de dados de toouse fácil:

| SFTP - propriedade de pasta extract | Descrição |
| --- | --- |
| Caminho de ficheiro do arquivo de origem |Este é o caminho de Olá para o ficheiro de Olá que está a ser extraído. Pode selecionar um dos Olá tokens a partir de uma ação anterior ou procurar o caminho de ficheiro de Olá servidor toofind Olá SFTP. |
| Caminho da pasta de destino |Este é o caminho de olá onde irão ser colocados ficheiros de Olá extraído. Pode selecionar um dos tokens Olá de uma ação anterior como caminho de destino Olá ou procurar o servidor SFTP Olá e selecione um caminho. |
| Substituir? |Indica se um ficheiro com Olá mesmo nome como ficheiros extraídos Olá se encontra no caminho de pasta de destino Olá se o ficheiro existente Olá deve ser substituído ou não. |

Vamos começar a adicionar os ficheiros do Olá ação tooextract Olá se a condição de Olá definida anteriormente avalia demasiado*verdadeiro*. 

1. Selecione **adicionar uma ação**.        
   ![Imagem de condição de ação de SFTP 6](./media/connectors-create-api-sftp/condition-6.png)   
2. Selecione Olá **SFTP - extrair pasta** ação      
   ![Imagem de condição de ação de SFTP 7](./media/connectors-create-api-sftp/condition-7.png)   
3. Selecione **caminho de ficheiro do arquivo de origem**              
   ![Imagem de condição de ação de SFTP 9](./media/connectors-create-api-sftp/condition-9.png)   
4. Selecione Olá **caminho do ficheiro** token. Isto indica que utiliza o caminho de ficheiro de Olá de ficheiro Olá Olá acionador foi encontrada como caminho de ficheiro de arquivo de origem Olá.           
   ![Imagem de condição de ação de SFTP 10](./media/connectors-create-api-sftp/condition-10.png)   
5. Selecione **caminho da pasta de destino**           
   ![Imagem de condição de ação de SFTP 11](./media/connectors-create-api-sftp/condition-11.png)   
6. Selecione Olá **caminho do ficheiro** token. Isto indica que utiliza o caminho de ficheiro de Olá de ficheiro Olá Olá acionador foi encontrada como caminho de destino Olá para ficheiros de Olá extraído.   
7. Introduza *\ExtractedFile* no Olá **caminho da pasta de destino** controlo. Fazê-lo imediatamente após o token de caminho de ficheiro Olá no Olá controlo de caminho de pasta de destino.         
   ![Imagem de condição de ação de SFTP 12](./media/connectors-create-api-sftp/condition-12.png)   
8. Introduza *verdadeiro* no Olá **substituir?* tooindicate de controlo que ficheiros existentes devem ser substituídos se tiverem o mesmo nome como Olá de Olá extraídos os ficheiros.      
   ![Imagem de condição de ação de SFTP 13](./media/connectors-create-api-sftp/condition-13.png)   
9. Guardar o fluxo de trabalho do Olá alterações tooyour  

