# Cambio de hora en servidores Linux


ver hora:
timedatectl status
date
hwclock

set hora:
hwclock --set --date="`date '+%D %H:%M:%S'`"
