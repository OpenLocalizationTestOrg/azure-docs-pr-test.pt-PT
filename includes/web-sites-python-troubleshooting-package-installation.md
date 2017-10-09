Alguns pacotes podem não ser instalados através do pip quando são executados no Azure.  Pode simplesmente ser que esse pacote Olá não está disponível no Olá índice de pacote do Python.  É possível que é necessário um compilador (um compilador não está disponível no Olá máquina Olá aplicação web em execução no App Service do Azure).

Nesta secção, vamos abordar formas toodeal com este problema.

### <a name="request-wheels"></a>Solicitar rodas
Se a instalação do pacote Olá exigir um compilador, deve tentar contactar Olá pacote proprietário toorequest que as rodas sejam disponibilizadas para o pacote de Olá.

Com Olá recente disponibilidade [Microsoft Visual C++ Compiler para o Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], agora é mais fácil pacotes toobuild com código nativo para o Python 2.7.

### <a name="build-wheels-requires-windows"></a>Criar rodas (requer o Windows)
Nota: Ao utilizar esta opção, certifique-se pacote de Olá toocompile através de um ambiente Python que corresponde à Olá plataforma/arquitetura/versão que é utilizada na aplicação de web de Olá no App Service do Azure (Windows/32-bit/2.7 ou 3.4).

Se não instalar o pacote Olá porque requer um compilador, pode instalar o compilador de Olá no seu computador local e criar uma roda para o pacote de Olá, que, em seguida, irá incluir no seu repositório.

Utilizadores Mac/Linux: Se não tiver máquina do acesso tooa Windows, consulte o artigo [criar uma Máquina Virtual com o Windows] [ Create a Virtual Machine Running Windows] como toocreate uma VM no Azure.  Pode utilizá-lo toobuild rodas de Olá, adicioná-los toohello repositório e eliminar Olá VM se assim o desejar. 

Para Python 2.7, pode instalar [Microsoft Visual C++ Compiler para o Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].

Para Python 3.4, pode instalar [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].

toobuild rodas, precisa de pacote de rodas Olá:

    env\scripts\pip install wheel

Irá utilizar `pip wheel` toocompile uma dependência:

    env\scripts\pip wheel azure==0.8.4

Esta ação cria um ficheiro de whl na pasta \wheelhouse de Olá.  Adicione pasta \wheelhouse de Olá e repositório de tooyour de ficheiros de rodas.

Editar o Olá de tooadd requirements.txt `--find-links` opção na parte superior do Olá. Isto indica pip toolook para obter uma correspondência exata na pasta local do Olá antes do índice de pacote toohello python.

    --find-links wheelhouse
    azure==0.8.4

Se quiser tooinclude todas as suas dependências Olá \wheelhouse pasta e não utilize Olá pacote do python do índice de todo, pode forçar o índice de pacote do pip tooignore Olá adicionando `--no-index` toohello superior do requirements.txt.

    --no-index

### <a name="customize-installation"></a>Personalizar a instalação
Pode personalizar tooinstall de script de implementação de Olá um pacote no ambiente virtual Olá a utilizar um instalador alternativo, tal como fácil\_instalar.  Veja o deploy.cmd para obter um exemplo comentado.  Certifique-se de que esses pacotes não estão listados no requirements.txt, tooprevent pip de instalá-los.

Adicione este script de implementação toohello:

    env\scripts\easy_install somepackage

Também pode ser capaz de toouse fácil\_instale tooinstall a partir de um instalador. exe (alguns são zip compatível, por isso, fácil\_instalar suporte).  Adicione Olá instalador tooyour repositório e invoque fácil\_instalar transferindo Olá toohello de caminho executável.

Adicione este script de implementação toohello:

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a>Incluir o ambiente virtual Olá no repositório de Olá (requer o Windows)
Nota: Ao utilizar esta opção, certifique-se de que toouse um ambiente virtual que corresponde à Olá plataforma/arquitetura/versão que é utilizada na aplicação de web de Olá no App Service do Azure (Windows/32-bit/2.7 ou 3.4).

Se incluir o ambiente virtual Olá no repositório de Olá, pode impedir o script de implementação de Olá de fazer a gestão do ambiente virtual no Azure através da criação de um ficheiro vazio:

    .skipPythonDeployment

Recomendamos que elimine o ambiente virtual existente na aplicação Olá, tooprevent representada ficheiros Olá quando o ambiente virtual Olá foi gerida automaticamente.

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
