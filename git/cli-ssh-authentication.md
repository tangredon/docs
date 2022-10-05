# Git CLI SSH Authentication
[TortoiseGit](https://tortoisegit.org/) requires a specific ssh private key format and credential manager in order to work. This is not compatible with the Git CLI commands in a repository that requires SSH authentication. In order to allow both TortoiseGit and Git CLI to work correctly, some steps are required.

## Steps
1. Open the **private key** used by **TortoiseGit** in [PuTTYgen](https://www.puttygen.com/)
2. Export the key in **openssh** format (Conversions > Export OpenSSH Key)
3. Use `ssh-add <openssh file>` to add the file to the OpenSSH Agent
    1. If `ssh-agent` service is not loaded, it needs to be enabled first from **Windows Services**
4. *Optional* move to **openssh key file** to `%%UserProfile%%\.ssh\id_rsa` to ensure seamless loading when using git commands
    1. You can debug if the key loading works correctly using `ssh -vT git@github.com` command. It will print out all the steps and keys used while trying to connect to GitHub.


## OpenSSH Key Permissions
`ssh-add` command will require very restrictive permissions on the private key. The following snippet show how to take ownership of said file and remove all other permissions.

Private key file: `%%USERPROFILE%%\.ssh\id_rsa`

**Powershell**
```powershell
# Set Key File Variable:
    New-Variable -Name Key -Value "$env:UserProfile\.ssh\id_rsa"

# Remove Inheritance:
    Icacls $Key /c /t /Inheritance:d

# Set Ownership to Owner:
    # Key's within $env:UserProfile:
        Icacls $Key /c /t /Grant ${env:UserName}:F

    # Key's outside of $env:UserProfile:
        TakeOwn /F $Key
        Icacls $Key /c /t /Grant:r ${env:UserName}:F

# Remove All Users, except for Owner:
    Icacls $Key /c /t /Remove:g Administrator "Authenticated Users" BUILTIN\Administrators BUILTIN Everyone System Users

# Verify:
    Icacls $Key
    # If this prints out multiple users besides the Owner, re-run the command above to remove them as well

# Remove Variable:
    Remove-Variable -Name Key
```

**CMD**
```shell
# Set Key File Variable:
    Set Key="%UserProfile%\.ssh\id_rsa"

# Remove Inheritance:
    Icacls %Key% /c /t /Inheritance:d

# Set Ownership to Owner:
    # Key's within %UserProfile%:
         Icacls %Key% /c /t /Grant %UserName%:F

    # Key's outside of %UserProfile%:
         TakeOwn /F %Key%
         Icacls %Key% /c /t /Grant:r %UserName%:F

# Remove All Users, except for Owner:
    Icacls %Key% /c /t /Remove:g "Authenticated Users" BUILTIN\Administrators BUILTIN Everyone System Users

# Verify:
    Icacls %Key%
    # If this prints out multiple users besides the Owner, re-run the command above to remove them as well

# Remove Variable:
    set "Key="

```

