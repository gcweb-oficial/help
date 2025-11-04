# 🐧 Ubuntu 23.04 EOL - Correção de Repositórios e Upgrade

O Ubuntu 23.04 (Lunar Lobster) chegou ao fim do suporte (EOL - End of Life).  
Isso faz com que os repositórios padrão (`archive.ubuntu.com`, `security.ubuntu.com`) deixem de funcionar.  
Este guia mostra como corrigir o `apt` e, opcionalmente, atualizar para a versão 24.04 LTS.

---

## 🧩 1. Editar as fontes do APT

Abra o arquivo de repositórios:

```bash
sudo nano /etc/apt/sources.list
```

Substitua **todas** as linhas que começam com `deb` e `deb-src`  
pelas entradas do repositório de arquivamento:

```bash
deb http://old-releases.ubuntu.com/ubuntu/ lunar main restricted universe multiverse
deb http://old-releases.ubuntu.com/ubuntu/ lunar-updates main restricted universe multiverse
deb http://old-releases.ubuntu.com/ubuntu/ lunar-backports main restricted universe multiverse
deb http://old-releases.ubuntu.com/ubuntu/ lunar-security main restricted universe multiverse
```

Salve e feche (`Ctrl + O`, `Enter`, `Ctrl + X`).

---

## 💾 1.1. Backup e Aplicação Automática via Script

Antes de alterar o arquivo `sources.list`, faça um backup e substitua o conteúdo automaticamente com o comando abaixo:

```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup.$(date +%Y%m%d%H%M)

sudo bash -c 'cat > /etc/apt/sources.list <<EOF
deb http://old-releases.ubuntu.com/ubuntu/ lunar main restricted universe multiverse
deb http://old-releases.ubuntu.com/ubuntu/ lunar-updates main restricted universe multiverse
deb http://old-releases.ubuntu.com/ubuntu/ lunar-backports main restricted universe multiverse
deb http://old-releases.ubuntu.com/ubuntu/ lunar-security main restricted universe multiverse
EOF'
```

Este comando faz **backup automático** do arquivo atual e escreve a nova configuração corretamente.

---

## ⚙️ 2. Atualizar os pacotes

Atualize os índices e os pacotes do sistema:

```bash
sudo apt update
sudo apt upgrade -y
```

---

## 🚀 3. (Opcional) Atualizar para o Ubuntu 24.04 LTS

Para garantir suporte de longo prazo e estabilidade,  
recomenda-se migrar para a versão LTS mais recente.

Instale o gerenciador de atualização:

```bash
sudo apt install update-manager-core
```

Inicie a atualização:

```bash
sudo do-release-upgrade
```

Se o sistema não detectar automaticamente a nova versão, use o modo forçado:

```bash
sudo do-release-upgrade -d
```

---

## ✅ Resultado Esperado

Após seguir os passos:

- O `apt update` volta a funcionar normalmente.
- Você pode continuar usando o Ubuntu 23.04 ou migrar para o 24.04 LTS com suporte ativo.

---

**Referência:**  
🔗 [Ubuntu Old Releases Mirror](http://old-releases.ubuntu.com/ubuntu/)
