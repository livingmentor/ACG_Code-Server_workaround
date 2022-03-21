# ACG_Code-Server_workaround


```
curl -fsSL https://code-server.dev/install.sh | sh

sudo systemctl enable --now code-server@$USER

openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ~/.config/code-server/key.pem -out ~/.config/code-server/cert.pem
#follow the prompts here

rm ~/.config/code-server/config.yaml
echo 'bind-addr: 0.0.0.0:8080' >> ~/.config/code-server/config.yaml
echo 'auth: password' >> ~/.config/code-server/config.yaml
echo 'disable-telemetry: true' >> ~/.config/code-server/config.yaml
echo 'disable-update-check: true' >> ~/.config/code-server/config.yaml
echo 'cert: /home/cloud_user/.config/code-server/cert.pem' >> ~/.config/code-server/config.yaml
echo 'cert-key: /home/cloud_user/.config/code-server/key.pem' >> ~/.config/code-server/config.yaml
echo 'extensions-dir: /home/cloud_user/.local/share/code-server-extensions' >> ~/.config/code-server/config.yaml
echo 'user-data-dir: /home/cloud_user/.local/share/code-server-user-data' >> ~/.config/code-server/config.yaml
echo 'password: CHANGE_THIS_PASSWORD' >> ~/.config/code-server/config.yaml

sudo systemctl restart code-server@$USER


sudo yum install -y --skip-broken git gcc zlib-devel readline-devel sqlite-devel bzip2-devel

git clone https://github.com/pyenv/pyenv.git ~/.pyenv

sed -Ei -e '/^([^#]|$)/ {a \
export PYENV_ROOT="$HOME/.pyenv"
a \
export PATH="$PYENV_ROOT/bin:$PATH"
a \
' -e ':a' -e '$!{n;ba};}' ~/.bash_profile
echo 'eval "$(pyenv init --path)"' >> ~/.bash_profile
echo 'eval "$(pyenv init -)"' >> ~/.bashrc

#I restarted my putty terminal for the environment variables and pyenv init to take effect.  There may be a better way to do this.
pyenv install 3.7.6


pyenv shell 3.7.6
pip3.7 install --upgrade pip
```
