## MacOS / PC

1. Create an empty vault folder
2. `git clone https://github.com/yewenlyu/Obsidian-Vault-Discrete-Notes.git <empty_vault_folder>`
3. Make sure *personal access token* is setup:
	a.  `git config --global credential.helper osxkeychain`
	b. Perform a Git *pull* and *push*
	```shell
	Username for 'https://github.com': yewenlyu
	Password for 'https://yewenlyu@github.com': <personal_access_token>
	```
1. Enable Git Community plugin
2. In Git plugin option, specify **Commit Author**
3. Open **command palette** and select **"Git: Create Backup"**
4. Open **command palette** and select **"Git: Open Source Control View"**

## iOS / iPadOS

1. Create an empty vault.
2. Enable Git Community Plugin.
3. In Git plugin option, under **Authentication / Commit Author**, input user name and personal *access token*, specify author name and email.
4. Open **command palette** and select **"Git: Clone existing remote repo"**
5. Fill in the **HTTPS Remote URL**