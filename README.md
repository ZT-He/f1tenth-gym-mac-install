# f1tenth-gym-mac-install
Installation guide and troubleshooting for F1TENTH Gym on macOS


🌟 F1TENTH Gym Installation Guide (macOS)

This guide provides step-by-step instructions to install the F1TENTH Gym simulation environment on macOS with Apple Silicon (M1/M2). It also includes solutions to common installation errors.

✅ Prerequisites

macOS with M1/M2 chip

Homebrew installed

Python 3.8 (managed via pyenv)

📆 Installation Steps

1. Install Homebrew

sh /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

Then add Homebrew to your shell:

echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

2. Install pyenv and Python 3.8

brew install pyenv

Add pyenv init to your shell config:

echo 'eval "$(pyenv init --path)"' >> ~/.zprofile
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
source ~/.zprofile
source ~/.zshrc

Install and set Python 3.8.18:

pyenv install 3.8.18
pyenv global 3.8.18

3. Create a Virtual Environment

mkdir -p ~/f1tenth_ws
cd ~/f1tenth_ws
python -m venv f1tenth_venv
source f1tenth_venv/bin/activate

4. Clone and Install F1TENTH Gym

git clone https://github.com/f1tenth/f1tenth_gym.git
cd f1tenth_gym
pip install -e .

5. Install System Dependencies

brew install sdl2 sdl2_image sdl2_mixer sdl2_ttf

6. Install Python Packages

pip install pygame==2.1.0
pip install matplotlib numpy scipy
gpip install gym==0.21.0

7. Run Example Simulation

python3 waypoint_follow.py

You should see a pygame window with the F1TENTH car following a track.

⚠️ Common Errors & Fixes

❌ ModuleNotFoundError: No module named 'gym_f1tenth'

✅ Fix: Use the correct import:

import f110_gym

❌ FileNotFoundError: map.png not found

✅ Fix 1: Specify the map explicitly in your script:

env = gym.make("f110_gym:f110-v0", map="levine", num_agents=1)

✅ Fix 2: Copy a default map to the current directory:

cp f110_gym/envs/maps/levine.png map.png

❌ source ../f1tenth_venv/bin/activate: No such file or directory

✅ Fix: Check the virtual environment path. If you followed this guide:

source ~/f1tenth_ws/f1tenth_venv/bin/activate

❌ cp: No such file or directory: levine.png

✅ Fix: Reclone the full repository:

rm -rf f1tenth_gym
git clone https://github.com/f1tenth/f1tenth_gym.git

🎉 Success!

Once the following command opens a pygame window with the simulation:

python3 waypoint_follow.py

You're all set! 🏎️
