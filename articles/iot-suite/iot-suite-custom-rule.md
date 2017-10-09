---
title: aaaCreate uma regra personalizada no Azure IoT Suite | Microsoft Docs
description: "Como toocreate uma regra personalizada num IoT Suite solução pré-configurada."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 6c5bb2ca54f3f17b99ad482e727c8e9fa28d7fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="0d3f7-103">Criar uma regra personalizada no Olá solução pré-configurada de monitorização remota</span><span class="sxs-lookup"><span data-stu-id="0d3f7-103">Create a custom rule in hello remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="0d3f7-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="0d3f7-104">Introduction</span></span>

<span data-ttu-id="0d3f7-105">Em soluções de Olá pré-configurada, pode configurar [regras que é acionam quando uma telemetria valor para um dispositivo atinge um limiar específico][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="0d3f7-105">In hello preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="0d3f7-106">[Utilizar telemetria dinâmica com Olá solução pré-configurada de monitorização remota] [ lnk-dynamic-telemetry] descreve como adicionar valores de telemetria personalizada, tal como *ExternalTemperature* tooyour solução.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-106">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* tooyour solution.</span></span> <span data-ttu-id="0d3f7-107">Este artigo mostra como tipos de regra personalizada de toocreate para telemetria dinâmica na sua solução.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-107">This article shows you how toocreate custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="0d3f7-108">Este tutorial utiliza um simple Node.js dispositivo simulado toogenerate telemetria dinâmica toosend toohello solução pré-configurada de back-end.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-108">This tutorial uses a simple Node.js simulated device toogenerate dynamic telemetry toosend toohello preconfigured solution back end.</span></span> <span data-ttu-id="0d3f7-109">Em seguida, adicione regras personalizadas no Olá **RemoteMonitoring** solução do Visual Studio e implementar este tooyour de back-end personalizado subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-109">You then add custom rules in hello **RemoteMonitoring** Visual Studio solution and deploy this customized back end tooyour Azure subscription.</span></span>

<span data-ttu-id="0d3f7-110">toocomplete neste tutorial, precisa de:</span><span class="sxs-lookup"><span data-stu-id="0d3f7-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="0d3f7-111">Uma subscrição ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-111">An active Azure subscription.</span></span> <span data-ttu-id="0d3f7-112">Se não tiver uma conta, pode criar uma de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0d3f7-113">Para obter mais detalhes, consulte [Azure Free Trial (Avaliação Gratuita do Azure)][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="0d3f7-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="0d3f7-114">[NODE.js] [ lnk-node] versão 0.12 ou posterior toocreate um dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-114">[Node.js][lnk-node] version 0.12.x or later toocreate a simulated device.</span></span>
* <span data-ttu-id="0d3f7-115">Visual Studio 2015 ou Visual Studio 2017 toomodify Olá pré-configurada solução de back-end com as regras de novo.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-115">Visual Studio 2015 or Visual Studio 2017 toomodify hello preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="0d3f7-116">Tome nota do nome da solução Olá que escolheu para a sua implementação.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-116">Make a note of hello solution name you chose for your deployment.</span></span> <span data-ttu-id="0d3f7-117">Terá este nome de solução mais tarde no tutorial.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="0d3f7-118">Pode parar a aplicação de consola do Node.js Olá quando tiver verificado que está a enviar **ExternalTemperature** telemetria toohello solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-118">You can stop hello Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry toohello preconfigured solution.</span></span> <span data-ttu-id="0d3f7-119">Janela de consola Olá manter abertas porque executar esta aplicação de consola do Node.js novamente depois de adicionar a solução de toohello Olá regra personalizada.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-119">Keep hello console window open because you run this Node.js console app again after you add hello custom rule toohello solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="0d3f7-120">Localizações de armazenamento de regra</span><span class="sxs-lookup"><span data-stu-id="0d3f7-120">Rule storage locations</span></span>

<span data-ttu-id="0d3f7-121">Informações sobre regras é persistente em duas localizações:</span><span class="sxs-lookup"><span data-stu-id="0d3f7-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="0d3f7-122">**DeviceRulesNormalizedTable** tabela – esta tabela armazena um normalizado regras toohello definidas pelo portal de solução Olá de referência.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference toohello rules defined by hello solution portal.</span></span> <span data-ttu-id="0d3f7-123">Quando o portal de solução Olá apresenta as regras de dispositivos, consulta esta tabela para definições de regras de Olá.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-123">When hello solution portal displays device rules, it queries this table for hello rule definitions.</span></span>
* <span data-ttu-id="0d3f7-124">**DeviceRules** blob – este blob armazena todas as regras de Olá definidas para todos os registado dispositivos e estão definidos como uma entrada toohello de referência do Azure Stream Analytics as tarefas.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-124">**DeviceRules** blob – This blob stores all hello rules defined for all registered devices and is defined as a reference input toohello Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="0d3f7-125">Quando atualizar uma regra existente ou definir uma nova regra no portal de solução Olá, tabela Olá e BLOBs são atualizados tooreflect Olá alterações.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-125">When you update an existing rule or define a new rule in hello solution portal, both hello table and blob are updated tooreflect hello changes.</span></span> <span data-ttu-id="0d3f7-126">regra de Olá definição apresentado no portal de Olá provém de arquivo de tabela Olá e regra Olá definição referenciada pelas tarefas do Stream Analytics Olá provém do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-126">hello rule definition displayed in hello portal comes from hello table store, and hello rule definition referenced by hello Stream Analytics jobs comes from hello blob.</span></span> 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="0d3f7-127">Atualizar a solução do Olá RemoteMonitoring Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0d3f7-127">Update hello RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="0d3f7-128">Olá passos seguintes mostram como toomodify Olá RemoteMonitoring Visual Studio solução tooinclude uma nova regra que utiliza Olá **ExternalTemperature** telemetria enviada do dispositivo simulado Olá:</span><span class="sxs-lookup"><span data-stu-id="0d3f7-128">hello following steps show you how toomodify hello RemoteMonitoring Visual Studio solution tooinclude a new rule that uses hello **ExternalTemperature** telemetry sent from hello simulated device:</span></span>

1. <span data-ttu-id="0d3f7-129">Se que ainda não tiver feito, Olá clone **azure-iot-remote-monitoring** localização de adequado tooa repositório no seu computador local utilizando Olá os seguintes comandos de Git:</span><span class="sxs-lookup"><span data-stu-id="0d3f7-129">If you have not already done so, clone hello **azure-iot-remote-monitoring** repository tooa suitable location on your local machine using hello following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="0d3f7-130">No Visual Studio, abra o ficheiro de RemoteMonitoring.sln de Olá da sua cópia local do Olá **azure-iot-remote-monitoring** repositório.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-130">In Visual Studio, open hello RemoteMonitoring.sln file from your local copy of hello **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="0d3f7-131">Abra o ficheiro de Olá Infrastructure\Models\DeviceRuleBlobEntity.cs e adicione um **ExternalTemperature** propriedade da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="0d3f7-131">Open hello file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="0d3f7-132">No mesmo ficheiro de Olá, adicione um **ExternalTemperatureRuleOutput** propriedade da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="0d3f7-132">In hello same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="0d3f7-133">Abra o ficheiro de Olá Infrastructure\Models\DeviceRuleDataFields.cs e adicione o seguinte Olá **ExternalTemperature** propriedade depois Olá existente **humidade** propriedade:</span><span class="sxs-lookup"><span data-stu-id="0d3f7-133">Open hello file Infrastructure\Models\DeviceRuleDataFields.cs and add hello following **ExternalTemperature** property after hello existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="0d3f7-134">No mesmo ficheiro de Olá, atualize Olá **_availableDataFields** método tooinclude **ExternalTemperature** da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="0d3f7-134">In hello same file, update hello **_availableDataFields** method tooinclude **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="0d3f7-135">Abra o ficheiro de Olá Infrastructure\Repository\DeviceRulesRepository.cs e modificar Olá **BuildBlobEntityListFromTableRows** método da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="0d3f7-135">Open hello file Infrastructure\Repository\DeviceRulesRepository.cs and modify hello **BuildBlobEntityListFromTableRows** method as follows:</span></span>

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-hello-solution"></a><span data-ttu-id="0d3f7-136">Reconstruir e voltar a implementar a solução de Olá.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-136">Rebuild and redeploy hello solution.</span></span>

<span data-ttu-id="0d3f7-137">Agora pode implementar Olá atualizado solução tooyour subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-137">You can now deploy hello updated solution tooyour Azure subscription.</span></span>

1. <span data-ttu-id="0d3f7-138">Abra uma linha de comandos elevada e navegue toohello raiz da sua cópia local do repositório azure-iot-remote-monitoring de Olá.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-138">Open an elevated command prompt and navigate toohello root of your local copy of hello azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="0d3f7-139">toodeploy solução atualizada, execute Olá os seguintes comandos substituindo **{nome da implementação}** com o nome de Olá da implementação da solução pré-configurada que apontou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="0d3f7-139">toodeploy your updated solution, run hello following command substituting **{deployment name}** with hello name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a><span data-ttu-id="0d3f7-140">Actualizar a tarefa de Stream Analytics Olá</span><span class="sxs-lookup"><span data-stu-id="0d3f7-140">Update hello Stream Analytics job</span></span>

<span data-ttu-id="0d3f7-141">Quando a implementação de Olá estiver concluída, pode atualizar Olá Stream Analytics tarefa toouse Olá novas definições de regras.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-141">When hello deployment is complete, you can update hello Stream Analytics job toouse hello new rule definitions.</span></span>

1. <span data-ttu-id="0d3f7-142">No portal do Azure Olá, navegue até toohello grupo de recursos que contém recursos da sua solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-142">In hello Azure portal, navigate toohello resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="0d3f7-143">Este grupo de recursos tem Olá mesmo nome que especificou para Olá solução durante a implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-143">This resource group has hello same name you specified for hello solution during hello deployment.</span></span>

2. <span data-ttu-id="0d3f7-144">Navegue toohello {nome da implementação}-tarefa do Stream Analytics de regras.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-144">Navigate toohello {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="0d3f7-145">Clique em **parar** tarefa de Stream Analytics Olá toostop a execução.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-145">Click **Stop** toostop hello Stream Analytics job from running.</span></span> <span data-ttu-id="0d3f7-146">(Tem de aguardar Olá de transmissão em fluxo toostop tarefa antes de poder editar consulta Olá).</span><span class="sxs-lookup"><span data-stu-id="0d3f7-146">(You must wait for hello streaming job toostop before you can edit hello query).</span></span>

4. <span data-ttu-id="0d3f7-147">Clique em **consulta**.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-147">Click **Query**.</span></span> <span data-ttu-id="0d3f7-148">Editar Olá do Olá consulta tooinclude **SELECIONE** instrução para **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-148">Edit hello query tooinclude hello **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="0d3f7-149">Olá exemplo seguinte mostra Olá concluída consulta com Olá novo **SELECIONE** instrução:</span><span class="sxs-lookup"><span data-stu-id="0d3f7-149">hello following sample shows hello complete query with hello new **SELECT** statement:</span></span>

    ```
    WITH AlarmsData AS 
    (
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Temperature' as ReadingType,
         Stream.Temperature as Reading,
         Ref.Temperature as Threshold,
         Ref.TemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Humidity' as ReadingType,
         Stream.Humidity as Reading,
         Ref.Humidity as Threshold,
         Ref.HumidityRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. <span data-ttu-id="0d3f7-150">Clique em **guardar** toochange Olá atualizado consulta de regra.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-150">Click **Save** toochange hello updated rule query.</span></span>

6. <span data-ttu-id="0d3f7-151">Clique em **iniciar** tarefa de Stream Analytics toostart Olá executar de novo.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-151">Click **Start** toostart hello Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-hello-dashboard"></a><span data-ttu-id="0d3f7-152">Adicionar a nova regra no dashboard de Olá</span><span class="sxs-lookup"><span data-stu-id="0d3f7-152">Add your new rule in hello dashboard</span></span>

<span data-ttu-id="0d3f7-153">Agora pode adicionar Olá **ExternalTemperature** dispositivo tooa de regra no dashboard de solução Olá.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-153">You can now add hello **ExternalTemperature** rule tooa device in hello solution dashboard.</span></span>

1. <span data-ttu-id="0d3f7-154">Navegue toohello portal de solução.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-154">Navigate toohello solution portal.</span></span>

2. <span data-ttu-id="0d3f7-155">Navegue toohello **dispositivos** painel.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-155">Navigate toohello **Devices** panel.</span></span>

3. <span data-ttu-id="0d3f7-156">Localizar Olá personalizadas do dispositivo que criou que envia **ExternalTemperature** telemetria e no Olá **detalhes do dispositivo** painel, clique em **Adicionar regra**.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-156">Locate hello custom device you created that sends **ExternalTemperature** telemetry and on hello **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="0d3f7-157">Selecione **ExternalTemperature** no **campo de dados**.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="0d3f7-158">Definir **limiar** too56.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-158">Set **Threshold** too56.</span></span> <span data-ttu-id="0d3f7-159">Em seguida, clique em **guardar e ver regras**.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="0d3f7-160">Devolva o histórico de alarme toohello dashboard tooview Olá.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-160">Return toohello dashboard tooview hello alarm history.</span></span>

7. <span data-ttu-id="0d3f7-161">Na janela de consola Olá que deixadas abertas, começar a enviar do Olá Node.js consola aplicação toobegin **ExternalTemperature** dados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-161">In hello console window you left open, start hello Node.js console app toobegin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="0d3f7-162">Tenha em atenção que Olá **histórico de alarme** tabela mostra alarmes novo quando nova regra de Olá é activada.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-162">Notice that hello **Alarm History** table shows new alarms when hello new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="0d3f7-163">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="0d3f7-163">Additional information</span></span>

<span data-ttu-id="0d3f7-164">Operador de Olá alteração  **>**  for mais complexo e vai mais além Olá passos descritos neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-164">Changing hello operator **>** is more complex and goes beyond hello steps outlined in this tutorial.</span></span> <span data-ttu-id="0d3f7-165">Enquanto pode alterar toouse de tarefa do Stream Analytics Olá qualquer operador pretender, ao refletir que operador no portal de solução Olá é uma tarefa de mais complexa.</span><span class="sxs-lookup"><span data-stu-id="0d3f7-165">While you can change hello Stream Analytics job toouse whatever operator you like, reflecting that operator in hello solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0d3f7-166">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0d3f7-166">Next steps</span></span>
<span data-ttu-id="0d3f7-167">Agora que viu como regras personalizadas toocreate, pode saber mais sobre soluções de Olá pré-configurada:</span><span class="sxs-lookup"><span data-stu-id="0d3f7-167">Now that you've seen how toocreate custom rules, you can learn more about hello preconfigured solutions:</span></span>

- <span data-ttu-id="0d3f7-168">[Ligar a aplicação lógica tooyour Azure IoT Suite monitorização remota pré-configurada solução][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="0d3f7-168">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="0d3f7-169">[Solução pré-configurada de metadados de informações do dispositivo na monitorização remota do Olá][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="0d3f7-169">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md