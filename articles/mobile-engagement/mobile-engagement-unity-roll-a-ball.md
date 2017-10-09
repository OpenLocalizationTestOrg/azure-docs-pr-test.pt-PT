---
title: "um tutorial Ball de agregação aaaUnity"
description: "Passos toocreate Olá clássico Unity Roll um jogo Ball que é um pré-requisito para todos os tutoriais do Unity do Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0afd0eca-f74a-43aa-bba8-436a0265c312
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 10d923682432961207594886b08e5db60cf60d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="a94a4-103"><a id="unity-roll-a-ball"></a>Criar Unity Roll um jogo Ball</span><span class="sxs-lookup"><span data-stu-id="a94a4-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="a94a4-104">Este tutorial explica passos principais do Olá ligeiramente modificado para [Unity Roll um tutorial Ball](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span><span class="sxs-lookup"><span data-stu-id="a94a4-104">This tutorial walks through hello main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="a94a4-105">Este jogos de exemplo é composta por um objeto de spherical 'player' que é controlado pelo utilizador de aplicação Olá, não sendo objetivo Olá de jogo de Olá too'collect' coleccionáveis objetos por objeto de leitor de Olá colliding com estes objetos coleccionáveis.</span><span class="sxs-lookup"><span data-stu-id="a94a4-105">This sample game consists of a spherical 'player' object which is controlled by hello app user and hello objective of hello game is too'collect' collectible objects by colliding hello player object with these collectible objects.</span></span> <span data-ttu-id="a94a4-106">Isto pressupõe familiaridade básica com o ambiente de editor do Unity.</span><span class="sxs-lookup"><span data-stu-id="a94a4-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="a94a4-107">Caso se depare com problemas devem consultar tutorial completa toohello.</span><span class="sxs-lookup"><span data-stu-id="a94a4-107">If you run into any issues then you should refer toohello full tutorial.</span></span> 

### <a name="setting-up-hello-game"></a><span data-ttu-id="a94a4-108">Configurar jogo Olá</span><span class="sxs-lookup"><span data-stu-id="a94a4-108">Setting up hello game</span></span>
<span data-ttu-id="a94a4-109">passos de Olá abaixo são de Olá [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="a94a4-109">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="a94a4-110">Abra **Unity Editor** e clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="a94a4-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="a94a4-111">Forneça um **nome do projeto** & **localização**, selecione **3D** e clique em **criar projeto**.</span><span class="sxs-lookup"><span data-stu-id="a94a4-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="a94a4-112">Guardar cena de predefinição Olá acabou de criar como parte do projeto novo Olá tal como acontece com o nome de Olá **MiniGame** dentro de um novo  **\_em segundo plano** pasta em **ativos** pasta:</span><span class="sxs-lookup"><span data-stu-id="a94a4-112">Save hello default scene just created as part of hello new project as with hello name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="a94a4-113">Criar um **objeto 3D -> Plane** como Olá reproduzir campo e mudar o nome deste objeto plane como **zero**</span><span class="sxs-lookup"><span data-stu-id="a94a4-113">Create a **3D Object -> Plane** as hello playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="a94a4-114">Componente de transformação de Olá reposição para este **zero** objeto para que o se encontra na Olá origem.</span><span class="sxs-lookup"><span data-stu-id="a94a4-114">Reset hello transform component for this **Ground** object so that it is at hello Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="a94a4-115">Desmarque **grelha mostrar** de **Gizmos menu** para Olá **zero** objeto.</span><span class="sxs-lookup"><span data-stu-id="a94a4-115">Uncheck **Show Grid** from **Gizmos menu** for hello **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="a94a4-116">Olá atualização **escala** componente para Olá **zero** objeto toobe [X = 2, Y = 1, Z = 2].</span><span class="sxs-lookup"><span data-stu-id="a94a4-116">Update hello **Scale** component for hello **Ground** object toobe [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="a94a4-117">Adicione um novo **objeto 3D -> Sphere** toohello projeto e mude o nome do objeto este sphere como **Player**.</span><span class="sxs-lookup"><span data-stu-id="a94a4-117">Add a new **3D Object -> Sphere** toohello project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="a94a4-118">Selecione Olá **Player** de objeto e clique em **repor transformar** objeto de Plane toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="a94a4-118">Select hello **Player** object and click **Reset Transform** similar toohello Plane object.</span></span> 
10. <span data-ttu-id="a94a4-119">Atualização **transformação -> posição -> coordenada Y** componente para Olá Player Y como 0,5.</span><span class="sxs-lookup"><span data-stu-id="a94a4-119">Update **Transform -> Position -> Y Coordinate** component for hello Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="a94a4-120">Criar uma nova pasta designada **materiais** no projeto olá onde iremos criar leitor de Olá Olá toocolor essenciais.</span><span class="sxs-lookup"><span data-stu-id="a94a4-120">Create a new folder called **Materials** in hello project where we will create hello material toocolor hello player.</span></span> 
12. <span data-ttu-id="a94a4-121">Crie um novo **Material** chamado **em segundo plano** nesta pasta.</span><span class="sxs-lookup"><span data-stu-id="a94a4-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="a94a4-122">Atualizar para atualizar cor Olá de material de Olá Olá **Albedo** propriedade do mesmo.</span><span class="sxs-lookup"><span data-stu-id="a94a4-122">Update hello color of hello material by updating hello **Albedo** property of it.</span></span> <span data-ttu-id="a94a4-123">Pode selecionar valores RGB Olá [0,32,64].</span><span class="sxs-lookup"><span data-stu-id="a94a4-123">You can select hello RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="a94a4-124">Arrastar deste material para Olá cena vista tooapply cor toohello **zero** objeto.</span><span class="sxs-lookup"><span data-stu-id="a94a4-124">Drag this material into hello scene view tooapply color toohello **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="a94a4-125">Por fim, atualize Olá **transformação -> rotação -> Y** too60 no objeto de leve Direcional Olá para efeitos de clareza.</span><span class="sxs-lookup"><span data-stu-id="a94a4-125">Finally update hello **Transform -> Rotation -> Y** too60 on hello Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-hello-player"></a><span data-ttu-id="a94a4-126">Leitor de Olá mover</span><span class="sxs-lookup"><span data-stu-id="a94a4-126">Moving hello player</span></span>
<span data-ttu-id="a94a4-127">passos de Olá abaixo são de Olá [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="a94a4-127">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="a94a4-128">Adicionar um **RigidBody** componente toohello **Player** objeto.</span><span class="sxs-lookup"><span data-stu-id="a94a4-128">Add a **RigidBody** component toohello **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="a94a4-129">Criar uma nova pasta designada **Scripts** no Olá projeto.</span><span class="sxs-lookup"><span data-stu-id="a94a4-129">Create a new folder called **Scripts** in hello Project.</span></span> 
3. <span data-ttu-id="a94a4-130">Clique em **adicionar componente -> Script novo -> c# Script**.</span><span class="sxs-lookup"><span data-stu-id="a94a4-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="a94a4-131">Nome **PlayerController**e clique em **criar e adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a94a4-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="a94a4-132">Isto irá criar e anexar um objeto de leitor de toohello de script.</span><span class="sxs-lookup"><span data-stu-id="a94a4-132">This will create and attach a script toohello Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="a94a4-133">Mover este script em Olá **Scripts** pasta do projeto de Olá.</span><span class="sxs-lookup"><span data-stu-id="a94a4-133">Move this script under hello **Scripts** folder in hello project.</span></span> 
5. <span data-ttu-id="a94a4-134">Abrir Olá script para edição no seu editor favorito script, atualize o código de script de Olá com Olá seguinte código e guardá-lo.</span><span class="sxs-lookup"><span data-stu-id="a94a4-134">Open hello script for editing in your favorite script editor, update hello script code with hello following code and save it.</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour 
        {
            public float speed;
            private Rigidbody rb;
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
                rb.AddForce (movement * speed);
            }
        }
6. <span data-ttu-id="a94a4-135">Tenha em atenção que script Olá acima utiliza um **velocidade** propriedade.</span><span class="sxs-lookup"><span data-stu-id="a94a4-135">Note that hello script above uses a **Speed** property.</span></span> <span data-ttu-id="a94a4-136">No editor do Unity Olá, atualize Olá velocidade propriedade too10.</span><span class="sxs-lookup"><span data-stu-id="a94a4-136">In hello Unity editor, update hello speed property too10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="a94a4-137">Atingiu o **reproduzir** no Olá Unity Editor.</span><span class="sxs-lookup"><span data-stu-id="a94a4-137">Hit **Play** in hello Unity Editor.</span></span> <span data-ttu-id="a94a4-138">Agora, deve ser capaz de toocontrol ball de Olá utilizando o teclado Olá e deve rodar e mover-se.</span><span class="sxs-lookup"><span data-stu-id="a94a4-138">Now you should be able toocontrol hello ball using hello keyboard and it should rotate and move around.</span></span> 

### <a name="moving-hello-camera"></a><span data-ttu-id="a94a4-139">Mover câmara de Olá</span><span class="sxs-lookup"><span data-stu-id="a94a4-139">Moving hello camera</span></span>
<span data-ttu-id="a94a4-140">passos de Olá abaixo são de Olá [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) e irá associar Olá **Main câmara** toohello **Player** objeto.</span><span class="sxs-lookup"><span data-stu-id="a94a4-140">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie hello **Main Camera** toohello **Player** object.</span></span> 

1. <span data-ttu-id="a94a4-141">Olá atualização **Transform.Position** toobe X = 0, Y = 10.5, a-Z = 10.</span><span class="sxs-lookup"><span data-stu-id="a94a4-141">Update hello **Transform.Position** toobe X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="a94a4-142">Olá atualização **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="a94a4-142">Update hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="a94a4-143">Adicionar um script novo chamado **CameraController** toohello **MainCamera** e movê-la sob a pasta de Scripts Olá.</span><span class="sxs-lookup"><span data-stu-id="a94a4-143">Add a new script called **CameraController** toohello **MainCamera** and move it under hello Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="a94a4-144">Abra o script de Olá para edição e adicionar Olá seguinte código na mesma:</span><span class="sxs-lookup"><span data-stu-id="a94a4-144">Open up hello script for editing and add hello following code in it:</span></span>
   
        using UnityEngine;
        using System.Collections;
   
        public class CameraController : MonoBehaviour {
   
            public GameObject player;
   
            private Vector3 offset;
   
            void Start ()
            {
                offset = transform.position - player.transform.position;
            }
   
            void LateUpdate ()
            {
                transform.position = player.transform.position + offset;
            }
        }
5. <span data-ttu-id="a94a4-145">No ambiente do Unity - arraste variável de leitor de Olá ranhura de leitor de Olá para o objeto principal câmara de Olá, para que hello dois estão associados a um do outro.</span><span class="sxs-lookup"><span data-stu-id="a94a4-145">In Unity environment - drag hello Player variable into hello Player slot for hello Main Camera object so that hello two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="a94a4-146">Agora se clicar em reproduzir no editor de Unity Olá e objeto de leitor Ball rodar Olá, em seguida, verá Olá câmara a seguir ao mesmo no movimento Olá.</span><span class="sxs-lookup"><span data-stu-id="a94a4-146">Now if you hit Play in hello Unity editor and rotate hello Player Ball object then you will see hello Camera following it in hello movement.</span></span>  

### <a name="setting-up-hello-play-area"></a><span data-ttu-id="a94a4-147">Configurar a área de Play Olá</span><span class="sxs-lookup"><span data-stu-id="a94a4-147">Setting up hello Play area</span></span>
<span data-ttu-id="a94a4-148">passos de Olá abaixo são de Olá [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="a94a4-148">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="a94a4-149">Iremos criar planos laterais Olá envolvente Olá zero para que hello objeto leitor Ball não remover a área de play Olá no respetivo movimento.</span><span class="sxs-lookup"><span data-stu-id="a94a4-149">We will create hello Walls surrounding hello Ground so that hello Player Ball object doesn't drop off hello play area in its movement.</span></span> 

1. <span data-ttu-id="a94a4-150">Clique em **criar -> Criar vazio -> jogo objeto** e dê-lhe nome **paredes**</span><span class="sxs-lookup"><span data-stu-id="a94a4-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="a94a4-151">Sob este objeto de planos laterais - criar um novo **objeto 3D -> cubo** e dê-lhe o nome "Lateral Oeste".</span><span class="sxs-lookup"><span data-stu-id="a94a4-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="a94a4-152">Olá atualização **transformação -> posição** e **transformação -> escala** para este objeto oeste lateral.</span><span class="sxs-lookup"><span data-stu-id="a94a4-152">Update hello **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="a94a4-153">Duplicar Olá oeste lateral toocreate um **lateral Leste** com Olá atualizado transformar posição e o dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="a94a4-153">Duplicate hello West wall toocreate an **East wall** with hello updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="a94a4-154">Duplicar Olá Leste lateral toocreate um **lateral Norte** com Olá atualizado transformar posição & escala.</span><span class="sxs-lookup"><span data-stu-id="a94a4-154">Duplicate hello East wall toocreate a **North wall** with hello updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="a94a4-155">Duplicar o padrão de fundo do Olá norte e criar um **lateral Sul** com Olá atualizado transformar posição & escala.</span><span class="sxs-lookup"><span data-stu-id="a94a4-155">Duplicate hello North wall and create a **South wall** with hello updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="a94a4-156">A criação de objetos coleccionáveis</span><span class="sxs-lookup"><span data-stu-id="a94a4-156">Creating Collectible objects</span></span>
<span data-ttu-id="a94a4-157">passos de Olá abaixo são de Olá [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="a94a4-157">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="a94a4-158">Iremos criar algumas apelativo à procura de objetos que irão formar o conjunto de Olá de objectos coleccionáveis tem do objeto de leitor Ball Olá too'collect' por colliding com os mesmos.</span><span class="sxs-lookup"><span data-stu-id="a94a4-158">We will create some attractive looking objects which will form hello set of collectible objects which hello Player Ball object needs too'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="a94a4-159">Crie um novo **3D objeto do cubo** e dê-lhe o nome recolha.</span><span class="sxs-lookup"><span data-stu-id="a94a4-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="a94a4-160">Ajustar Olá **transformação -> rotação** & **transformação -> escala** do objeto de recolha de Olá.</span><span class="sxs-lookup"><span data-stu-id="a94a4-160">Adjust hello **Transform -> Rotation** & **Transform -> Scale** of hello Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="a94a4-161">Criar e anexar um **novo Script do c#** chamado **Rotator** toohello objeto de recolha.</span><span class="sxs-lookup"><span data-stu-id="a94a4-161">Create and attach a **new C# Script** called **Rotator** toohello Pickup object.</span></span> <span data-ttu-id="a94a4-162">Certifique-se de script de Olá tooput na pasta de Scripts Olá.</span><span class="sxs-lookup"><span data-stu-id="a94a4-162">Make sure tooput hello script under hello Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="a94a4-163">Abra este script para edição e atualizá-lo Olá toobe seguintes:</span><span class="sxs-lookup"><span data-stu-id="a94a4-163">Open this script for editing and update it toobe hello following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="a94a4-164">Agora ser rodar Olá acessos Play modo Olá Unity Editor e mostrar a recolha do objeto no respetivo eixo.</span><span class="sxs-lookup"><span data-stu-id="a94a4-164">Now hit hello Play mode in hello Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="a94a4-165">Criar uma nova pasta designada **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="a94a4-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="a94a4-166">Olá arrastar **recolha** objeto e colocá-la na pasta de Prefabs Olá.</span><span class="sxs-lookup"><span data-stu-id="a94a4-166">Drag hello **Pickup** object and put it in hello Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="a94a4-167">Crie um novo **objeto jogo vazio** chamado **Pickups**.</span><span class="sxs-lookup"><span data-stu-id="a94a4-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="a94a4-168">Repor o respetivo tooorigin posição e, em seguida, arraste objetos de recolha de Olá sob este objecto de jogo.</span><span class="sxs-lookup"><span data-stu-id="a94a4-168">Reset its position tooorigin and then drag hello Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="a94a4-169">Olá duplicado **recolha** de objeto e distribuídos-lo no Olá **zero** objeto em torno Olá **Player** objeto atualizando Olá **X & Z do Transform.Position**  valores adequadamente.</span><span class="sxs-lookup"><span data-stu-id="a94a4-169">Duplicate hello **Pickup** object and spread it on hello **Ground** object around hello **Player** object by updating hello **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="a94a4-170">Criar um **material novo** chamado **recolha** e atualizá-lo toobe vermelho no cor atualizando Olá **propriedade Albedo** toowhat semelhante que para atualizar Olá zero de objeto.</span><span class="sxs-lookup"><span data-stu-id="a94a4-170">Create a **new material** called **Pickup** and update it toobe Red in color by updating hello **Albedo property** similar toowhat we did for updating hello Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="a94a4-171">Aplicam-se a objetos de recolha Olá tooall materiais Olá 4.</span><span class="sxs-lookup"><span data-stu-id="a94a4-171">Apply hello material tooall hello 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a><span data-ttu-id="a94a4-172">Recolher objetos de recolha de Olá</span><span class="sxs-lookup"><span data-stu-id="a94a4-172">Collecting hello Pickup objects</span></span>
<span data-ttu-id="a94a4-173">passos de Olá abaixo são de Olá [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="a94a4-173">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="a94a4-174">Iremos atualizar Olá leitor para que seja capaz de too'collect' Olá objetos recolha por colliding com os mesmos.</span><span class="sxs-lookup"><span data-stu-id="a94a4-174">We will update hello Player so that it is able too'collect' hello pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="a94a4-175">Abra Olá **PlayerController** script toohello ligado ao objeto de leitor para edição e atualizá-lo toohello seguintes:</span><span class="sxs-lookup"><span data-stu-id="a94a4-175">Open up hello **PlayerController** script attached toohello Player object for editing and update it toohello following:</span></span>  
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour {
   
            public float speed;
   
            private Rigidbody rb;
   
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
   
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
   
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
   
                rb.AddForce (movement * speed);
            }
   
            void OnTriggerEnter(Collider other) 
            {
                if (other.gameObject.CompareTag ("Pick Up"))
                {
                    other.gameObject.SetActive (false);
                }
            }
        }
2. <span data-ttu-id="a94a4-176">Crie um novo **Tag** chamado **escolha segurança** (tem de corresponder Novidades no script de Olá)</span><span class="sxs-lookup"><span data-stu-id="a94a4-176">Create a new **Tag** called **Pick Up** (it must match what is in hello script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="a94a4-177">Aplicar isto **Tag** objeto de recolha Prefab toohello.</span><span class="sxs-lookup"><span data-stu-id="a94a4-177">Apply this **Tag** toohello Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="a94a4-178">Ativar **IsTrigger** caixa de verificação para o objeto de Prefab Olá.</span><span class="sxs-lookup"><span data-stu-id="a94a4-178">Enable **IsTrigger** checkbox for hello Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="a94a4-179">Adicione um objeto do corpo Rigid tooPickup Prefab.</span><span class="sxs-lookup"><span data-stu-id="a94a4-179">Add a Rigid body tooPickup Prefab object.</span></span> <span data-ttu-id="a94a4-180">Para a otimização de desempenho, atualizaremos collider estático Olá que utilizámos collider dinâmica tooa.</span><span class="sxs-lookup"><span data-stu-id="a94a4-180">For performance optimization we will update hello static collider that we used tooa Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="a94a4-181">Por fim, verifique Olá **IsKinematic** propriedade do objeto prefab Olá.</span><span class="sxs-lookup"><span data-stu-id="a94a4-181">Finally check hello **IsKinematic** property for hello prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="a94a4-182">Atingiu o **reproduzir** no editor de Unity Olá e será capaz de tooplay isto **implementar um Ball** jogo movendo Olá objeto leitor com as chaves de teclado para a entrada de direção.</span><span class="sxs-lookup"><span data-stu-id="a94a4-182">Hit **Play** in hello Unity editor and you will be able tooplay this **Roll a Ball** game by moving hello Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-hello-game-for-mobile-play"></a><span data-ttu-id="a94a4-183">Atualizar Olá jogo para play móvel</span><span class="sxs-lookup"><span data-stu-id="a94a4-183">Updating hello game for mobile play</span></span>
<span data-ttu-id="a94a4-184">secções Olá acima tutorial de básico Olá concluído do Unity.</span><span class="sxs-lookup"><span data-stu-id="a94a4-184">hello sections above concluded hello basic tutorial from Unity.</span></span> <span data-ttu-id="a94a4-185">Agora vamos modificará Olá toomake jogo-amigável de dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="a94a4-185">Now we will modify hello game toomake it mobile device friendly.</span></span> <span data-ttu-id="a94a4-186">Tenha em atenção que utilizámos introdução por teclado para Olá jogo até ao momento para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="a94a4-186">Note that we used keyboard input for hello game so far for testing.</span></span> <span data-ttu-id="a94a4-187">Agora, irá modificá-lo para que iremos pode controlar o leitor Olá utilizando o movimento de Olá de Olá phone ou seja, utilizando Accelerometer como entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="a94a4-187">Now we will modify it so that we can control hello player by using hello motion of hello phone i.e. using Accelerometer as hello input.</span></span> 

<span data-ttu-id="a94a4-188">Abra Olá **PlayerController** script para edição e atualização Olá **FixedUpdate** movimento de Olá toouse método do objeto de leitor Olá accelerometer toomove Olá.</span><span class="sxs-lookup"><span data-stu-id="a94a4-188">Open up hello **PlayerController** script for editing and update hello **FixedUpdate** method toouse hello motion from hello accelerometer toomove hello Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="a94a4-189">Este tutorial conclui a criação de jogo básica com Unity e pode implementá-la num dispositivo de jogo de Olá de tooplay sua escolha.</span><span class="sxs-lookup"><span data-stu-id="a94a4-189">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice tooplay hello game.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-unity-roll-a-ball/1.png    
[2]: ./media/mobile-engagement-unity-roll-a-ball/2.png
[3]: ./media/mobile-engagement-unity-roll-a-ball/3.png
[4]: ./media/mobile-engagement-unity-roll-a-ball/4.png
[5]: ./media/mobile-engagement-unity-roll-a-ball/5.png
[6]: ./media/mobile-engagement-unity-roll-a-ball/6.png
[7]: ./media/mobile-engagement-unity-roll-a-ball/7.png
[8]: ./media/mobile-engagement-unity-roll-a-ball/8.png
[9]: ./media/mobile-engagement-unity-roll-a-ball/9.png    
[10]: ./media/mobile-engagement-unity-roll-a-ball/10.png    
[11]: ./media/mobile-engagement-unity-roll-a-ball/11.png    
[12]: ./media/mobile-engagement-unity-roll-a-ball/12.png
[13]: ./media/mobile-engagement-unity-roll-a-ball/13.png
[14]: ./media/mobile-engagement-unity-roll-a-ball/14.png
[15]: ./media/mobile-engagement-unity-roll-a-ball/15.png
[16]: ./media/mobile-engagement-unity-roll-a-ball/16.png
[17]: ./media/mobile-engagement-unity-roll-a-ball/17.png
[18]: ./media/mobile-engagement-unity-roll-a-ball/18.png
[19]: ./media/mobile-engagement-unity-roll-a-ball/19.png    
[20]: ./media/mobile-engagement-unity-roll-a-ball/20.png    
[21]: ./media/mobile-engagement-unity-roll-a-ball/21.png    
[22]: ./media/mobile-engagement-unity-roll-a-ball/22.png    
[23]: ./media/mobile-engagement-unity-roll-a-ball/23.png    
[24]: ./media/mobile-engagement-unity-roll-a-ball/24.png    
[25]: ./media/mobile-engagement-unity-roll-a-ball/25.png    
[26]: ./media/mobile-engagement-unity-roll-a-ball/26.png    
[27]: ./media/mobile-engagement-unity-roll-a-ball/27.png    
[28]: ./media/mobile-engagement-unity-roll-a-ball/28.png    
[29]: ./media/mobile-engagement-unity-roll-a-ball/29.png    
[30]: ./media/mobile-engagement-unity-roll-a-ball/30.png    
[31]: ./media/mobile-engagement-unity-roll-a-ball/31.png    
[32]: ./media/mobile-engagement-unity-roll-a-ball/32.png    
[33]: ./media/mobile-engagement-unity-roll-a-ball/33.png    
[34]: ./media/mobile-engagement-unity-roll-a-ball/34.png    
[35]: ./media/mobile-engagement-unity-roll-a-ball/35.png    
[36]: ./media/mobile-engagement-unity-roll-a-ball/36.png    
[37]: ./media/mobile-engagement-unity-roll-a-ball/37.png    
[38]: ./media/mobile-engagement-unity-roll-a-ball/38.png    
[51]: ./media/mobile-engagement-unity-roll-a-ball/new-project.png
[52]: ./media/mobile-engagement-unity-roll-a-ball/new-project-properties.png
[53]: ./media/mobile-engagement-unity-roll-a-ball/save-scene.png













