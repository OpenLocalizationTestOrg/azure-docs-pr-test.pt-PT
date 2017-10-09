## <a name="next-steps"></a>Passos seguintes

Depois de ativar a integração do Cofre de chaves do Azure, pode ativar a encriptação do SQL Server na sua VM do SQL Server. Em primeiro lugar, precisa de toocreate uma chave assimétrica no interior do seu Cofre de chaves e uma chave simétrica dentro do SQL Server na VM. Em seguida, será capaz de tooexecute T-SQL instruções tooenable a encriptação para as bases de dados e as cópias de segurança.

Existem várias formas de encriptação, pode tirar partido de:

* [Encriptação de dados transparente (TDE)](https://msdn.microsoft.com/library/bb934049.aspx)
* [Cópias de segurança encriptadas](https://msdn.microsoft.com/library/dn449489.aspx)
* [Encriptação de nível de coluna (CLE)](https://msdn.microsoft.com/library/ms173744.aspx)

Olá scripts de Transact-SQL seguintes fornecem exemplos para cada uma destas áreas.

### <a name="prerequisites-for-examples"></a>Pré-requisitos de exemplos

Cada exemplo baseia-se na pré-requisitos de Olá dois: chamada de uma chave assimétrica do seu Cofre de chaves **CONTOSO_KEY** e uma credencial criado através da funcionalidade de integração AKV Olá denominada **Azure_EKM_TDE_cred**. Olá seguintes comandos de Transact-SQL a configuração destes pré-requisitos para a execução de exemplos de Olá.

``` sql
USE master;
GO

sp_configure [show advanced options], 1;
GO
RECONFIGURE;
GO

-- Enable EKM provider
sp_configure [EKM provider enabled], 1;
GO
RECONFIGURE;

--create provider
CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov
FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';
GO

--create credential
CREATE CREDENTIAL sysadmin_ekm_cred
    WITH IDENTITY = 'keytestvault', --keyvault
    SECRET = '<<SECRET>>'
FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;


--must have sysadmin
ALTER LOGIN [TDE_Login]
ADD CREDENTIAL sysadmin_ekm_cred;


CREATE ASYMMETRIC KEY CONTOSO_KEY
FROM PROVIDER [AzureKeyVault_EKM_Prov]
WITH PROVIDER_KEY_NAME = 'keytestvault',  --key name
CREATION_DISPOSITION = OPEN_EXISTING;
```

### <a name="transparent-data-encryption-tde"></a>Encriptação de dados transparente (TDE)

1. Criar um toobe de início de sessão do SQL Server utilizada pelo motor de base de dados de Olá para TDE, em seguida, adicionar Olá credencial tooit.

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello TDE Login tooadd hello credential for use by the
   -- Database Engine tooaccess hello key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. Crie chave de encriptação de base de dados Olá que será utilizado para TDE.

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello database tooenable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a>Cópias de segurança encriptadas

1. Crie um toobe de início de sessão do SQL Server utilizada pelo motor de base de dados de encriptação de cópias de segurança de Olá e adicionar Olá credencial tooit.

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it is encrypting hello backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello Encrypted Backup Login tooadd hello credential for use by
   -- hello Database Engine tooaccess hello key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. Base de dados de cópia de segurança Olá especificação de encriptação com chave assimétrica Olá armazenado no Cofre de chaves Olá.

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a>Encriptação de nível de coluna (CLE)

Este script cria uma chave simétrica protegida por chave assimétrica do Olá no Cofre de chaves Olá e, em seguida, utiliza dados de tooencrypt chave simétrica Olá na base de dados de Olá.

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open hello symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data tooencrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close hello symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a>Recursos adicionais

Para mais informações sobre como toouse estas funcionalidades de encriptação, consulte o artigo [utilizando EKM com funcionalidades de encriptação do SQL Server](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).

Tenha em atenção que Olá passos deste artigo partem do princípio de que já tenha SQL Server em execução numa máquina virtual do Azure. Caso contrário, veja [aprovisionar uma máquina virtual do SQL Server no Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md). Para obter outras orientações sobre a executar o SQL Server em VMs do Azure, consulte [SQL Server em Virtual Machines do Azure descrição-geral](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).
