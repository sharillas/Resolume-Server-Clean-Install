# Studio Master Control Suite

> **Otimização, Hardening & Blindagem de Sistema Operacional Windows para Servidores de Exibição (Resolume Arena & Pixera)**

<!-- Badges de Linguagens, Frameworks e Ferramentas -->
<p align="left">
  <img src="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/PySide6-Qt%206-41CD52?style=for-the-badge&logo=qt&logoColor=white" alt="PySide6 / Qt" />
  <img src="https://img.shields.io/badge/PowerShell-5.1%2B-5391FE?style=for-the-badge&logo=powershell&logoColor=white" alt="PowerShell" />
  <img src="https://img.shields.io/badge/Windows%20Batch-CMD-4D4D4D?style=for-the-badge&logo=windows-terminal&logoColor=white" alt="Windows Batch" />
  <img src="https://img.shields.io/badge/Win32%20API-Registry-0078D6?style=for-the-badge&logo=windows&logoColor=white" alt="Win32 API" />
  <img src="https://img.shields.io/badge/PyInstaller-Executable-FFD43B?style=for-the-badge&logo=python&logoColor=black" alt="PyInstaller" />
  <img src="https://img.shields.io/badge/Markdown-Docs-000000?style=for-the-badge&logo=markdown&logoColor=white" alt="Markdown" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License MIT" />
</p>

---

## 📌 Visão Geral

O **Studio Master Control Suite** é uma aplicação desktop portátil desenvolvida em **Python** e **PySide6** projetada especificamente para engenheiros de vídeo, VJs e técnicos de servidores de mídia (*media servers*). O objetivo principal da suíte é otimizar, blindar e eliminar potenciais gargalos de desempenho e micro-stuttering no Windows 10/11 Pro antes de shows e produções de grande porte em **Resolume Arena** e **AV Stumpfl Pixera**.

A aplicação unifica ajustes profundos de kernel via scripts **PowerShell** e comandos **Win32/Batch**, perfil de energia de GPUs (**NVIDIA RTX / Quadro** e **AMD Radeon Pro**), gerenciamento de memória virtual, desativação de telemetria/bloatware UWP e limpeza rigorosa de caches do sistema e dos motores de renderização.

---

## 🛠️ Stack Tecnológica & Linguagens Utilizadas

| Tecnologia / Linguagem | Função no Projeto |
| :--- | :--- |
| **Python 3.10+** | Linguagem principal de lógica, threading e orquestração de sistema. |
| **PySide6 (Qt 6)** | Framework para construção da interface gráfica moderna (*Skin Studio Graphite*). |
| **PowerShell** | Scripts de automação do Windows (gerenciamento de serviços, regras de Defender, remoção de pacotes AppX). |
| **Windows Batch / CMD** | Comandos diretos de terminal (`netsh`, `bcdedit`, `powercfg`, `nvidia-smi`). |
| **Win32 API & Registry** | Manipulação direta do Registro do Windows (`reg.exe` e `winreg`) para otimizações de Kernel e GPU. |
| **PyInstaller** | Compilação do código Python para um executável binário portátil estático `.exe`. |

---

## ✨ Principais Funcionalidades

### 🎮 1. Seletor de Perfil de GPU DEDICADO

* **NVIDIA Suite:** Ajusta o modo de gerenciamento de energia da placa gráfica via `nvidia-smi` para *Prefer Maximum Performance* (`nvidia-smi -pm 1; nvidia-smi --auto-boost-default=0`).
* **AMD Radeon Pro Suite:** Ajusta o perfil de energia Workstation e desativa o *PowerPlay* no registro do Windows para impedir variações bruscas de *clock* sob cargas de renderização DXV3.

### ⚙️ 2. Estabilidade Crítica de Kernel & SO

* **Plano de Energia Máximo:** Ativa e força o plano *Ultimate Performance* (`e9a42b02-d5df-448d-aa00-03f14749eb61`).
* **MPO (Multiplane Overlay):** Desativa o MPO para eliminar micro-stuttering, tearing e piscamentos de saída em múltiplos projetores ou painéis LED.
* **Win32PrioritySeparation:** Ajusta a alocação de prioridade de threads para garantir que a aplicação em primeiro plano (Resolume/Pixera) tenha prioridade total do processador (`Value 38 / 0x26`).
* **Pagefile Fixo em 16GB:** Bloqueia o arquivo de paginação em 16384 MB estáticos na unidade `C:\`, evitando fragmentação ou travamentos por expansão dinâmica de memória virtual.
* **BSOD Auto-Reboot Disabled:** Impede a reinicialização automática do sistema em caso de tela azul, mantendo o erro visível para diagnóstico imediato no estúdio.

### 🧹 3. Limpeza Profunda de Cache

* Limpeza de caches locais do **Resolume Arena** (`%LOCALAPPDATA%\Resolume Arena`).
* Purga completa de pastas temporárias do Windows (`C:\Windows\Temp` e `%TEMP%`).
* Limpeza de cache de compiladores de shaders DirectX.

### 🌐 4. Otimização de Rede para Controle (Art-Net / sACN / NDI)

* **Energy Efficient Ethernet (EEE):** Desativa globalmente a economia de energia das placas de rede via comandos PowerShell/WMI para evitar *jitter*, atrasos e perda de pacotes DMX/Ethernet durante a execução de shows ao vivo.

### 🛡️ 5. Limpeza de Bloatware & Blindagem do Defender

* **Remoção de Apps UWP:** Elimina aplicativos nativos dispensáveis via PowerShell (`Get-AppxPackage`) (Xbox Live, Cortana, Skype, Bing Weather, Zune, etc.).
* **OneDrive Disabled:** Encerra e bloqueia a inicialização do Microsoft OneDrive.
* **Windows Update Block:** Desativa e interrompe temporariamente o serviço `wuauserv` para prevenir atualizações automáticas indesejadas e reinicializações no meio de eventos.
* **Windows Defender (Modo Offline/Dedicado):** Aplica regras de política de grupo/registro para desativar a monitorização em tempo real e telemetria em ambientes isolados da internet com tratamento contra permissões de *Tamper Protection*.

### 🛠️ 6. Utilitários Integrados

* **Criador de Atalho:** Cria automaticamente um atalho funcional na Área de Trabalho com suporte a execução como Administrador.
* **LatencyMon Launcher:** Atalho de um clique para abrir ou redirecionar o operador para o LatencyMon para verificação de latência DPC.
* **Gerador de Guia de Campo (TXT):** Cria instantaneamente o arquivo `README_Guia_Campo.txt` com o checklist de pré-produção para a equipe de vídeo.

---

## 🎨 Interface Gráfica (Skin *Studio Graphite*)

A interface foi projetada com um tema escuro de alto contraste adaptado para ambientes de régia/FOH (Front of House) com pouca luz:

* **Página Inicial:** Seletor visual do modelo da GPU com dimensão compacta (`850x700`).
* **Painel de Blindagem:** Interface expansível (`900x950`) com navegação por barra de rolagem customizada.
* **Checkboxes Estilizados:** Indicadores visuais claros com ícones gráficos de *check*.
* **Barra de Progresso & Log:** Acompanhamento em tempo real das etapas executadas via `QProgressBar` e `QTextEdit` somente leitura.
* **Sem Fechamento Prematuro:** A janela permanece aberta ao término de todas as rotinas para permitir a auditoria dos logs de execução pelo operador.

---

## 🚀 Como Executar o Projeto em Desenvolvimento

### Pré-requisitos

* **Sistema Operacional:** Windows 10/11 (versão Pro recomendada).
* **Python:** 3.10 ou superior.

### Passos

1. Clone este repositório:
   ```bash
   git clone https://github.com/SEU_USUARIO/Studio-Master-Control-Suite.git
   cd Studio-Master-Control-Suite
   ```

2. Crie e ative um ambiente virtual:
   ```powershell
   python -m venv venv
   .\venv\Scripts\activate
   ```

3. Instale as dependências necessárias:
   ```bash
   pip install PySide6 pyinstaller
   ```

4. Execute a aplicação diretamente em modo de desenvolvimento (requer terminal elevado como Administrador):
   ```powershell
   python Studio_Master_Suite.py
   ```

---

## 📦 Compilação para Executável Portátil (`.exe`)

Para compilar a aplicação em um **único arquivo executável portátil** (`--onefile`) com solicitação automática de privilégios de Administrador (`--uac-admin`):

```bash
pyinstaller --onefile --uac-admin --name "Studio_Server_Master_Suite" Studio_Master_Suite.py
```

> **Nota:** O executável compilado estará localizado na pasta `dist/Studio_Server_Master_Suite.exe`.

---

## 📁 Estrutura do Repositório

```text
├── Studio_Master_Suite.py     # Script principal em Python (PySide6 GUI + Lógica Kernel/Win32)
├── README.md                  # Documentação principal com Badges e especificações
├── README_Guia_Campo.txt      # Checklist e guia de operação em campo (gerado pela ferramenta)
├── crash_log.txt              # Arquivo de log gravado automaticamente em caso de exceções
└── dist/
    └── Studio_Server_Master_Suite.exe  # Executável portátil gerado pelo PyInstaller
```

---

## 📄 Licença

Este projeto está licenciado sob a Licença **MIT**. Veja o arquivo `LICENSE` para mais detalhes.

---

<p align="center">
  <sub>Desenvolvido para máxima performance e estabilidade em eventos ao vivo e instalações imersivas.</sub>
</p>
