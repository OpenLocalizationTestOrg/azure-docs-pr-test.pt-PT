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
# <a id="unity-roll-a-ball"></a>Criar Unity Roll um jogo Ball
Este tutorial explica passos principais do Olá ligeiramente modificado para [Unity Roll um tutorial Ball](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial). Este jogos de exemplo é composta por um objeto de spherical 'player' que é controlado pelo utilizador de aplicação Olá, não sendo objetivo Olá de jogo de Olá too'collect' coleccionáveis objetos por objeto de leitor de Olá colliding com estes objetos coleccionáveis. Isto pressupõe familiaridade básica com o ambiente de editor do Unity. Caso se depare com problemas devem consultar tutorial completa toohello. 

### <a name="setting-up-hello-game"></a>Configurar jogo Olá
passos de Olá abaixo são de Olá [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)

1. Abra **Unity Editor** e clique em **novo**. 
   
    ![][51] 
2. Forneça um **nome do projeto** & **localização**, selecione **3D** e clique em **criar projeto**.
   
    ![][52]
3. Guardar cena de predefinição Olá acabou de criar como parte do projeto novo Olá tal como acontece com o nome de Olá **MiniGame** dentro de um novo  **\_em segundo plano** pasta em **ativos** pasta:
   
    ![][53]
4. Criar um **objeto 3D -> Plane** como Olá reproduzir campo e mudar o nome deste objeto plane como **zero**
   
    ![][1]
5. Componente de transformação de Olá reposição para este **zero** objeto para que o se encontra na Olá origem. 
   
    ![][3]
6. Desmarque **grelha mostrar** de **Gizmos menu** para Olá **zero** objeto.
   
    ![][4]
7. Olá atualização **escala** componente para Olá **zero** objeto toobe [X = 2, Y = 1, Z = 2]. 
   
    ![][5]
8. Adicione um novo **objeto 3D -> Sphere** toohello projeto e mude o nome do objeto este sphere como **Player**. 
   
    ![][6]
9. Selecione Olá **Player** de objeto e clique em **repor transformar** objeto de Plane toohello semelhante. 
10. Atualização **transformação -> posição -> coordenada Y** componente para Olá Player Y como 0,5.  
    
    ![][7]
11. Criar uma nova pasta designada **materiais** no projeto olá onde iremos criar leitor de Olá Olá toocolor essenciais. 
12. Crie um novo **Material** chamado **em segundo plano** nesta pasta. 
    
    ![][8]
13. Atualizar para atualizar cor Olá de material de Olá Olá **Albedo** propriedade do mesmo. Pode selecionar valores RGB Olá [0,32,64]. 
    
    ![][9]
14. Arrastar deste material para Olá cena vista tooapply cor toohello **zero** objeto. 
    
    ![][10]
15. Por fim, atualize Olá **transformação -> rotação -> Y** too60 no objeto de leve Direcional Olá para efeitos de clareza. 
    
    ![][12]

### <a name="moving-hello-player"></a>Leitor de Olá mover
passos de Olá abaixo são de Olá [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)

1. Adicionar um **RigidBody** componente toohello **Player** objeto. 
   
    ![][13]
2. Criar uma nova pasta designada **Scripts** no Olá projeto. 
3. Clique em **adicionar componente -> Script novo -> c# Script**. Nome **PlayerController**e clique em **criar e adicionar**. Isto irá criar e anexar um objeto de leitor de toohello de script.  
   
    ![][14]
4. Mover este script em Olá **Scripts** pasta do projeto de Olá. 
5. Abrir Olá script para edição no seu editor favorito script, atualize o código de script de Olá com Olá seguinte código e guardá-lo. 
   
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
6. Tenha em atenção que script Olá acima utiliza um **velocidade** propriedade. No editor do Unity Olá, atualize Olá velocidade propriedade too10.  
   
    ![][15]
7. Atingiu o **reproduzir** no Olá Unity Editor. Agora, deve ser capaz de toocontrol ball de Olá utilizando o teclado Olá e deve rodar e mover-se. 

### <a name="moving-hello-camera"></a>Mover câmara de Olá
passos de Olá abaixo são de Olá [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) e irá associar Olá **Main câmara** toohello **Player** objeto. 

1. Olá atualização **Transform.Position** toobe X = 0, Y = 10.5, a-Z = 10.  
2. Olá atualização **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.  
   
    ![][16]
3. Adicionar um script novo chamado **CameraController** toohello **MainCamera** e movê-la sob a pasta de Scripts Olá. 
   
    ![][17]
4. Abra o script de Olá para edição e adicionar Olá seguinte código na mesma:
   
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
5. No ambiente do Unity - arraste variável de leitor de Olá ranhura de leitor de Olá para o objeto principal câmara de Olá, para que hello dois estão associados a um do outro. 
   
    ![][18]
6. Agora se clicar em reproduzir no editor de Unity Olá e objeto de leitor Ball rodar Olá, em seguida, verá Olá câmara a seguir ao mesmo no movimento Olá.  

### <a name="setting-up-hello-play-area"></a>Configurar a área de Play Olá
passos de Olá abaixo são de Olá [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141). Iremos criar planos laterais Olá envolvente Olá zero para que hello objeto leitor Ball não remover a área de play Olá no respetivo movimento. 

1. Clique em **criar -> Criar vazio -> jogo objeto** e dê-lhe nome **paredes**
   
    ![][19]
2. Sob este objeto de planos laterais - criar um novo **objeto 3D -> cubo** e dê-lhe o nome "Lateral Oeste". 
   
    ![][20]
3. Olá atualização **transformação -> posição** e **transformação -> escala** para este objeto oeste lateral. 
   
    ![][21]
4. Duplicar Olá oeste lateral toocreate um **lateral Leste** com Olá atualizado transformar posição e o dimensionamento. 
   
    ![][22]
5. Duplicar Olá Leste lateral toocreate um **lateral Norte** com Olá atualizado transformar posição & escala. 
   
    ![][23]
6. Duplicar o padrão de fundo do Olá norte e criar um **lateral Sul** com Olá atualizado transformar posição & escala. 
   
    ![][24]

### <a name="creating-collectible-objects"></a>A criação de objetos coleccionáveis
passos de Olá abaixo são de Olá [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141). Iremos criar algumas apelativo à procura de objetos que irão formar o conjunto de Olá de objectos coleccionáveis tem do objeto de leitor Ball Olá too'collect' por colliding com os mesmos. 

1. Crie um novo **3D objeto do cubo** e dê-lhe o nome recolha. 
2. Ajustar Olá **transformação -> rotação** & **transformação -> escala** do objeto de recolha de Olá. 
   
    ![][25]
3. Criar e anexar um **novo Script do c#** chamado **Rotator** toohello objeto de recolha. Certifique-se de script de Olá tooput na pasta de Scripts Olá. 
   
    ![][26]
4. Abra este script para edição e atualizá-lo Olá toobe seguintes: 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. Agora ser rodar Olá acessos Play modo Olá Unity Editor e mostrar a recolha do objeto no respetivo eixo.
6. Criar uma nova pasta designada **Prefabs** 
   
    ![][27]
7. Olá arrastar **recolha** objeto e colocá-la na pasta de Prefabs Olá.
   
    ![][28]
8. Crie um novo **objeto jogo vazio** chamado **Pickups**. Repor o respetivo tooorigin posição e, em seguida, arraste objetos de recolha de Olá sob este objecto de jogo.  
   
    ![][29]
9. Olá duplicado **recolha** de objeto e distribuídos-lo no Olá **zero** objeto em torno Olá **Player** objeto atualizando Olá **X & Z do Transform.Position**  valores adequadamente. 
   
    ![][30]
10. Criar um **material novo** chamado **recolha** e atualizá-lo toobe vermelho no cor atualizando Olá **propriedade Albedo** toowhat semelhante que para atualizar Olá zero de objeto. 
    
    ![][31]
11. Aplicam-se a objetos de recolha Olá tooall materiais Olá 4.
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a>Recolher objetos de recolha de Olá
passos de Olá abaixo são de Olá [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141). Iremos atualizar Olá leitor para que seja capaz de too'collect' Olá objetos recolha por colliding com os mesmos. 

1. Abra Olá **PlayerController** script toohello ligado ao objeto de leitor para edição e atualizá-lo toohello seguintes:  
   
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
2. Crie um novo **Tag** chamado **escolha segurança** (tem de corresponder Novidades no script de Olá)  
   
    ![][33]
   
    ![][34]
3. Aplicar isto **Tag** objeto de recolha Prefab toohello. 
   
    ![][35]
4. Ativar **IsTrigger** caixa de verificação para o objeto de Prefab Olá.
   
    ![][36]
5. Adicione um objeto do corpo Rigid tooPickup Prefab. Para a otimização de desempenho, atualizaremos collider estático Olá que utilizámos collider dinâmica tooa. 
   
    ![][37]
6. Por fim, verifique Olá **IsKinematic** propriedade do objeto prefab Olá. 
   
    ![][38]
7. Atingiu o **reproduzir** no editor de Unity Olá e será capaz de tooplay isto **implementar um Ball** jogo movendo Olá objeto leitor com as chaves de teclado para a entrada de direção. 

### <a name="updating-hello-game-for-mobile-play"></a>Atualizar Olá jogo para play móvel
secções Olá acima tutorial de básico Olá concluído do Unity. Agora vamos modificará Olá toomake jogo-amigável de dispositivos móveis. Tenha em atenção que utilizámos introdução por teclado para Olá jogo até ao momento para fins de teste. Agora, irá modificá-lo para que iremos pode controlar o leitor Olá utilizando o movimento de Olá de Olá phone ou seja, utilizando Accelerometer como entrada Olá. 

Abra Olá **PlayerController** script para edição e atualização Olá **FixedUpdate** movimento de Olá toouse método do objeto de leitor Olá accelerometer toomove Olá. 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

Este tutorial conclui a criação de jogo básica com Unity e pode implementá-la num dispositivo de jogo de Olá de tooplay sua escolha. 

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













