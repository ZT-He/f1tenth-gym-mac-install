# f1tenth-gym-mac-install
Installation guide and troubleshooting for F1TENTH Gym on macOS


🌟 F1TENTH Gym Installation Guide (macOS)

This guide provides step-by-step instructions to install the F1TENTH Gym simulation environment on macOS based on the instruction from: https://github.com/f1tenth/f1tenth_gym. It also includes solutions to some common installation errors.

You can also use Docker for the installation. However, please keep in mind that an **_Nvidia GPU_** is required for the Docker setup.


✅ Prerequisites

Homebrew installed

Python 3.8 (managed via pyenv)

---

📆 Installation Steps

1. Install Homebrew
```ruby
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Then add Homebrew to your shell:

```ruby
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```
---
2. Install pyenv and Python 3.8

```ruby
brew install pyenv
```

Add pyenv init to your shell config:
```ruby
echo 'eval "$(pyenv init --path)"' >> ~/.zprofile
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
source ~/.zprofile
source ~/.zshrc
```
Install and set Python 3.8.18:
```ruby
pyenv install 3.8.18
pyenv global 3.8.18
```
---
3. Create a Virtual Environment
```ruby
mkdir -p ~/f1tenth_ws
cd ~/f1tenth_ws
python -m venv f1tenth_venv
source f1tenth_venv/bin/activate
```
---
4. Clone and Install F1TENTH Gym
```ruby
git clone https://github.com/f1tenth/f1tenth_gym.git
cd f1tenth_gym
pip install -e .
```
---
5. Install System Dependencies
```ruby
brew install sdl2 sdl2_image sdl2_mixer sdl2_ttf
```
---
6. Install Python Packages
```ruby
pip install pygame==2.1.0
pip install matplotlib numpy scipy
pip install gym==0.19.0
```
---
7. Run Example Simulation
```ruby
python3 waypoint_follow.py
```
You should see a pygame window with the F1TENTH car following a track like below:

<img width="995" alt="waypoint-follow-screenshot" src="https://github.com/user-attachments/assets/476c7ac8-3428-4366-8881-5bbdccf0c1b9" />  

You're all set! 🏎️

---

⚠️ Some Errors & Fixes

❌ ModuleNotFoundError: No module named 'gym_f1tenth'

✅ Fix: Use the correct import:

```ruby
import f110_gym
```

---
❌ % echo 'eval "$(pyenv init -)"' >> ~/.zshrc
zsh: permission denied: /Users/xxx/.zshrc

✅ Fix: Try this command with ```sudo```:

```ruby
sudo sh -c 'echo "eval \"\$(pyenv init -)\"" >> ~/.zshrc'
```
You’ll be prompted for your password

---
❌ source ../f1tenth_venv/bin/activate: No such file or directory

✅ Fix: Check the virtual environment path. If you followed this guide:

```ruby
source ~/f1tenth_ws/f1tenth_venv/bin/activate
```

---
❌ cp: No such file or directory: levine.png

✅ Fix: Reclone the full repository:

```ruby
rm -rf f1tenth_gym
git clone https://github.com/f1tenth/f1tenth_gym.git
```
