# Gerenciamento de Máquinas Virtuais

## Introdução

O uso de máquinas virtuais (VMs) na nuvem permite às organizações escalar suas operações com flexibilidade, agilidade e segurança. O Microsoft Azure, como uma das principais plataformas de nuvem pública, oferece um amplo conjunto de ferramentas para provisionamento, gerenciamento e monitoramento de VMs. Um aspecto fundamental do gerenciamento moderno de VMs é a integração com serviços de identidade e acesso — e é aí que entra o **Microsoft Entra ID** (anteriormente conhecido como Azure Active Directory).

Neste artigo, abordaremos os principais aspectos do gerenciamento de VMs no Azure, com integração do Microsoft Entra ID, incluindo provisionamento, controle de acesso, monitoramento e boas práticas de segurança.

---

## 1. Conceitos Básicos

### O que é uma Máquina Virtual (VM) no Azure?

Uma máquina virtual no Azure é uma instância de computação baseada em infraestrutura como serviço (IaaS). Com ela, é possível executar sistemas operacionais Windows ou Linux e aplicativos em uma infraestrutura escalável e globalmente disponível.

### O que é o Microsoft Entra ID?

O **Microsoft Entra ID** (antigo Azure AD) é o serviço de gerenciamento de identidades baseado na nuvem da Microsoft. Ele permite a autenticação de usuários, gerenciamento de permissões e acesso condicional a recursos do Azure.

---

## 2. Provisionamento de VMs no Azure

### Etapas Básicas:

1. **Escolha da imagem base** (Windows, Ubuntu, etc.)
2. **Configuração de tamanho e recursos** (CPU, RAM, disco)
3. **Definição de rede virtual e sub-rede**
4. **Criação ou associação de grupo de segurança de rede (NSG)**
5. **Configuração de autenticação:**
   - Senha local
   - **Autenticação com Microsoft Entra ID**

<br />

> **Dica**: Habilitar o login com Entra ID no momento da criação da VM garante melhor integração com políticas organizacionais e segurança baseada em identidade.

---

## 3. Integração da VM com o Microsoft Entra ID

### Pré-requisitos:

- Uma assinatura ativa do Azure
- Uma VM compatível (Windows Server 2019/2022 ou Windows 10/11)
- Microsoft Entra ID Premium P1 ou P2 (para alguns recursos avançados)
- Extensão de login habilitada na VM

### Como habilitar o login com Entra ID:

1. Ao criar a VM, vá até a aba **"Identity"**.
2. Ative a opção **"Login com Entra ID" (Azure AD login)**.
3. Habilite a **Identidade Gerenciada (Managed Identity)** — isso permite à VM autenticar-se em outros serviços do Azure sem armazenar credenciais.

---

## 4. Gerenciamento de Acesso com RBAC e Entra ID

### Controle Baseado em Funções (RBAC)

O Azure oferece um modelo de **Role-Based Access Control (RBAC)**, no qual você define quem pode fazer o quê, com base em funções atribuídas a identidades.

#### Funções comuns para VMs:
- **Owner** – Permite o acesso completo para gerenciar todos os recursos, incluindo a capacidade de atribuir funções no RBAC.
- **Role Based Access Control Administrator** – Permite que você gerencie o acesso do usuário aos recursos do Azure.
- **User Access Administrator** – Permite que você gerencie o acesso do usuário aos recursos do Azure.
- **Contributor** – Permite o acesso completo para gerenciar todos os recursos, mas não permite atribuir funções no RBAC.
- **Reader** – Permite somente a leitura dos recursos, não podendo fazer nenhuma alteração.

### Atribuição de papéis:

1. Vá até a VM no portal do Azure.
2. Selecione **"Controle de Acesso (IAM)"**.
3. Clique em **"Adicionar atribuição de função"**.
4. Escolha a função (por exemplo, "VM User Login") e selecione o usuário/grupo do Entra ID.

---

## 5. Autenticação e Login na VM

### Com Entra ID:

- Usuários autorizados podem fazer login na VM usando **seu e-mail corporativo e senha do Entra ID**.
- Suporte a **autenticação multifator (MFA)**, login com certificado e biometria (via Windows Hello).
- Uso do **Windows Admin Center** ou **Remote Desktop (RDP)** com autenticação Entra ID.

---

## 6. Monitoramento e Auditoria

### Ferramentas disponíveis:

- **Azure Monitor** – coleta métricas e logs das VMs.
- **Azure Log Analytics** – permite consultas sobre logs de atividade.
- **Defender for Cloud** – recomendações de segurança e análise de vulnerabilidades.
- **Activity Logs** – registra ações administrativas (incluindo login e alterações de configuração).

---

## 7. Práticas Recomendadas

- **Evite senhas locais**: use autenticação Entra ID sempre que possível.
- **Habilite a identidade gerenciada** da VM para acesso seguro a outros recursos (ex: Key Vault, Storage).
- **Implemente políticas de acesso condicional** com base em localização, dispositivo ou risco.
- **Audite acessos regularmente** com Azure AD Sign-In Logs.
- **Utilize grupos para atribuição de acesso** em larga escala.

---

## Conclusão

Integrar o gerenciamento de máquinas virtuais ao Microsoft Entra ID proporciona maior controle, segurança e escalabilidade. Essa abordagem se alinha com a visão moderna de "segurança baseada em identidade", essencial em ambientes de nuvem.

Ao usar os recursos nativos do Azure e do Entra ID, as organizações podem simplificar a administração, reduzir a dependência de credenciais locais e aplicar políticas de segurança mais consistentes e eficazes.

---

## Links de Referências

- [Documentação oficial do Azure Virtual Machines](https://learn.microsoft.com/azure/virtual-machines)
- [O que é o gerenciamento de VM local do Azure?](https://learn.microsoft.com/pt-br/azure/azure-local/manage/azure-arc-vm-management-overview?view=azloc-2505)
- [Gerenciar máquinas virtuais do Azure](https://learn.microsoft.com/pt-br/system-center/vmm/manage-azure-vms)
- [Criar e gerenciar as VMs do Windows com o Azure PowerShell](https://learn.microsoft.com/pt-br/azure/virtual-machines/windows/tutorial-manage-vm)
- [Gerenciar uma VM do Windows usando o Windows Admin Center no Azure](https://learn.microsoft.com/pt-br/windows-server/manage/windows-admin-center/azure/manage-vm)
- [Gerencie VMs usando autenticação e autorização baseadas em ID do Microsoft Entra e assinaturas do Azure específicas da região](https://learn.microsoft.com/pt-br/system-center/vmm/vms-manage-azure-ad-and-region-specific)
