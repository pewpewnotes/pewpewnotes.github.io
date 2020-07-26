1. For fixing the terminfo of Termite 

Do infocmp on host machine, 
infocmp > termite.terminfo 
then tic -x termite.terminfo on alpine machine, you can use nc to transfer that. 
if tic is not found, install ncurses. 

2. Fixing X11 forwarding

install xauth my mate, thats usually missing. 


