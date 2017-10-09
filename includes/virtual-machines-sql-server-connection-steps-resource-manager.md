### <a name="configure-a-dns-label-for-hello-public-ip-address"></a>Configurar uma etiqueta de DNS para endereço IP público Olá

tooconnect toohello motor de base de dados do SQL Server de Olá Internet, considere criar uma etiqueta de DNS para o seu endereço IP público. Pode ligar ao endereço IP, mas Olá etiqueta de DNS cria um registo que seja mais fácil tooidentify e abstracts Olá subjacente endereço IP público.

> [!NOTE]
> As etiquetas de DNS não são necessárias se a instância de plano tooonly ligar toohello do SQL Server dentro Olá mesma rede Virtual ou apenas localmente.

toocreate uma etiqueta de DNS, comece por selecionar **máquinas virtuais** no portal de Olá. Selecione o seu toobring VM do SQL Server, as respetivas propriedades.

1. Na descrição geral de máquina virtual de Olá, selecione o **endereço IP público**.

    ![endereço IP público.](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. Nas propriedades de Olá do endereço IP público, expanda **configuração**.

1. Introduza um nome para a Etiqueta de DNS. Este nome é um registo que podem ser utilizados tooconnect tooyour VM do SQL Server por nome em vez de por endereço IP diretamente.

1. Clique em Olá **guardar** botão.

    ![etiqueta de DNS](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Ligar toohello motor de base de dados a partir de outro computador

1. Num computador ligado toohello internet, abra SQL Server Management Studio (SSMS). Se não tiver o SQL Server Management Studio, poderá transferi-lo [aqui](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

1. No Olá **ligar tooServer** ou **ligar tooDatabase motor** caixa de diálogo, editar Olá **nome do servidor** valor. Introduza o endereço IP Olá ou nome DNS completo da máquina virtual de Olá (determinado na tarefa anterior Olá). Também pode adicionar uma vírgula e fornecer a porta TCP do SQL Server. Por exemplo, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.

1. No Olá **autenticação** caixa, selecione **autenticação do SQL Server**.

1. No Olá **início de sessão** caixa, nome do tipo Olá de um início de sessão SQL válido.

1. No Olá **palavra-passe** caixa, a palavra-passe Olá de tipo de início de sessão Olá.

1. Clique em **Ligar**.

    ![ligação SSMS](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)