Devido ao desenvolvimento em curso, versão do Android SDK Olá instalado no Android Studio, não poderá corresponder à versão de Olá no código Olá. Olá SDK Android referenciado neste tutorial está Olá 23, da versão mais recente momento Olá de escrita. Pode aumentar o número de versão Olá como novas versões do Olá SDK são apresentados e, recomendamos que utilize Olá versão mais recente disponível.

Dois sintomas de incompatibilidade de versão são:

- Quando criar ou reconstruir o projeto de Olá, poderá receber mensagens de erro do Gradle como "**falha toofind destino Google Inc.:Google APIs:n**".
- Objetos Android padrão no código que deve resolver com base no `import` instruções poderão estar a gerar mensagens de erro.

Se qualquer um destes for apresentada, versão de Olá do Olá SDK Android instalado no Android Studio, poderá não corresponder Olá SDK de destino do projeto de Olá transferido. versão de Olá tooverify, tornar Olá seguintes alterações:

1. No Android Studio, clique em **ferramentas** > **Android** > **SDK Manager**. Se não tiver instalado a versão mais recente do Olá do Olá plataforma do SDK, em seguida, clique em tooinstall-lo. Anote o número de versão Olá.
2. No Olá **Explorador de projeto** separador em **Gradle Scripts**, abra o ficheiro de Olá **gradle (modeule: aplicação)**. Certifique-se de que Olá **compileSdkVersion** e **buildToolsVersion** estão definidas toohello versão do SDK mais recente instalada. etiquetas de Olá poderão ter o seguinte aspeto:

             compileSdkVersion 'Google Inc.:Google APIs:23'
            buildToolsVersion "23.0.2"
3. Olá Explorador de projeto Android Studio, nó do projeto de contexto Olá, escolha **propriedades**e na coluna esquerda Olá escolha **Android**. Certifique-se de que Olá **compilação do projeto de destino** está definido toohello mesma versão do SDK como Olá **targetSdkVersion**.

No Android Studio, o ficheiro de manifesto Olá deixou de destino de Olá toospecify utilizados SDK e versão mínima do SDK, ao contrário das maiúsculas e minúsculas de Olá com o Eclipse.
