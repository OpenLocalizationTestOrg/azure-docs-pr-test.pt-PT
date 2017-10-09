## <a name="next-steps"></a><span data-ttu-id="3def6-101">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3def6-101">Next steps</span></span>

<span data-ttu-id="3def6-102">Depois de ativar a integração do Cofre de chaves do Azure, pode ativar a encriptação do SQL Server na sua VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3def6-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="3def6-103">Em primeiro lugar, precisa de toocreate uma chave assimétrica no interior do seu Cofre de chaves e uma chave simétrica dentro do SQL Server na VM.</span><span class="sxs-lookup"><span data-stu-id="3def6-103">First, you will need toocreate an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="3def6-104">Em seguida, será capaz de tooexecute T-SQL instruções tooenable a encriptação para as bases de dados e as cópias de segurança.</span><span class="sxs-lookup"><span data-stu-id="3def6-104">Then, you will be able tooexecute T-SQL statements tooenable encryption for your databases and backups.</span></span>

<span data-ttu-id="3def6-105">Existem várias formas de encriptação, pode tirar partido de:</span><span class="sxs-lookup"><span data-stu-id="3def6-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="3def6-106">Encriptação de dados transparente (TDE)</span><span class="sxs-lookup"><span data-stu-id="3def6-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="3def6-107">Cópias de segurança encriptadas</span><span class="sxs-lookup"><span data-stu-id="3def6-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="3def6-108">Encriptação de nível de coluna (CLE)</span><span class="sxs-lookup"><span data-stu-id="3def6-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="3def6-109">Olá scripts de Transact-SQL seguintes fornecem exemplos para cada uma destas áreas.</span><span class="sxs-lookup"><span data-stu-id="3def6-109">hello following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="3def6-110">Pré-requisitos de exemplos</span><span class="sxs-lookup"><span data-stu-id="3def6-110">Prerequisites for examples</span></span>

<span data-ttu-id="3def6-111">Cada exemplo baseia-se na pré-requisitos de Olá dois: chamada de uma chave assimétrica do seu Cofre de chaves **CONTOSO_KEY** e uma credencial criado através da funcionalidade de integração AKV Olá denominada **Azure_EKM_TDE_cred**.</span><span class="sxs-lookup"><span data-stu-id="3def6-111">Each example is based on hello two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by hello AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="3def6-112">Olá seguintes comandos de Transact-SQL a configuração destes pré-requisitos para a execução de exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="3def6-112">hello following Transact-SQL commands setup these prerequisites for running hello examples.</span></span>

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

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="3def6-113">Encriptação de dados transparente (TDE)</span><span class="sxs-lookup"><span data-stu-id="3def6-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="3def6-114">Criar um toobe de início de sessão do SQL Server utilizada pelo motor de base de dados de Olá para TDE, em seguida, adicionar Olá credencial tooit.</span><span class="sxs-lookup"><span data-stu-id="3def6-114">Create a SQL Server login toobe used by hello Database Engine for TDE, then add hello credential tooit.</span></span>

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

1. <span data-ttu-id="3def6-115">Crie chave de encriptação de base de dados Olá que será utilizado para TDE.</span><span class="sxs-lookup"><span data-stu-id="3def6-115">Create hello database encryption key that will be used for TDE.</span></span>

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

### <a name="encrypted-backups"></a><span data-ttu-id="3def6-116">Cópias de segurança encriptadas</span><span class="sxs-lookup"><span data-stu-id="3def6-116">Encrypted backups</span></span>

1. <span data-ttu-id="3def6-117">Crie um toobe de início de sessão do SQL Server utilizada pelo motor de base de dados de encriptação de cópias de segurança de Olá e adicionar Olá credencial tooit.</span><span class="sxs-lookup"><span data-stu-id="3def6-117">Create a SQL Server login toobe used by hello Database Engine for encrypting backups, and add hello credential tooit.</span></span>

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

1. <span data-ttu-id="3def6-118">Base de dados de cópia de segurança Olá especificação de encriptação com chave assimétrica Olá armazenado no Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="3def6-118">Backup hello database specifying encryption with hello asymmetric key stored in hello key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="3def6-119">Encriptação de nível de coluna (CLE)</span><span class="sxs-lookup"><span data-stu-id="3def6-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="3def6-120">Este script cria uma chave simétrica protegida por chave assimétrica do Olá no Cofre de chaves Olá e, em seguida, utiliza dados de tooencrypt chave simétrica Olá na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="3def6-120">This script creates a symmetric key protected by hello asymmetric key in hello key vault, and then uses hello symmetric key tooencrypt data in hello database.</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="3def6-121">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3def6-121">Additional resources</span></span>

<span data-ttu-id="3def6-122">Para mais informações sobre como toouse estas funcionalidades de encriptação, consulte o artigo [utilizando EKM com funcionalidades de encriptação do SQL Server](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span><span class="sxs-lookup"><span data-stu-id="3def6-122">For more information on how toouse these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="3def6-123">Tenha em atenção que Olá passos deste artigo partem do princípio de que já tenha SQL Server em execução numa máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="3def6-123">Note that hello steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="3def6-124">Caso contrário, veja [aprovisionar uma máquina virtual do SQL Server no Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="3def6-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="3def6-125">Para obter outras orientações sobre a executar o SQL Server em VMs do Azure, consulte [SQL Server em Virtual Machines do Azure descrição-geral](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3def6-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
