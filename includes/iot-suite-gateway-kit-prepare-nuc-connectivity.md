## <a name="prepare-your-intel-nuc"></a>Preparar o Intel NUC

configuração de hardware do toocomplete Olá, tem de:

- Ligar o Intel NUC toohello fonte de alimentação incluído no kit de Olá.
- Ligar à rede de tooyour do Intel NUC com um cabo de Ethernet.

Agora concluiu a configuração de hardware de Olá do seu dispositivo de gateway Intel NUC.

### <a name="sign-in-and-access-hello-terminal"></a>A iniciar sessão e aceder ao terminal Olá

Tem duas opções tooaccess num ambiente de terminal no seu NUC Intel:

- Se tiver um teclado e monitorizar tooyour ligado Intel NUC, pode aceder diretamente a shell de Olá. as credenciais predefinidas de Olá são username **raiz** e palavra-passe **raiz**.

- Shell de Olá de acesso na sua NUC Intel utilizando SSH a partir do seu computador de secretária.

#### <a name="sign-in-with-ssh"></a>Inicie sessão com SSH

toosign com SSH, terá de endereço IP de Olá do seu NUC Intel. Se tiver um teclado e monitorizar tooyour ligado Intel NUC, utilize Olá `ifconfig` endereço IP de Olá toofind de comandos. Em alternativa, ligar tooyour router toolist Olá endereços dispositivos na sua rede.

Inicie sessão com o nome de utilizador **raiz** e palavra-passe **raiz**.

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a>Opcional: Partilhar uma pasta no seu NUC Intel

Opcionalmente, poderá ser útil tooshare uma pasta no seu NUC Intel com o seu ambiente de trabalho. Uma pasta de partilha permite toouse seu editor de texto preferido de ambiente de trabalho (tais como [Visual Studio Code](https://code.visualstudio.com/) ou [texto Sublime](http://www.sublimetext.com/)) tooedit ficheiros no seu NUC Intel em vez de utilizar `nano` ou `vi`.

tooshare uma pasta com o Windows, configurar um servidor de Samba em Olá Intel NUC. Em alternativa, utilize o servidor SFTP Olá no Olá Intel NUC com um cliente SFTP no seu computador de secretária.
