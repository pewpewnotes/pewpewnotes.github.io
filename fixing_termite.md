In termite most of the time xterm-termite is not recognised over ssh

thats why 

`curl -sSL https://raw.githubusercontent.com/thestinger/termite/master/termite.terminfo | tic -x -`
to fix the issue, its because terminfo has the info but doesnt maps it correctly. 
