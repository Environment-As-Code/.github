# marcomiler — Dev Environment Setup

Automatizacion de entorno de desarrollo con Ansible para Linux/WSL y Windows.

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

## Quick start

```bash
sudo apt update && sudo apt install -y git
git clone https://github.com/Environment-As-Code/dev-setup.git ~/.dev-setup
cd ~/.dev-setup
./bootstrap.sh
```

---

## Configuracion basica

Revisa los valores en [group_vars/all.yml](group_vars/all.yml):

```yaml
linux_user: "{{ ansible_facts['user_id'] }}"
dotfiles_repo: "git@github.com:Environment-As-Code/dotfiles.git"
node_lts_version: "lts/krypton"    # Node 24 LTS
```

---

## SSH (dotfiles privados)

```bash
ssh-keygen -t ed25519 -C "tu_email@dominio.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519.pub
```

Agrega la clave en GitHub y prueba:

```bash
ssh -T git@github.com
```

---

## Ejecutar playbooks

```bash
ansible-playbook linux.yml --ask-become-pass
ansible-playbook windows.yml
ansible-playbook site.yml --ask-become-pass
```

---

## Verificacion rapida

```bash
git --version
node --version
docker --version
gh --version
code --version
```

---

## Notas

- Si ves el warning de "world writable", ejecuta: `chmod o-w ~/.dev-setup`.
- Si la terminal muestra simbolos raros, instala una Nerd Font (ej: FiraCode Nerd Font) en Windows Terminal o VS Code.

---

## Repositorios

- dev-setup: https://github.com/Environment-As-Code/dev-setup
- dotfiles: https://github.com/Environment-As-Code/dotfiles
