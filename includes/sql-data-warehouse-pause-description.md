
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="9d5b9-101">custos de toosave, pode colocar em pausa e retomar computação recursos a pedido.</span><span class="sxs-lookup"><span data-stu-id="9d5b9-101">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="9d5b9-102">Por exemplo, se não utilizar a base de dados de Olá durante a noite Olá e no fim de semana, pode colocar em pausa-lo durante essas horas e retomá-lo durante o dia de Olá.</span><span class="sxs-lookup"><span data-stu-id="9d5b9-102">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="9d5b9-103">Não lhe será cobrado dwus enquanto a base de dados de Olá está em pausa.</span><span class="sxs-lookup"><span data-stu-id="9d5b9-103">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="9d5b9-104">Quando colocar em pausa uma base de dados:</span><span class="sxs-lookup"><span data-stu-id="9d5b9-104">When you pause a database:</span></span>

* <span data-ttu-id="9d5b9-105">Recursos de computação e memória são devolvidos toohello agrupamento de recursos disponíveis no Centro de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="9d5b9-105">Compute and memory resources are returned toohello pool of available resources in hello data center</span></span>
* <span data-ttu-id="9d5b9-106">Os custos DWU são zero Olá enquanto estiver em curso pausa Olá.</span><span class="sxs-lookup"><span data-stu-id="9d5b9-106">DWU costs are zero for hello duration of hello pause.</span></span>
* <span data-ttu-id="9d5b9-107">Armazenamento de dados não é afetado e os dados permanecem intactos.</span><span class="sxs-lookup"><span data-stu-id="9d5b9-107">Data storage is not affected and your data stays intact.</span></span> 
* <span data-ttu-id="9d5b9-108">O SQL Data Warehouse cancela todas as operações em execução ou em fila.</span><span class="sxs-lookup"><span data-stu-id="9d5b9-108">SQL Data Warehouse cancels all running or queued operations.</span></span>

