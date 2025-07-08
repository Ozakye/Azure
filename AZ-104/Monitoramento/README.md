# Monitoramento de Máquinas Virtuais

## Introdução

O uso de máquinas virtuais (VMs) na nuvem oferece às organizações flexibilidade, agilidade e segurança para suas operações. O Microsoft Azure, uma plataforma líder de nuvem pública, disponibiliza ferramentas completas para criar, gerenciar e monitorar VMs.

A integração com o Microsoft Entra ID (antigo Azure Active Directory) é fundamental para garantir controle de acesso seguro e eficiente. Neste artigo, abordaremos o gerenciamento de VMs no Azure com foco nessa integração, incluindo provisionamento, controle de acesso, monitoramento e boas práticas de segurança.

---

## 1. O que são VMs no Azure?

As VMs no Azure são recursos de **Infraestrutura como Serviço (IaaS)**, permitindo que você execute sistemas operacionais e aplicativos personalizados em um ambiente altamente escalável e sob demanda.

### Vantagens do uso de VMs:
- Escalabilidade rápida de recursos
- Suporte a diversos sistemas operacionais (Windows, Linux)
- Controle total sobre o ambiente
- Integração com serviços de rede, identidade e segurança

---

## 2. Criando uma VM no Azure

### Via Portal Azure:

1. Acesse [portal.azure.com](https://portal.azure.com)
2. Vá em **"Máquinas Virtuais" → "Criar"**
3. Configure os seguintes campos:
   - Grupo de Recursos
   - Nome da VM
   - Região (ex: Brazil South)
   - Imagem do sistema operacional
   - Tamanho da máquina
   - Autenticação (senha ou SSH)
4. Avance e clique em **"Revisar e Criar"**

### Via Azure CLI:

```bash
az login
az vm create \
  --resource-group MeuGrupo \
  --name MinhaVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

<br />

> **Dica:** Utilize scripts ou templates ARM para automatizar a criação em ambientes corporativos.

---

## 3. Gerenciando a VM

### Ações comuns no Portal:

- Iniciar / Parar / Reiniciar
- Conectar via RDP ou SSH
- Alterar tamanhos, discos ou configurações
- Monitorar desempenho e logs

### Via Azure CLI:

```bash
az vm start --name MinhaVM --resource-group MeuGrupo
az vm stop --name MinhaVM --resource-group MeuGrupo
```

### Via PowerShell:

```bash
Start-AzVM -ResourceGroupName "MeuGrupo" -Name "MinhaVM"
Stop-AzVM -ResourceGroupName "MeuGrupo" -Name "MinhaVM"
```

---

## 4. Automação e Scripts

Automatizar o gerenciamento de VMs reduz erros humanos e aumenta a produtividade.

### Ferramentas recomendadas:

- Azure CLI ou PowerShell
- Azure DevOps (pipelines)
- GitHub Actions
- Azure Automation
- Terraform / Bicep (infraestrutura como código)

> **Dica:** Combine scripts com agendadores (ex: Logic Apps ou Azure Automation) para ligar/desligar VMs em horários específicos e economizar recursos.

---

## 5. Monitoramento e Segurança

### Monitoramento:

- **Azure Monitor:** métricas e alertas personalizados
- **Log Analytics:** consultas sobre eventos e uso
- **Activity Log:** ações administrativas
- **Defender for Cloud:** recomendações de segurança

### Segurança:

- Crie grupos de segurança de rede (NSG) adequados
- Use identidade gerenciada (MSI) para autenticação segura
- Evite abrir portas públicas desnecessárias
- Ative logs de login e alertas

---

## 6. Boas Práticas

- Utilize naming conventions para facilitar o gerenciamento
- Defina tags para rastreamento e cobrança
- Use identidade gerenciada para acesso seguro a outros serviços
- Aplique RBAC para controle granular de permissões
- Crie snapshots ou backups regulares

---

## Conclusão

Gerenciar máquinas virtuais no Azure envolve mais do que apenas criá-las — é preciso controlar o acesso, manter a segurança, monitorar o desempenho e buscar sempre a automação. Com as ferramentas oferecidas pelo Azure, é possível construir uma infraestrutura robusta, eficiente e alinhada às melhores práticas de computação em nuvem.

Ao dominar o ciclo completo de vida de uma VM, você estará preparado para entregar soluções escaláveis e confiáveis na nuvem.

---

## Links de Referências

- [Documentação oficial do Azure VMs](https://learn.microsoft.com/azure/virtual-machines/)
- [Azure CLI Documentation](https://learn.microsoft.com/cli/azure/)
- [Azure Monitor Documentation](https://learn.microsoft.com/azure/azure-monitor/)
- [Azure Automation](https://learn.microsoft.com/azure/automation/)
- [Azure DevOps](https://azure.microsoft.com/services/devops/)
- [Terraform Azure Provider](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)
- [Azure Bicep](https://learn.microsoft.com/azure/azure-resource-manager/bicep/)
- [Microsoft Learn: Introduction to Azure VMs](https://learn.microsoft.com/learn/modules/intro-to-azure-virtual-machines/)
