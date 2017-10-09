As organizações estão a utilizar mais [Software como serviço (SaaS)](https://azure.microsoft.com/overview/what-is-saas/) aplicações de produtividade porque tecnologia de nuvem e ferramentas são cada vez mais prontamente disponíveis. À medida que cresce o número de Olá de aplicações SaaS, este torna-se um desafio para contas de toomanage Olá administradores e os direitos de acesso e para Olá tooremember utilizadores as respetivas palavras-passe diferentes. Gerir estas aplicações individualmente cria trabalho adicional e é menos seguro.

* Os empregados que têm tookeep controlar de palavras-passe muitos tendem toouse menos seguras tooremember métodos Olá-los, a escrita de palavras-passe ou utilizar as mesmas palavras-passe em muitas contas.
* Quando um empregado novo chega ou um deixa, todas as contas têm de ser individualmente aprovisionadas ou anular aprovisionadas.
* Além disso, o que os funcionários podem começar a utilizar aplicações SaaS para o trabalho sem passar TI, que significa que estão a criar as suas próprias contas em sistemas Olá, os administradores de TI ainda não aprovou e não são de monitorização.  

É uma solução para todos estes desafios-início de sessão único (SSO). Este tem Olá toomanage de forma mais simples várias aplicações e fornecer aos utilizadores uma experiência de início de sessão consistente. Azure Active Directory (Azure AD) fornece uma solução SSO robusta e tem muitas aplicações previamente integradas disponíveis, com tutoriais para administradores tooquickly configurar uma nova aplicação e iniciar o aprovisionamento de utilizadores.

## <a name="how-does-azure-active-directory-integrate-apps"></a>Como é que o Azure Active Directory integrar aplicações?
Azure AD permite-lhe toointegrate as suas aplicações e aprovisionamento de contas. Isto pode ser feito através de qualquer uma das duas abordagens.

* Se a aplicação Olá previamente está integrada na aplicação Olá galeria, pode passar por essa tooset portal cópia de segurança as aplicações e configurar as definições de Olá tooallow SSO. Para qualquer aplicação de galeria, pode começar a utilizar por seguir Olá simples instruções passo a passo apresentadas na Galeria de aplicações de Olá e Olá tooenable portal do Azure-início de sessão único.
* Se não estiver a ser Olá Galeria aplicação Olá, pode ainda configurar a maioria das aplicações no Azure AD como uma aplicação personalizada. Isto requer um pouco mais técnica conhecimentos tooconfigure. Pode adicionar qualquer aplicação que suporta SAML 2.0 como uma aplicação federada ou de qualquer aplicação que tenha uma baseado em HTML-página sessão como uma aplicação SSO de palavra-passe.

No Olá caso em que os utilizadores criou os suas próprias contas para aplicações SaaS que não são geridas pelo departamento de TI Olá [Cloud App Discovery](../articles/active-directory/active-directory-cloudappdiscovery-whatis.md) ferramenta fornece uma solução. Esta ferramenta monitoriza Olá web tráfego tooidentify que aplicações estão a ser utilizadas em toda a organização Olá e número de Olá de pessoas com cada um deles. IT pode utilizar este toolearn de informações que os utilizadores Olá de aplicações preferem e decidir que toointegrate com o Azure AD para SSO.  

Quando integrar uma aplicação do Azure AD, pode mapear as identidades dos utilizadores Olá aplicação estabelecida identidades tootheir respetivo do Azure AD.  

