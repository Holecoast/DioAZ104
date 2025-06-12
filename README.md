# DioAZ104

# Criando uma Máquina Virtual no Azure: `testDioAz`

Este guia explica passo a passo como criar uma máquina virtual chamada `testDioAz` no Microsoft Azure, utilizando o portal web ou a CLI do Azure.

---

## Pré-requisitos

Antes de começar, você precisa ter:

- Uma conta Microsoft com acesso ao [Azure Portal](https://portal.azure.com)
- Uma assinatura ativa do Azure
- (Opcional) Azure CLI instalado ([instalar](https://learn.microsoft.com/pt-br/cli/azure/install-azure-cli))

---

## Opção 1: Criando a VM pelo Portal do Azure

1. Acesse o [Azure Portal](https://portal.azure.com).
2. No menu lateral esquerdo, clique em **"Máquinas Virtuais"**.
3. Clique em **"Criar" > "Máquina virtual"**.
4. Preencha as seguintes informações:

   - **Assinatura**: escolha a sua assinatura
   - **Grupo de Recursos**: crie ou selecione um existente
   - **Nome da VM**: `testDioAz`
   - **Região**: selecione uma próxima de você (ex: "Brazil South")
   - **Imagem**: `Ubuntu Server 22.04 LTS` (ou outra de sua preferência)
   - **Tamanho**: escolha uma adequada (ex: `Standard B1s`)
   - **Usuário administrador**: defina um nome de usuário e senha ou chave SSH
   - **Portas de entrada públicas**: permita SSH (porta 22)

5. Clique em **"Revisar + Criar"**, verifique os detalhes e clique em **"Criar"**.

---

## Opção 2: Criando a VM com Azure CLI

Se preferir usar a linha de comando, siga os passos abaixo:

### 1. Login no Azure

```bash
az login
```

### 2. Criar um grupo de recursos (caso necessário)

```bash
az group create --name MeuGrupoRecursos --location brazilsouth
```

### 3. Criar a máquina virtual

```bash
az vm create \
  --resource-group MeuGrupoRecursos \
  --name testDioAz \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys \
  --location brazilsouth
```

> Isso criará uma VM chamada `testDioAz` com Ubuntu, chave SSH e acesso via SSH liberado.

---

## Acessando a VM

Após criada, obtenha o IP público:

```bash
az vm show --resource-group MeuGrupoRecursos --name testDioAz -d --query publicIps -o tsv
```

Acesse via SSH:

```bash
ssh azureuser@<IP_PUBLICO>
```
