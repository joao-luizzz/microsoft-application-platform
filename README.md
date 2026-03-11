# microsoft-application-platform
Documentação e infraestrutura como código (IaC) para serviços PaaS na Azure. Mais um passo na consolidação dos meus conhecimentos em desenvolvimento de sistemas e cloud computing.

# ☁️ Microsoft Application Platform - Arquitetura e Deploy na Azure

Este repositório contém o resumo prático, o desenho de arquitetura e os aprendizados obtidos durante o projeto "Microsoft Application Platform" do bootcamp da Digital Innovation One (DIO).

> **Nota de Implementação:** O foco deste repositório é documentar a infraestrutura como código (IaC), o racional arquitetural e os conceitos de serviços gerenciados. O provisionamento físico foi abstraído para focar no desenho de soluções escaláveis utilizando o ecossistema Microsoft Azure.

## 🎯 Objetivo do Projeto
O objetivo principal deste projeto é projetar e documentar o processo de construção, implantação e gerenciamento de aplicações modernas na plataforma Microsoft Azure, utilizando serviços PaaS (Platform as a Service) e tecnologias de contêinerização para garantir alta disponibilidade e fácil manutenção.

## 🏗️ Arquitetura e Serviços Utilizados
Para compor uma arquitetura moderna e alinhada com as melhores práticas de mercado (Cloud Native), os seguintes serviços foram desenhados na solução:

* **Azure App Services:** Utilizado como o host principal para aplicações web e APIs, eliminando a necessidade de gerenciamento de infraestrutura (IaaS) e oferecendo escalonamento automático.
* **Azure Container Apps:** Adotado para a execução de microsserviços em contêineres de forma serverless, garantindo agilidade no deploy sem a complexidade de um cluster Kubernetes completo (AKS).
* **Azure Storage Account / SQL Database:** Camada de persistência de dados para armazenamento de blobs e dados relacionais da aplicação.
* **Azure CLI:** Ferramenta de linha de comando utilizada para a criação e automação dos recursos, seguindo os princípios de DevOps.

## ⚙️ O Processo de Implantação (Passo a Passo)
Abaixo está o racional do fluxo de trabalho para provisionar o ambiente na nuvem:

1. **Criação do Resource Group (Grupo de Recursos):**
   Agrupamento lógico de todos os recursos do projeto para facilitar o monitoramento e o gerenciamento de custos.
   * *Comando de exemplo:* `az group create --name myResourceGroup --location eastus`

2. **Provisionamento do App Service Plan:**
   Definição da capacidade computacional (tamanho da máquina e tier de preço) que hospedará as aplicações web.
   * *Comando de exemplo:* `az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1 --is-linux`

3. **Deploy do Web App (App Service):**
   Criação da instância do aplicativo web vinculada ao plano de serviço criado anteriormente.
   * *Comando de exemplo:* `az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name myUniqueAppName --runtime "NODE|18-lts"`

4. **Configuração de Contêineres (Container Apps):**
   Para a camada de microsserviços, o ambiente de Container Apps foi provisionado para rodar imagens Docker a partir do Azure Container Registry (ACR) ou Docker Hub.

![Arquitetura Azure](https://learn.microsoft.com/pt-br/azure/architecture/guide/technology-choices/images/compute-choices.png)

## 💡 Insights e Aprendizados
Durante o desenho e estudo desta arquitetura, destaco:
* **Poder do PaaS:** O App Services abstrai configurações complexas de SO e rede, permitindo que o time de desenvolvimento foque 100% no código.
* **Evolução com Contêineres:** O Azure Container Apps é o "meio-termo" perfeito para quem precisa rodar contêineres na nuvem sem precisar administrar a complexidade do Azure Kubernetes Service (AKS).
* **Automação é chave:** A utilização do Azure CLI acelera drasticamente o processo de recriação de ambientes e evita erros humanos causados por cliques manuais no Portal do Azure.

## 🚀 Possibilidades Futuras
Como melhoria arquitetural para este ecossistema, o projeto poderia evoluir com:
* Implementação de uma esteira CI/CD completa utilizando **GitHub Actions** para automatizar o build e o deploy direto no App Service.
* Adição do **Azure Key Vault** para gerenciar de forma segura senhas, chaves de API e connection strings.
* Configuração do **Azure Front Door** como ponto de entrada global para balanceamento de carga e proteção contra ataques DDoS.
