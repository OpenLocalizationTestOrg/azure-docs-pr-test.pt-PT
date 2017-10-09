## <a name="using-vault-credentials-tooauthenticate-with-hello-azure-backup-service"></a>Utilizar tooauthenticate de credenciais de cofre com Olá serviço de cópia de segurança do Azure
servidor de no local de Olá (cliente Windows ou servidor Windows Server ou do Data Protection Manager) tem de toobe autenticado com um cofre de cópia de segurança antes-pode criar cópias de segurança tooAzure de dados. autenticação de Olá é conseguida utilizando "as credenciais do cofre". conceito de Olá de credenciais do Cofre é semelhante toohello conceito de um ficheiro de "publicar definições" que é utilizado no Azure PowerShell.

### <a name="what-is-hello-vault-credential-file"></a>O que é o ficheiro de credenciais de cofre Olá?
o ficheiro de credenciais do cofre Olá é um certificado gerado pelo portal Olá para cada Cofre de cópia de segurança. portal de Olá, em seguida, carrega toohello de chave pública de Olá serviço de controlo de acesso (ACS). chave privada do Olá do certificado de Olá é efetuada utilizador toohello disponível como parte do fluxo de trabalho de Olá que está indicado como uma entrada no fluxo de trabalho do Olá máquina registo. Isto efetua a autenticação Olá máquina toosend dados de cópia de segurança tooan identificado cofre Olá serviço cópia de segurança do Azure.

credenciais de cofre Hello são utilizadas apenas durante o fluxo de trabalho do Olá registo. É tooensure de responsabilidade do utilizador Olá que Olá as credenciais do cofre ficheiro não fiquem comprometido. Se ficarem Olá às mãos de qualquer utilizador não autorizado, o ficheiro de credenciais de cofre Olá pode ser utilizado tooregister outras máquinas contra Olá mesmo cofre. No entanto, como dados de cópia de segurança de Olá são encriptados utilizando uma frase de acesso que pertence toohello cliente, os dados de cópia de segurança existentes não podem ficar comprometidos. toomitigate com esta preocupação, as credenciais do cofre estão definidas tooexpire no 48hrs. Pode transferir as credenciais do cofre Olá de um cofre de cópia de segurança qualquer número de vezes, mas apenas Olá ficheiro mais recente cofre credencial é aplicável durante o fluxo de trabalho do Olá registo.

### <a name="download-hello-vault-credential-file"></a>Transferir o ficheiro de credenciais de cofre Olá
o ficheiro de credenciais do cofre Olá é transferido através de um canal seguro do Olá portal do Azure. Olá serviço de cópia de segurança do Azure não tem conhecimento da chave privada do certificado de Olá da Olá e chave privada Olá não é continuada no portal de Olá ou serviço Olá. Utilize Olá os seguintes passos toodownload Olá cofre credencial ficheiro tooa computador local.

1. Inicie sessão no toohello [Portal de gestão](https://manage.windowsazure.com/)
2. Clique em **dos serviços de recuperação** no painel de navegação esquerdo Olá e Cofre de cópias de segurança de Olá selecione que criou. Clique em Olá nuvem ícone tooget toohello vista de início rápido do Cofre de cópias de segurança de Olá.
   
   ![Vista rápida](./media/backup-download-credentials/quickview.png)
3. Na página de início rápido de Olá, clique em **as credenciais do Cofre de transferência**. portal Olá gera o ficheiro de credenciais do Olá cofre, que é disponibilizado para transferência.
   
   ![Transferência](./media/backup-download-credentials/downloadvc.png)
4. portal de Olá irá gerar uma credencial do cofre utilizando uma combinação de nome do cofre Olá e Olá data atual. Clique em **guardar** toodownload Olá cofre credenciais toohello conta local transfere pasta ou selecione guardar como de Olá guardar menu toospecify uma localização para as credenciais do cofre Olá.

### <a name="note"></a>Nota
* Certifique-se de que as credenciais do cofre Olá é guardado numa localização que pode ser acedida a partir do seu computador. Se esta está armazenada numa partilha de ficheiros/SMB, verifique as permissões de acesso de Olá.
* o ficheiro de credenciais do cofre hello é utilizado apenas durante o fluxo de trabalho do Olá registo.
* o ficheiro de credenciais do cofre Olá expira após 48hrs e pode ser transferido a partir do portal de Olá.
* Consulte toohello cópia de segurança do Azure [FAQ](../articles/backup/backup-azure-backup-faq.md) para quaisquer perguntas sobre o fluxo de trabalho Olá.

