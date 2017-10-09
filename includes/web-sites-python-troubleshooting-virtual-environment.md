script de implementação de Olá ignorará a criação do ambiente virtual Olá no Azure se detetar que já existe um ambiente virtual compatível.  o que pode acelerar a implementação significativamente.  Os pacotes já instalados serão ignorados pelo pip.

Em determinadas situações, poderá ser útil tooforce eliminação desse ambiente virtual.  Poderá ser útil toodo isto se decidir tooinclude um ambiente virtual como parte do seu repositório.  Também poderá toodo isto se precisar de tooget eliminar determinados pacotes ou testar alterações toorequirements.txt.

Existem alguns Olá de toomanage opções existente ambiente virtual no Azure:

### <a name="option-1-use-ftp"></a>Opção 1: utilizar o FTP
Com um cliente de FTP, ligue toohello servidor e irá ser pasta do toodelete capaz de Olá env.  Tenha em atenção que alguns clientes FTP (por exemplo, browsers da web) poderão ser só de leitura e não lhe permitem toodelete pastas, pelo que deverá toomake se toouse um cliente de FTP com essa capacidade.  nome de anfitrião de Olá FTP e o utilizador são apresentados no painel da sua aplicação web no Olá [Portal do Azure](https://portal.azure.com).

### <a name="option-2-toggle-runtime"></a>Opção 2: ativar/desativar o runtime
Esta é uma alternativa que tira partido do facto de Olá que o script de implementação de Olá irá eliminar a pasta env de Olá quando não corresponder à versão pretendida do Olá do Python.  Efetivamente esta ação eliminará o ambiente existente Olá e criar um novo.

1. Versão diferente do tooa de comutador do Python (através do runtime.txt ou Olá **definições da aplicação** painel no Portal do Azure de Olá)
2. Emita consolidações de git de algumas alterações (ignore os erros de instalação do pip, se aplicável)
3. Versão back-tooinitial de comutador do Python
4. Emita consolidações de git de algumas alterações novamente

### <a name="option-3-customize-deployment-script"></a>Opção 3: personalizar o script de implementação
Se tiver personalizado o script de implementação de Olá, pode alterar Olá código no deploy.cmd tooforce-pasta do toodelete Olá env.

