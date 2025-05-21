---
hidden: true
---

# c2V4eXRlcm1pbmFsdGhlbWU

## <mark style="color:yellow;">You have found me :3</mark>

<mark style="color:green;">⠀⠀⠀⠀⠀⠀⠀⢀⠀⠔⡀⠀⢀⠞⢰⠂⠀⠀⠀⠀⠀⠀⠀</mark>\ <mark style="color:green;">⠀⠀⠀⠀⠀⠀⠀⢸⠘⢰⡃⠔⠩⠤⠦⠤⢀⡀⠀⠀⠀⠀⠀</mark>\ <mark style="color:green;">⠀⠀⠀⢀⠄⢒⠒⠺⠆⠈⠀⠀⢐⣂⠤⠄⡀⠯⠕⣒⣒⡀⠀</mark>\ <mark style="color:green;">⠀⠀⢐⡡⠔⠁⠆⠀⠀⠀⠀⠀⢀⠠⠙⢆⠀⠈⢁⠋⠥⣀⣀</mark>\ <mark style="color:green;">⠈⠉⠀⣰⠀⠀⠀⠀⡀⠀⢰⣆⢠⠠⢡⡀⢂⣗⣖⢝⡎⠉⠀</mark>\ <mark style="color:green;">⢠⡴⠛⡇⠀⠐⠀⡄⣡⢇⠸⢸⢸⡇⠂⡝⠌⢷⢫⢮⡜⡀⠀</mark>\ <mark style="color:green;">⠀⠀⢰⣜⠘⡀⢡⠰⠳⣎⢂⣟⡎⠘⣬⡕⣈⣼⠢⠹⡟⠇⠀</mark>\ <mark style="color:green;">⠀⠠⢋⢿⢳⢼⣄⣆⣦⣱⣿⣿⣿⣷⠬⣿⣿⣿⣿⠑⠵⠀⠀</mark>\ <mark style="color:green;">⠀⠀⠀⡜⢩⣯⢝⡀⠁⠀⠙⠛⠛⠃⠀⠈⠛⠛⡿⠀⠀⠀⠀</mark>\ <mark style="color:green;">⠀⠀⠀⠀⠀⣿⠢⡁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⡇⠀⠀⠀⠀</mark>\ <mark style="color:green;">⠀⠀⠀⠀⢀⣀⡇⠀⠑⠀⠀⠀⠀⠐⢄⠄⢀⡼⠃⠀⠀⠀⠀</mark>\ <mark style="color:green;">⠀⠀⠀⠀⢸⣿⣷⣤⣀⠈⠲⡤⣀⣀⠀⡰⠋⠀⠀⠀⠀⠀⠀</mark>\ <mark style="color:green;">⠀⠀⠀⠀⣼⣿⣿⣿⣿⣿⣶⣤⣙⣷⣅⡀⠀⠀⠀⠀⠀⠀⠀</mark>\ <mark style="color:green;">⠀⠀⢀⣾⣿⣿⣿⣿⣻⢿⣿⣿⣿⣿⣿⡿⠀⠀⠀⠀⠀⠀⠀</mark>\ <mark style="color:green;">⠀⡠⠟⠁⠙⠟⠛⠛⢿⣿⣾⣿⣿⣿⣿⣧⡀⠀</mark>⠀⠀

This is archive for my **Kali Theme + Setup**, as prize for mini-CTF.

This is _oneliner_ to install archive, use setup.sh script to install everything.&#x20;

> <mark style="color:orange;">**DISCLAIMER:**</mark>\ <mark style="color:orange;">If you afraid that this is virus or script will delete everything, you can just install it raw and check it yourself. But with oneliner it's easier.</mark>

```bash
wget -O kali.v17-setup.zip 'https://1512601210-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FxX3XegaS6tqwW9d8bpam%2Fuploads%2F1HOQVxQGKEhgFjXiq1qI%2Fkali.v17-setup.zip?alt=media&token=bb2f86f1-be98-4413-90ed-83f45785aa10' && unzip kali.v17-setup.zip && cd kali.v17-setup && chmod +x setup.sh && ./setup.sh
```

## <mark style="color:yellow;">SCRIPT</mark>

{% file src="../.gitbook/assets/kali.v17-setup (1).zip" %}

## <mark style="color:yellow;">IMAGES</mark>

<figure><img src="../.gitbook/assets/Screenshot_2025-05-20_23_44_11.png" alt=""><figcaption><p>Desktop</p></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot_2025-05-20_23_45_55.png" alt=""><figcaption><p>Customized Terminal</p></figcaption></figure>

## <mark style="color:yellow;">USAGE</mark>

So what this script installed is 4 things:

1. <mark style="color:green;">`cool-retro-term`</mark> is very cool terminal emulator. I use Futuristic theme (Manual setup)
2. <mark style="color:green;">`fastfetch`</mark> for kali symbol and OS Specifics output
3. <mark style="color:green;">`tmux`</mark> with all required configs for comfortable use
4. <mark style="color:green;">`sl`</mark> is for funny ASCII train

#### <mark style="color:blue;">TMUX</mark>

<mark style="color:red;">**TMUX**</mark> is tool that lets you <mark style="color:purple;">**manage multiple terminal sessions**</mark> within a single terminal window or remote SSH session. Setup script changed default shortcut from weird Ctrl+B to comfortable Ctrl+Space. All shortcuts I use (for more use this [**cheatsheet**](https://tmuxcheatsheet.com/)) is:

1. Create new Window : `Ctrl + Space C`
2. Switch Window : `Ctrl + Space 0...9`
3. Rename Window : `Ctrl + Space ,`
4. Move Window : `Ctrl + Space .`
5. List Windows : `Ctrl + Space W`
6. Create Horizontal Pane : `Ctrl + Space -`
7. Create Vertical Pane : `Ctrl + Space |`
8. Change Panes : `Ctrl + Space {Arrow Keys}`
9. Enter Command Mode: `Ctrl + Space :`

> Wallpapers are in /home/Pictures
>
> Tools are in /home/TOOLS
