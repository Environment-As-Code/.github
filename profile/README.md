# marcomiler — Dev Environment Setup

Configuración automatizada de mi entorno de desarrollo (Linux/WSL + Windows).

---

## Arquitectura

```
┌─────────────────────────────────────────────────────────────────┐
│                    NUEVA COMPUTADORA                            │
│           Instalas: Windows + WSL2 + Ubuntu                     │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
        ┌──────────────────────────────────────┐
        │    Abre WSL Terminal                 │
        │    git clone marcomiler/dev-setup    │
        │    cd ~/.dev-setup                   │
        │    ./bootstrap.sh                    │
        └────────────┬─────────────────────────┘
                     │
         ┌───────────┴────────────┐
         │                        │
         ▼                        ▼
    ┌─────────────┐        ┌──────────────┐
    │   LINUX     │        │   WINDOWS    │
    │   (Ansible) │        │ (PowerShell) │
    └─────┬───────┘        └──────┬───────┘
          │                       │
   ✓ Base system          ✓ Brave, Firefox
   ✓ Docker Engine        ✓ Windows Terminal
   ✓ Zsh + Oh My Zsh      ✓ VS Code
   ✓ Node.js LTS + fnm    ✓ Git, DBeaver
   ✓ GitHub CLI           ✓ SQL Server, SSMS
   ✓ VS Code              ✓ Discord, Teams
   ✓ Dotfiles             ✓ PowerToys
   ✓ Git config
   ✓ Prompt (Starship)
```

---

## 🎯 Quick Start (3 pasos)

### 1️⃣ Pre-Formateo: Preparar Windows

```powershell
# En PowerShell como Administrador:
wsl --install -d Ubuntu-24.04

# Reinicia tu PC y espera a que WSL se configure
```

### 2️⃣ Post-Formateo: Ejecutar Bootstrap

```bash
# En WSL (recién formateado):
sudo apt update && sudo apt install -y git
git clone https://github.com/marcomiler/dev-setup.git ~/.dev-setup
cd ~/.dev-setup
./bootstrap.sh
```

**¿Qué hace `bootstrap.sh` automáticamente?**
- ✅ Instala Ansible (no necesitas hacerlo manualmente)
- ✅ Instala Python + dependencias
- ✅ Ejecuta todos los playbooks
- ✅ Configura Linux/WSL + Windows

### 3️⃣ Post-Bootstrap: Finalizar

```bash
# Refresca terminal (carga Zsh y fnm)
exec zsh

# Autenticar GitHub CLI
gh auth login
# → Selecciona SSH
# → Autoriza en navegador

# Verifica instalación
git --version
node --version
docker --version
code --version
```

---

## 📋 Checklist PRE-Bootstrap

- [ ] Windows 11 instalado
- [ ] WSL2 habilitado: `wsl --list --verbose` → versión 2
- [ ] Ubuntu 24.04 instalada en WSL
- [ ] Acceso a GitHub y SSH keys configuradas

---

## 📋 Checklist POST-Bootstrap

```bash
# Verifica que todo está correcto:
[ ] git --version           # ≥ 2.40
[ ] node --version          # v24+ (LTS)
[ ] npm --version           # ≥ 10
[ ] docker --version        # ≥ 24
[ ] zsh --version           # ≥ 5.9
[ ] gh --version            # ≥ 2.0
[ ] code --version          # ≥ 1.90
```

---

## 🗂️ Repositorios

- **[dev-setup](https://github.com/Environment-As-Code/dev-setup)** — Automatización con Ansible
- **[dotfiles](https://github.com/Environment-As-Code/dotfiles)** — Configuraciones personales

---

## 🚀 Qué Se Instala

### Linux/WSL
- **Sistema:** git, curl, wget, build-essential, zsh, tmux, Docker Engine
- **CLI tools:** bat, ripgrep, fd, fzf, exa, jq, tree, httpie, GitHub CLI
- **Node:** fnm + Node.js LTS (v24 Krypton)
- **Shell:** Zsh + Oh My Zsh + Powerlevel10k + plugins
- **Editor:** VS Code + extensiones

### Windows
- **Apps:** Brave, Firefox, Windows Terminal, VS Code, Git, Discord
- **DB Tools:** DBeaver, SQL Server Developer, SQL Server Management Studio
- **Utilities:** 7zip, Postman, ShareX, PowerToys, Teams, Zoom
- **VS Code:** Extensiones (Remote WSL, GitLens, Prettier, ESLint, etc.)

### Configuración
- **.gitconfig:** Usuario, email, aliases globales
- **.gitignore_global:** Reglas compartidas para todos los repos
- **.zshrc:** Aliases, plugins, integraciones
- **starship.toml:** Prompt moderno y personalizado

---

## ⚡ Información Técnica

### Arquitectura
- **bootstrap.sh:** Punto de entrada único
- **Ansible playbooks:** `linux.yml`, `windows.yml`, `site.yml`
- **Roles modulares:** base, shell, node, dotfiles, windows
- **Variables:** `group_vars/all.yml`

### Características
- ✅ **Idempotencia:** Ejecuta múltiples veces sin romper nada
- ✅ **Modular:** Agrega/quita roles según necesites
- ✅ **Versionado:** Todo en Git
- ✅ **Reutilizable:** Funciona en cualquier PC nueva

### Extensibilidad

#### Agregar Python:
```bash
cd ~/.dev-setup
vim linux.yml
# Descomenta: # - python
ansible-playbook linux.yml --ask-become-pass
```

#### Agregar Java o .NET:
```bash
# Lo mismo: descomenta en linux.yml y re-ejecuta
```

---

## 🔧 Troubleshooting

### WSL2 no está activo
```powershell
# En PowerShell como Admin:
wsl --set-default-version 2
wsl --install -d Ubuntu-24.04
```

### Terminal no carga Zsh
```bash
exec zsh
# O abre nueva terminal
```

### dotfiles no se clonan
```bash
# Verifica que el repo es privado y tienes SSH key:
ssh -T git@github.com
# Debería responder: "Hi marcomiler!"
```

### Volver a ejecutar bootstrap
```bash
cd ~/.dev-setup
ansible-playbook linux.yml --ask-become-pass
# Es seguro, Ansible es idiopotente
```

---

## 📚 Documentación Adicional

- **dev-setup README:** Estructura del proyecto, roles disponibles
- **dotfiles README:** Configuración de archivos, personalizaciones

---

## 🔐 Privacidad

Los repositorios `dev-setup` y `dotfiles` son **privados**. Este README es público para facilitar discovery.

---

**Última actualización:** Abril 2026
