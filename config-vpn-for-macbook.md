# 0. Prerequisites

1. ClashX is downloaded
2. Commercial VPN purchased
3. ClashX and the URL is well setup
4. Ensure the routing is set as "Global"

# 1. Confirm terminal command is routing through the proxy

Even in Global Mode, command-line tools like `brew` may bypass the proxy. Ensure `brew` explicitly uses ClashX's proxy by setting environment variables:

```bash
export http_proxy=http://127.0.0.1:7890
export https_proxy=http://127.0.0.1:7890
```
Replace `7890` with the HTTP proxy port configured in ClashX (check the port in ClashX settings or configuration file).

Verify the settings:

```bash
echo $http_proxy
echo $https_proxy
```
you should see http://127.0.0.1:7890 as the output for both commands.


# 2. Make these proxy setting persistent

1. Identify your Shell:
```bash
echo $SHELL
```
Depending on the output
- `/bin/zsh`: You’re using Zsh (default on macOS Catalina and later).
- `/bin/bash`: You’re using Bash.

2. Open the configuration file
- For Zsh: `~/.zshrc`
- For Bash: `~/.bash_profile` or `~/.bashrc`

Open the file using a text editor, in my case, it's sublime
```bash
subl ~/.zshc
```
Scroll to the end of the file and add the following lines:
```bash
export http_proxy=http://127.0.0.1:7890
export https_proxy=http://127.0.0.1:7890
```
Save and exit

Reload the configuration:
```bash
source ~/.zshrc
```

# 3. Verify proxy setting

To confirm the proxy settings are persistent, open a new terminal window and run:
```bash
echo $http_proxy
echo $https_proxy
```
You should see http://127.0.0.1:7890 as the output for both.