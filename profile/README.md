# ⚡ INICIO RÁPIDO

## 1️⃣ PRE-FORMATEO

```bash
# Edita SOLO estos 2 archivos en dotfiles:
vi dotfiles/git/.gitconfig
# Cambiar: name, email

# Listo. Eso es todo.
```

## 2️⃣ POST-FORMATEO

```bash
# En WSL recién formateado:
sudo apt update && sudo apt install -y git
git clone https://github.com/USERNAME/dev-setup.git ~/.dev-setup
cd ~/.dev-setup
./bootstrap.sh
```

## 3️⃣ DESPUÉS

```bash
# Autenticar GitHub
gh auth login
# → SSH → Autoriza en navegador
```

**¡Listo.** Todo instalado y configurado automáticamente.

---

## ❓ ¿Si algo falla?

```bash
cd ~/.dev-setup
ansible-playbook linux.yml --ask-become-pass
```

Solo vuelve a ejecutar. Ansible es idiopotente (no rompe nada).

---

## 📝 Edita esto pre-formateo:

**`dotfiles/git/.gitconfig`** — Tu nombre y email:
```
[user]
    name = Tu Nombre
    email = tu-email@ejemplo.com
```

**Listo. Eso es literalmente todo lo que necesitas cambiar.**
