---
title: O padrão DevOps no Hub Azure Stack
description: Saiba mais sobre o padrão DevOps para que você possa garantir a consistência entre implantações no Azure e no Hub Azure Stack.
author: BryanLa
ms.topic: article
ms.date: 11/05/2019
ms.author: bryanla
ms.reviewer: anajod
ms.lastreviewed: 11/05/2019
ms.openlocfilehash: 306cc9604a8e919724f9f76b7e5122d534d2d1ae
ms.sourcegitcommit: bb3e40b210f86173568a47ba18c3cc50d4a40607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84909819"
---
# <a name="devops-pattern"></a><span data-ttu-id="713af-103">Padrão DevOps</span><span class="sxs-lookup"><span data-stu-id="713af-103">DevOps pattern</span></span>

<span data-ttu-id="713af-104">Codifique a partir de um único local e implante em vários destinos em ambientes de desenvolvimento, teste e produção que podem estar em seu datacenter local, em nuvens privadas ou na nuvem pública.</span><span class="sxs-lookup"><span data-stu-id="713af-104">Code from a single location and deploy to multiple targets in development, test, and production environments that may be in your local datacenter, private clouds, or the public cloud.</span></span>

## <a name="context-and-problem"></a><span data-ttu-id="713af-105">Contexto e problema</span><span class="sxs-lookup"><span data-stu-id="713af-105">Context and problem</span></span>

<span data-ttu-id="713af-106">A continuidade, a segurança e a confiabilidade da implantação de aplicativos são essenciais para as organizações e para as equipes de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="713af-106">Application deployment continuity, security, and reliability are essential to organizations and critical to development teams.</span></span>

<span data-ttu-id="713af-107">Os aplicativos geralmente exigem código refatorado para serem executados em cada ambiente de destino.</span><span class="sxs-lookup"><span data-stu-id="713af-107">Apps often require refactored code to run in each target environment.</span></span> <span data-ttu-id="713af-108">Isso significa que um aplicativo não é completamente portátil.</span><span class="sxs-lookup"><span data-stu-id="713af-108">This means that an app isn't completely portable.</span></span> <span data-ttu-id="713af-109">Ele deve ser atualizado, testado e validado à medida que se move em cada ambiente.</span><span class="sxs-lookup"><span data-stu-id="713af-109">It must be updated, tested, and validated as it moves through each environment.</span></span> <span data-ttu-id="713af-110">Por exemplo, o código escrito em um ambiente de desenvolvimento deve ser reescrito para funcionar em um ambiente de teste e reescrito quando ele finalmente chega em um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="713af-110">For example, code written in a development environment must then be rewritten to work in a test environment and rewritten when it finally lands in a production environment.</span></span> <span data-ttu-id="713af-111">Além disso, esse código está especificamente vinculado ao host.</span><span class="sxs-lookup"><span data-stu-id="713af-111">Furthermore, this code is specifically tied to the host.</span></span> <span data-ttu-id="713af-112">Isso aumenta o custo e a complexidade de manter seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="713af-112">This increases the cost and complexity of maintaining your app.</span></span> <span data-ttu-id="713af-113">Cada versão do aplicativo é vinculada a cada ambiente.</span><span class="sxs-lookup"><span data-stu-id="713af-113">Each version of the app is tied to each environment.</span></span> <span data-ttu-id="713af-114">A maior complexidade e a duplicação aumentam o risco de segurança e qualidade de código.</span><span class="sxs-lookup"><span data-stu-id="713af-114">The increased complexity and duplication increase the risk of security and code quality.</span></span> <span data-ttu-id="713af-115">Além disso, o código não pode ser reimplantado prontamente quando você remove os hosts com falha de restauração ou implanta hosts adicionais para lidar com aumentos na demanda.</span><span class="sxs-lookup"><span data-stu-id="713af-115">In addition, the code can't be readily redeployed when you remove restore failed hosts or deploy additional hosts to handle increases in demand.</span></span>

## <a name="solution"></a><span data-ttu-id="713af-116">Solução</span><span class="sxs-lookup"><span data-stu-id="713af-116">Solution</span></span>

<span data-ttu-id="713af-117">O padrão DevOps permite criar, testar e implantar um aplicativo que é executado em várias nuvens.</span><span class="sxs-lookup"><span data-stu-id="713af-117">The DevOps Pattern enables you to build, test, and deploy an app that runs on multiple clouds.</span></span> <span data-ttu-id="713af-118">Esse padrão une a prática da integração contínua e da entrega contínua.</span><span class="sxs-lookup"><span data-stu-id="713af-118">This pattern unites the practice of continuous integration and continuous delivery.</span></span> <span data-ttu-id="713af-119">Com a integração contínua, o código é criado e testado toda vez que um membro da equipe confirma uma alteração no controle de versão.</span><span class="sxs-lookup"><span data-stu-id="713af-119">With continuous integration, code is built and tested every time a team member commits a change to version control.</span></span> <span data-ttu-id="713af-120">A entrega contínua automatiza cada etapa de um Build para um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="713af-120">Continuous delivery automates each step from a build to a production environment.</span></span> <span data-ttu-id="713af-121">Juntos, esses processos criam um processo de liberação que dá suporte à implantação em diversos ambientes.</span><span class="sxs-lookup"><span data-stu-id="713af-121">Together, these processes create a release process that supports deployment across diverse environments.</span></span> <span data-ttu-id="713af-122">Com esse padrão, você pode rascunhar seu código e, em seguida, implantar o mesmo código em um ambiente premisso, diferentes nuvens privadas e as nuvens públicas.</span><span class="sxs-lookup"><span data-stu-id="713af-122">With this pattern, you can draft your code and then deploy the same code to a premise environment, different private clouds, and the public clouds.</span></span> <span data-ttu-id="713af-123">As diferenças no ambiente exigem uma alteração em um arquivo de configuração em vez de alterações no código.</span><span class="sxs-lookup"><span data-stu-id="713af-123">Differences in environment require a change to a configuration file rather than changes to the code.</span></span>

![Padrão DevOps](media/pattern-cicd-pipeline/hybrid-ci-cd.png)

<span data-ttu-id="713af-125">Com um conjunto consistente de ferramentas de desenvolvimento em ambientes locais, de nuvem privada e de nuvem pública, você pode implementar uma prática de integração contínua e entrega contínua.</span><span class="sxs-lookup"><span data-stu-id="713af-125">With a consistent set of development tools across on-premises, private cloud, and public cloud environments, you can implement a practice of continuous integration and continuous delivery.</span></span> <span data-ttu-id="713af-126">Os aplicativos e serviços implantados usando o padrão DevOps são intercambiáveis e podem ser executados em qualquer um desses locais, tirando proveito dos recursos e funcionalidades de nuvem pública e local.</span><span class="sxs-lookup"><span data-stu-id="713af-126">Apps and services deployed using the DevOps Pattern are interchangeable and can run in any of these locations, taking advantage of on-premises and public cloud features and capabilities.</span></span>

<span data-ttu-id="713af-127">O uso de um pipeline de liberação do DevOps ajuda você a:</span><span class="sxs-lookup"><span data-stu-id="713af-127">Using a DevOps release pipeline helps you:</span></span>

- <span data-ttu-id="713af-128">Inicie uma nova compilação com base em confirmações de código em um único repositório.</span><span class="sxs-lookup"><span data-stu-id="713af-128">Initiate a new build based on code commits to a single repository.</span></span>
- <span data-ttu-id="713af-129">Implante automaticamente seu código recém-criado na nuvem pública para o teste de aceitação do usuário.</span><span class="sxs-lookup"><span data-stu-id="713af-129">Automatically deploy your newly built code to the public cloud for user acceptance testing.</span></span>
- <span data-ttu-id="713af-130">Implante automaticamente em uma nuvem privada depois que seu código passar por testes.</span><span class="sxs-lookup"><span data-stu-id="713af-130">Automatically deploy to a private cloud once your code has passed testing.</span></span>

## <a name="issues-and-considerations"></a><span data-ttu-id="713af-131">Problemas e considerações</span><span class="sxs-lookup"><span data-stu-id="713af-131">Issues and considerations</span></span>

<span data-ttu-id="713af-132">O padrão DevOps destina-se a garantir a consistência entre implantações, independentemente do ambiente de destino.</span><span class="sxs-lookup"><span data-stu-id="713af-132">The DevOps Pattern is intended to ensure consistency across deployments regardless of the target environment.</span></span> <span data-ttu-id="713af-133">No entanto, os recursos variam em ambientes de nuvem e locais.</span><span class="sxs-lookup"><span data-stu-id="713af-133">However, capabilities vary across cloud and on-premises environments.</span></span> <span data-ttu-id="713af-134">Considere os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="713af-134">Consider the following points:</span></span>

- <span data-ttu-id="713af-135">As funções, os pontos de extremidade, os serviços e outros recursos em sua implantação estão disponíveis nos locais de implantação de destino?</span><span class="sxs-lookup"><span data-stu-id="713af-135">Are the functions, endpoints, services, and other resources in your deployment available in the target deployment locations?</span></span>
- <span data-ttu-id="713af-136">Os artefatos de configuração são armazenados em locais acessíveis entre nuvens?</span><span class="sxs-lookup"><span data-stu-id="713af-136">Are configuration artifacts stored in locations that are accessible across clouds?</span></span>
- <span data-ttu-id="713af-137">Os parâmetros de implantação funcionarão em todos os ambientes de destino?</span><span class="sxs-lookup"><span data-stu-id="713af-137">Will deployment parameters work in all the target environments?</span></span>
- <span data-ttu-id="713af-138">As propriedades específicas do recurso estão disponíveis em todas as nuvens de destino?</span><span class="sxs-lookup"><span data-stu-id="713af-138">Are resource-specific properties available in all target clouds?</span></span>

<span data-ttu-id="713af-139">Para obter mais informações, consulte [desenvolver modelos de Azure Resource Manager para consistência de nuvem](https://docs.microsoft.com/azure/azure-resource-manager/templates-cloud-consistency).</span><span class="sxs-lookup"><span data-stu-id="713af-139">For more information, see [Develop Azure Resource Manager templates for cloud consistency](https://docs.microsoft.com/azure/azure-resource-manager/templates-cloud-consistency).</span></span>

<span data-ttu-id="713af-140">Além disso, considere os seguintes pontos ao decidir como implementar esse padrão:</span><span class="sxs-lookup"><span data-stu-id="713af-140">In addition, consider the following points when deciding how to implement this pattern:</span></span>

### <a name="scalability"></a><span data-ttu-id="713af-141">Escalabilidade</span><span class="sxs-lookup"><span data-stu-id="713af-141">Scalability</span></span>

<span data-ttu-id="713af-142">Os sistemas de automação de implantação são o ponto de controle principal nos padrões de DevOps.</span><span class="sxs-lookup"><span data-stu-id="713af-142">Deployment automation systems are the key control point in the DevOps Patterns.</span></span> <span data-ttu-id="713af-143">As implementações podem variar.</span><span class="sxs-lookup"><span data-stu-id="713af-143">Implementations can vary.</span></span> <span data-ttu-id="713af-144">A seleção do tamanho do servidor correto depende do tamanho da carga de trabalho esperada.</span><span class="sxs-lookup"><span data-stu-id="713af-144">The selection of the correct server size depends on the size of the expected workload.</span></span> <span data-ttu-id="713af-145">As VMs custam mais para dimensionar os contêineres.</span><span class="sxs-lookup"><span data-stu-id="713af-145">VMs cost more to scale than containers.</span></span> <span data-ttu-id="713af-146">Para usar os contêineres para o dimensionamento, no entanto, o processo de compilação deve executar com os contêineres.</span><span class="sxs-lookup"><span data-stu-id="713af-146">To use containers for scaling, however, your build process must run with containers.</span></span>

### <a name="availability"></a><span data-ttu-id="713af-147">Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="713af-147">Availability</span></span>

<span data-ttu-id="713af-148">A disponibilidade no contexto do DevPattern significa ser capaz de recuperar qualquer informação de estado associada ao fluxo de trabalho, como resultados de teste, dependências de código ou outros artefatos.</span><span class="sxs-lookup"><span data-stu-id="713af-148">Availability in the context of the DevPattern means being able to recover any state information associated with your workflow, such as test results, code dependencies, or other artifacts.</span></span> <span data-ttu-id="713af-149">Para avaliar seus requisitos de disponibilidade, considere duas métricas comuns:</span><span class="sxs-lookup"><span data-stu-id="713af-149">To assess your availability requirements, consider two common metrics:</span></span>

- <span data-ttu-id="713af-150">O RTO (objetivo de tempo de recuperação) especifica por quanto tempo você pode ir sem um sistema.</span><span class="sxs-lookup"><span data-stu-id="713af-150">Recovery Time Objective (RTO) specifies how long you can go without a system.</span></span>

- <span data-ttu-id="713af-151">O RPO (objetivo de ponto de recuperação) indica a quantidade de dados que você pode perder se uma interrupção no serviço afetar o sistema.</span><span class="sxs-lookup"><span data-stu-id="713af-151">Recovery Point Objective (RPO) indicates how much data you can afford to lose if a disruption in service affects the system.</span></span>

<span data-ttu-id="713af-152">Na prática, o RTO e o RPO implicam redundância e backup.</span><span class="sxs-lookup"><span data-stu-id="713af-152">In practice, RTO, and RPO imply redundancy and backup.</span></span> <span data-ttu-id="713af-153">Na nuvem global do Azure, a disponibilidade não é uma questão de recuperação de hardware — que faz parte do Azure — mas, em vez disso, garante que você mantenha o estado dos seus sistemas DevOps.</span><span class="sxs-lookup"><span data-stu-id="713af-153">On the global Azure cloud, availability isn't a question of hardware recovery—that's part of Azure—but rather ensuring you maintain the state of your DevOps systems.</span></span> <span data-ttu-id="713af-154">No Hub Azure Stack, a recuperação de hardware pode ser uma consideração.</span><span class="sxs-lookup"><span data-stu-id="713af-154">On Azure Stack Hub, hardware recovery may be a consideration.</span></span>

<span data-ttu-id="713af-155">Outra consideração importante ao criar o sistema usado para a automação da implantação é o controle de acesso e o gerenciamento adequado dos direitos necessários para implantar serviços em ambientes de nuvem.</span><span class="sxs-lookup"><span data-stu-id="713af-155">Another major consideration when designing the system used for deployment automation is access control and the proper management of the rights needed to deploy services to cloud environments.</span></span> <span data-ttu-id="713af-156">Quais direitos são necessários para criar, excluir ou modificar implantações?</span><span class="sxs-lookup"><span data-stu-id="713af-156">What rights are needed to create, delete, or modify deployments?</span></span> <span data-ttu-id="713af-157">Por exemplo, um conjunto de direitos normalmente é necessário para criar um grupo de recursos no Azure e outro para implantar serviços no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="713af-157">For example, one set of rights is typically required to create a resource group in Azure and another to deploy services in the resource group.</span></span>

### <a name="manageability"></a><span data-ttu-id="713af-158">Capacidade de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="713af-158">Manageability</span></span>

<span data-ttu-id="713af-159">O design de qualquer sistema baseado no padrão DevOps deve considerar a automação, o registro em log e o alerta para cada serviço em todo o portfólio.</span><span class="sxs-lookup"><span data-stu-id="713af-159">The design of any system based on the DevOps pattern must consider automation, logging, and alerting for each service across the portfolio.</span></span> <span data-ttu-id="713af-160">Use serviços compartilhados, uma equipe de aplicativos, ou ambos, e acompanhe políticas de segurança e governança também.</span><span class="sxs-lookup"><span data-stu-id="713af-160">Use shared services, an application team, or both, and track security policies and governance as well.</span></span>

<span data-ttu-id="713af-161">Implante ambientes de produção e ambientes de desenvolvimento/teste em grupos de recursos separados no Azure ou no Hub de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="713af-161">Deploy production environments and development/test environments in separate resource groups on Azure or Azure Stack Hub.</span></span> <span data-ttu-id="713af-162">Em seguida, você pode monitorar os recursos de cada ambiente e acumular os custos de cobrança por grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="713af-162">Then you can monitor each environment's resources and roll up billing costs by resource group.</span></span> <span data-ttu-id="713af-163">Também é possível excluir recursos como um conjunto, o que é útil para implantações de teste.</span><span class="sxs-lookup"><span data-stu-id="713af-163">You can also delete resources as a set, which is useful for test deployments.</span></span>

## <a name="when-to-use-this-pattern"></a><span data-ttu-id="713af-164">Quando usar esse padrão</span><span class="sxs-lookup"><span data-stu-id="713af-164">When to use this pattern</span></span>

<span data-ttu-id="713af-165">Use esse padrão se:</span><span class="sxs-lookup"><span data-stu-id="713af-165">Use this pattern if:</span></span>

- <span data-ttu-id="713af-166">Você pode desenvolver código em um ambiente que atenda às necessidades de seus desenvolvedores e implantar em um ambiente específico para sua solução, onde pode ser difícil desenvolver um novo código.</span><span class="sxs-lookup"><span data-stu-id="713af-166">You can develop code in one environment that meets the needs of your developers, and deploy to an environment specific to your solution where it may be difficult to develop new code.</span></span>
- <span data-ttu-id="713af-167">Você pode usar o código e as ferramentas que seus desenvolvedores desejam, contanto que eles possam seguir o processo de integração contínua e de entrega contínua no padrão DevOps.</span><span class="sxs-lookup"><span data-stu-id="713af-167">You can use the code and tools your developers would like, as long as they're able to follow the continuous integration and continuous delivery process in the DevOps Pattern.</span></span>

<span data-ttu-id="713af-168">Este padrão não é recomendável:</span><span class="sxs-lookup"><span data-stu-id="713af-168">This pattern isn't recommended:</span></span>

- <span data-ttu-id="713af-169">Se você não puder automatizar a infraestrutura, o provisionamento de recursos, a configuração, a identidade e as tarefas de segurança.</span><span class="sxs-lookup"><span data-stu-id="713af-169">If you can't automate infrastructure, provisioning resources, configuration, identity, and security tasks.</span></span>
- <span data-ttu-id="713af-170">Se as equipes não tiverem acesso aos recursos de nuvem híbrida para implementar uma abordagem de CI/CD (integração contínua/desenvolvimento contínuo).</span><span class="sxs-lookup"><span data-stu-id="713af-170">If teams don't have access to hybrid cloud resources to implement a Continuous Integration/Continuous Development (CI/CD) approach.</span></span>

## <a name="next-steps"></a><span data-ttu-id="713af-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="713af-171">Next steps</span></span>

<span data-ttu-id="713af-172">Para saber mais sobre os tópicos apresentados neste artigo:</span><span class="sxs-lookup"><span data-stu-id="713af-172">To learn more about topics introduced in this article:</span></span>

- <span data-ttu-id="713af-173">Consulte a [documentação do Azure DevOps](/azure/devops) para saber mais sobre as DevOps do Azure e as ferramentas relacionadas, incluindo Azure Repos e Azure pipelines.</span><span class="sxs-lookup"><span data-stu-id="713af-173">See the [Azure DevOps documentation](/azure/devops) to learn more about Azure DevOps and related tools, including Azure Repos, and Azure Pipelines.</span></span>
- <span data-ttu-id="713af-174">Consulte a [família de produtos e soluções Azure Stack](/azure-stack) para saber mais sobre todo o portfólio de produtos e soluções.</span><span class="sxs-lookup"><span data-stu-id="713af-174">See the [Azure Stack family of products and solutions](/azure-stack) to learn more about the entire portfolio of products and solutions.</span></span>

<span data-ttu-id="713af-175">Quando você estiver pronto para testar o exemplo de solução, continue com o [Guia de implantação da solução de CI/CD híbrido do DevOps](https://aka.ms/hybriddevopsdeploy).</span><span class="sxs-lookup"><span data-stu-id="713af-175">When you're ready to test the solution example, continue with the [DevOps hybrid CI/CD solution deployment guide](https://aka.ms/hybriddevopsdeploy).</span></span> <span data-ttu-id="713af-176">O guia de implantação fornece instruções passo a passo para implantar e testar seus componentes.</span><span class="sxs-lookup"><span data-stu-id="713af-176">The deployment guide provides step-by-step instructions for deploying and testing its components.</span></span> <span data-ttu-id="713af-177">Você aprende a implantar um aplicativo no Azure e no Hub de Azure Stack usando um pipeline de CI/CD (integração contínua/entrega contínua).</span><span class="sxs-lookup"><span data-stu-id="713af-177">You learn how to deploy an app to Azure and Azure Stack Hub using a hybrid continuous integration/continuous delivery (CI/CD) pipeline.</span></span>