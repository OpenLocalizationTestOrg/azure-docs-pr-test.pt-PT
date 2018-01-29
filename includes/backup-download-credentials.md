## <a name="using-vault-credentials-to-authenticate-with-the-azure-backup-service"></a>Utilizar as credenciais do cofre para autenticar com o serviço de cópia de segurança do Azure
Antes de pode criar cópias de segurança um servidor no local (cliente Windows ou servidor Windows Server ou do Data Protection Manager) para o Azure, autentica o servidor com um cofre dos serviços de recuperação. Utilize um ficheiro de credenciais do cofre para autenticar o servidor com o Azure. As credenciais do cofre são semelhantes ao conceito de um ficheiro de "publicar definições" utilizado no Azure PowerShell.

### <a name="what-is-the-vault-credential-file"></a>O que é o ficheiro de credenciais do cofre?
O ficheiro de credenciais do cofre é um certificado gerado pelo portal para cada cofre de cópia de segurança. O portal, em seguida, carrega a chave pública para o Access Control Service (ACS). A chave privada do certificado é disponibilizada para o utilizador como parte do fluxo de trabalho que está indicado como uma entrada no fluxo de trabalho de registo da máquina. Isto autentica a máquina para enviar dados de cópia de segurança para um cofre identificado no serviço de cópia de segurança do Azure.

As credenciais do cofre são utilizadas apenas durante o fluxo de trabalho do registo. É da responsabilidade do utilizador para se certificar de que o ficheiro de credenciais do Cofre não fiquem comprometido. Se ficarem às mãos de qualquer utilizador não autorizado, o ficheiro de credenciais do cofre pode ser utilizado para registar outras máquinas contra o mesmo cofre. No entanto, como os dados de cópia de segurança são encriptados utilizando uma frase de acesso que pertence ao cliente, os dados de cópia de segurança existentes não podem ficar comprometidos. Para atenuar esta preocupação, as credenciais do cofre estão definidas para expirar em 48hrs. Pode transferir as credenciais do Cofre de um cofre de cópia de segurança qualquer número de vezes, mas apenas o ficheiro de credenciais de cofre mais recente é aplicável durante o fluxo de trabalho do registo.

### <a name="download-the-vault-credential-file"></a>Transfira o ficheiro de credenciais do Cofre
O ficheiro de credenciais do Cofre é transferido através de um canal seguro do portal do Azure. O serviço de cópia de segurança do Azure não tem conhecimento da chave privada do certificado e a chave privada não é continuada no portal ou o serviço. Utilize os seguintes passos para transferir o ficheiro de credenciais do cofre para um computador local.

1. Abra o [Portal do Azure](https://ms.azure.portal.com/)
2. No menu da esquerda, selecione **todos os serviços** e na lista de serviços, escreva **dos serviços de recuperação**. Clique em **cofres dos serviços de recuperação**.

   ![Abra o Cofre dos serviços de recuperação](../articles/backup/media/tutorial-backup-windows-server-to-azure/full-browser-open-rs-vault_2.png)
3. Na página de início rápido, clique em **as credenciais do Cofre de transferência**. O portal gera o ficheiro de credenciais do cofre, que é disponibilizado para transferência.
   
   ![Transferência](./media/backup-download-credentials/downloadvc.png)
4. O portal irá gerar uma credencial de cofre utilizando uma combinação de nome do cofre e a data atual. Clique em **guardar** para transferir as credenciais do cofre para a pasta de transferências da conta local, ou selecione guardar como no menu Guardar para especificar uma localização para as credenciais do cofre.

### <a name="note"></a>Nota
* Certifique-se de que as credenciais do Cofre é guardado numa localização que pode ser acedida a partir do seu computador. Se esta está armazenada numa partilha de ficheiros/SMB, verifique as permissões de acesso.
* O ficheiro de credenciais do Cofre é utilizado apenas durante o fluxo de trabalho do registo.
* O ficheiro de credenciais do cofre expira após 48hrs e pode ser transferido a partir do portal.
* Consulte a cópia de segurança do Azure [FAQ](../articles/backup/backup-azure-backup-faq.md) para quaisquer perguntas sobre o fluxo de trabalho.

