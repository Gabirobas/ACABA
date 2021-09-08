eval `ssh-agent -s`

ssh-add C:/Users/PC/.ssh/id_Gabi

ssh-add -L  ((esse eh so pra conferir))


No VS COde
start-ssh-agent

Powershell
export USER_AT_HOST="your-user-name-on-host@hostname"
export PUBKEYPATH="$C:/Users/PC/.ssh/id_Gabi.pub"

ssh $USER_AT_HOST "powershell New-Item -Force -ItemType Directory -Path \"\$HOME\\.ssh\"; Add-Content -Force -Path \"\$HOME\\.ssh\\authorized_keys\" -Value '$(tr -d '\n\r' < "$PUBKEYPATH")'"



$pubKey=(Get-Content "$PUBKEYPATH" | Out-String); ssh "$USER_AT_HOST" "mkdir -p C:/Users/PC/.ssh && chmod 700 C:/Users/PC/.ssh && echo '${pubKey}' >> C:/Users/PC/.ssh/authorized_keys && chmod 600 C:/Users/PC/.ssh/authorized_keys"