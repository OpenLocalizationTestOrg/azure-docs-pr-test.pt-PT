<span data-ttu-id="aaf3c-101">Todos os Blobs no armazenamento do Azure têm de residir num contentor.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-101">Every blob in Azure storage must reside in a container.</span></span> <span data-ttu-id="aaf3c-102">parte de formulários do contentor Olá do nome do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-102">hello container forms part of hello blob name.</span></span> <span data-ttu-id="aaf3c-103">Por exemplo, `mycontainer` é Olá nome do contentor de Olá nestes URIs de blob de exemplo:</span><span class="sxs-lookup"><span data-stu-id="aaf3c-103">For example, `mycontainer` is hello name of hello container in these sample blob URIs:</span></span>

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

<span data-ttu-id="aaf3c-104">Um nome de contentor tem de ser um nome DNS válido, cumprindo toohello seguintes regras de nomenclatura:</span><span class="sxs-lookup"><span data-stu-id="aaf3c-104">A container name must be a valid DNS name, conforming toohello following naming rules:</span></span>

1. <span data-ttu-id="aaf3c-105">Os nomes de contentor tem de começar com uma letra ou número e só podem conter letras, números e caráter de travessão (-) Olá.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-105">Container names must start with a letter or number, and can contain only letters, numbers, and hello dash (-) character.</span></span>
2. <span data-ttu-id="aaf3c-106">Cada caráter de travessão (-) tem de ser imediatamente precedido e seguido por uma letra ou um número; os traços consecutivos não são permitidos em nomes de contentor.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-106">Every dash (-) character must be immediately preceded and followed by a letter or number; consecutive dashes are not permitted in container names.</span></span>
3. <span data-ttu-id="aaf3c-107">Tenha em atenção que o nome do contentor tem de estar em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-107">All letters in a container name must be lowercase.</span></span>
4. <span data-ttu-id="aaf3c-108">Os nomes de contentor devem ter entre 3 e 63 carateres.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-108">Container names must be from 3 through 63 characters long.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aaf3c-109">Tenha em atenção que Olá nome de um contentor deve estar sempre em minúscula.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-109">Note that hello name of a container must always be lowercase.</span></span> <span data-ttu-id="aaf3c-110">Se incluir uma letra em maiúsculas num nome de contentor ou violar regras de nomenclatura de contentor de Olá, poderá receber um erro 400 (pedido incorreto).</span><span class="sxs-lookup"><span data-stu-id="aaf3c-110">If you include an upper-case letter in a container name, or otherwise violate hello container naming rules, you may receive a 400 error (Bad Request).</span></span> 
> 
> 

