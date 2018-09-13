# Instruções

As instruções abaixo te ajudarão a:

- Ter um editor de texto (Sublime Text 3)
- Instalar um package manager no seu Linux
- Melhorar seu Terminal
- Setup Git e GitHub
- Instalar o Ruby


## Conta no GitHub

Se ainda não tem uma conta no GitHub, [crie ela aqui](https://github.com/join).

:point_right: **[Ajuste seu perfil aqui](https://github.com/settings/profile)** e ponha um nome e uma foto que dê para reconhecer, por favor.


## Git

Pra instalar o `git`, abra seu terminal e copie a seguinte linha de código

```bash
sudo apt-get install -y git
```

:bulb: Para **colar algo no terminal**, você precisa usar `Ctrl` + `Shift` + `V`.


## Sublime Text 3

Para baixar o sublime text:

```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
```

:point_up: Esse comando vai pedir sua senha: `[sudo] password for <username>:` (porquê está chamando `sudo`). Não se preocupe se nunca tiver feito isso antes, é normal. Você não terá um feedback visual enquanto digita sua senha (não irá aparecer nenhum `*` quando apertar uma tecla), então digite com cuidado e garanta que a senha está correta. Após digitá-la, aperte `Enter`.

Continue com a instalação do sublime:

```bash
sudo apt-get install -y apt-transport-https
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt-get update
sudo apt-get install -y sublime-text
```

Sublime Text é um de vários editores de texto. É gratuito, mas de vez em quando aparecerá um popup perguntando se quer comprar uma licença. Caso não queira, apenas aperte `Esc` e o popup sumirá.


## Oh-my-zsh

Usaremos um tipo diferente de shell: o `zsh` (o default é o `bash`).

```bash
sudo apt-get install -y zsh curl vim nodejs imagemagick jq
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
# Sua senha será pedida
```

Cuidado, sua senha será requisitada duas vezes. Ao fim da instalação seu prompt deverá parecer com isso:

![](images/ubuntu_oh_my_zsh.png)

Se não parecer, algo deu errado. **Pergunte ao Professor** (ou à internet) como resolver o problema (caso não saiba como resolver sozinho)

Perfeito! Mas agora você precisa garantir que o seu novo shell permaneça toda vez que abrir uma nova janela do terminal. Para que isso aconteça, você terá que reiniciar sua máquina:

```bash
sudo reboot
```

Até daqui a pouco.

## GitHub

Você precisará gerar uma chave (denomidada SSH key) para autenticar sua máquina tanto no GitHub quanto no outro site que usaremos mais para frente: o Heroku. Caso já tenha feito isso, pode simplesmente pular esse passo e seguir ao próximo.

Abra seu terminal e escreva isso. **CUIDADO**, você terá que substituir `SEU_EMAIL@AQUI.COM` pelo seu email (não copie e cole cegamente). O email deverá ser o mesmo que usou para se cadastrar no GitHub. Essa linha irá requisitar algumas informações. Aperte `Enter` até que **uma senha seja requisitada**.

```bash
mkdir -p ~/.ssh && ssh-keygen -t ed25519 -o -a 100 -f ~/.ssh/id_ed25519 -C "TYPE_YOUR_EMAIL@HERE.com"
```

Quando a senha for requisitada, ponha algo que você irá lembrar. É uma senha que protegerá sua SSH key **privada** guardada no seu HD. Se achar que não precisa de uma senha, apenas aperte `Enter`.

Agora você precisará dar sua SSH key **pública** ao GitHub. Para isso, cole no terminal:

```bash
cat ~/.ssh/id_ed25519.pub
```

Isso irá printar a informação contida no arquivo de caminho absoluto `~/.ssh/id_ed25519.pub`. Copie esse texto, vá em [github.com/settings/ssh](https://github.com/settings/ssh), clique em **Add SSH key**, ponha como título o nome do seu computador e cole a informação abaixo. Salve a chave clicando em **Add key**.

Para verificar se o processo foi bem sucedido, rode isso. O terminal irá printar um aviso. Digite `yes` e aperte `Enter`.

```bash
ssh -T git@github.com
```

Se algo como isso aparecer, tudo ocorreu como esperado :)

```bash
# Hi --------! You've successfully authenticated, but GitHub does not provide shell access
```

Caso não funcione, tente rodar isso antes de tentar de novo o comando `ssh -T`:

```bash
ssh-add ~/.ssh/id_ed25519
```

Caso tenha interesse em entender melhor o que aconteceu, [leia esse artigo](http://sebastien.saunier.me/blog/2015/05/10/github-public-key-authentication.html) (em inglês).


## Dotfiles (Standard configuration)


:arrow_right: [Clique aqui para **fork**](https://github.com/lewagon/dotfiles/fork) the `lewagon/dotfiles` repository to your account. Forking means that it will create a new repo in your GitHub account, identical to the original one. You'll have a new repository on your GitHub account, `your_github_username/dotfiles`. We need to fork because each of you will need to put specific information (e.g. your name) in those files.

Open your terminal. **Don't blindly copy paste this line**, replace `replace_this_with_your_github_username` with *your*
own github usernickname.

```bash
export GITHUB_USERNAME=replace_this_with_your_github_username

# Example:
#   export GITHUB_USERNAME=ssaunier
```

Now copy/paste this very long line in your terminal. Do **not** change this one.

```bash
mkdir -p ~/code/$GITHUB_USERNAME && cd $_ && git clone git@github.com:$GITHUB_USERNAME/dotfiles.git
```

Run the `dotfiles` installer.

```bash
cd ~/code/$GITHUB_USERNAME/dotfiles
zsh install.sh
```

Then run the git installer:

```bash
cd ~/code/$GITHUB_USERNAME/dotfiles
zsh git_setup.sh
```

:point_up: This will **prompt** you for your name (`Firstname Lastname`) and your email.

Be careful, you **need** to put the **same** email as the one you sign up with on GitHub.

Please now **quit** all your opened terminal windows.

### Sublime Text auto-configuration

Open a new terminal and type this:

```bash
stt
```

It will **open Sublime Text in the context of your current folder**. That's how we'll use it.

**Close Sublime text** and open it again:

```bash
stt
```

**Wait 1 minute** for additional packages to be automatically installed (New tabs with text will automatically open, containing documentation for each new package installed). TO follow package installation, you can go to `View > Show console`.

To check if plugins are installed, open the Command Palette (`⌘` + `⇧` + `P` on OSX, `Ctrl` + `⇧` + `P` on Linux), type in `Packlist` and then `Enter`, you should see a couple of packages installed (like [Emmet](http://emmet.io/)).

If you don't, please install all of them manually. The list is referenced [here](https://github.com/lewagon/dotfiles/blob/master/Package%20Control.sublime-settings).

When it's done, you can close Sublime Text.


## Installing Ruby (with [rbenv](https://github.com/sstephenson/rbenv))

First we need to clean up any previous Ruby installation you might have:

```bash
rvm implode && sudo rm -rf ~/.rvm
# If you got "zsh: command not found: rvm", carry on. It means `rvm` is not
# on your computer, that's what we want!

rm -rf ~/.rbenv
```

Then in the terminal, run:

```bash
sudo apt-get install -y build-essential tklib zlib1g-dev libssl-dev libffi-dev libxml2 libxml2-dev libxslt1-dev libreadline-dev
sudo apt-get clean
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
```

**Close your terminal and open it again** (Alt+F4 and restart it). If you get a warning, just **ignore** it from now (Ruby is not installed yet).


Now, you are ready to install the latest ruby version, and set it as the default version.

Run this command, it will **take a while (5-10 minutes)**

```bash
rbenv install 2.4.4
```

Once the ruby installation is done, run this command to tell the system
to use the 2.4.4 version by default.

```bash
rbenv global 2.4.4
```

Then **restart** your Terminal again (close it and reopen it).

```bash
ruby -v
```

You should see something starting with `ruby 2.4.4p`. If not, ask a teacher.

## Installing some gems

---

:warning: If you are in **China** :cn:, you should update the way we'll install gem with the following commands. If you are not in China, well just skip this and go directly to the next `gem install` command!

```bash
# China only!
gem sources --remove https://rubygems.org/
gem sources -a https://ruby.taobao.org/
gem sources -l
# *** CURRENT SOURCES ***

# https://ruby.taobao.org
# Ensure it only has ruby.taobao.org
```

---

All, please run the following line:

```bash
gem install rake bundler rspec rubocop pry pry-byebug hub colored octokit
```

**Never** install a gem with `sudo gem install`! Even if you stumble upon a Stackoverflow answer
(or the Terminal) telling you to do so.


## Postgresql

In a few weeks, we'll talk about SQL and Databases and you'll need something called Postgresql,
an open-source robust and production-ready database. Let's install it now.

```
sudo apt-get install -y postgresql postgresql-contrib libpq-dev build-essential
echo `whoami` > /tmp/caller
sudo su - postgres
psql --command "CREATE ROLE `cat /tmp/caller` LOGIN createdb;"
exit
rm -f /tmp/caller
```


## Check-up

Let's check if you successfully installed everything.

Quit all opened Terminal, open a new one and run the following commands:

```bash
curl -Ls https://raw.githubusercontent.com/lewagon/setup/master/check.rb > _.rb && ruby _.rb || rm _.rb
```

It should tell you if your workstation is ready :) If not, ask a teacher.


## Alumni

Register as a Wagon alumni by going to [kitt.lewagon.com/onboarding](http://kitt.lewagon.com/onboarding). Select your batch, sign in with GitHub and enter all your information.

Your teacher will then validate that you are indeed part of the batch. You can ask him to do it as soon as you completed the registration form.

Once the teacher has approved your profile, go to your email inbox. You should have 2 emails:

- One from Slack, inviting you to the Le Wagon Alumni slack community (where you'll chat with your buddies and all the previous alumni). Click on **Join** and fill the information.
- One from GitHub, inviting you to `lewagon` team. **Accept it** otherwise you won't be able to access the lecture slides.


## Slack

[Install Slack for Linux (beta)](https://get.slack.help/hc/en-us/articles/212924728-Slack-for-Linux-beta-).

Launch the app and sign in to `lewagon-alumni` organization.

Make sure you upload a picture there.

You can also sign in to Slack on your iPhone or Android device!

The idea is that you'll have Slack open all day, so that you can share useful links / ask for help / decide where to go to lunch / etc.

Enjoy your ride with Le Wagon :)


