# Emacs Notes
-- Ctrl-v -> forward one screen
-- Meta-v -> Backward one screen
ctrl-p / ctrl-n -> one line up and down

			  Previous line, C-p
				  :
				  :
   Backward, C-b .... Current cursor position .... Forward, C-f
				  :
				  :
			    Next line, C-n
	C-f	Move forward a character
	C-b	Move backward a character

	M-f	Move forward a word
	M-b	Move backward a word

	C-n	Move to next line
	C-p	Move to previous line

	C-a	Move to beginning of line
	C-e	Move to end of line

	M-a	Move back to beginning of sentence
	M-e	Move forward to end of sentence

You can use C-g to stop a command which is taking too long to execute

C-x 1	One window (i.e., kill all other windows).

	<DEL>        Delete the character just before the cursor
	C-d   	     Delete the next character after the cursor

	M-<DEL>      Kill the word immediately before the cursor
	M-d	     Kill the next word after the cursor

	C-k	     Kill from the cursor position to end of line
	M-k	     Kill to the end of the current sentence

The difference between "killing" and "deleting" is that "killed" text
can be reinserted (at any position), whereas "deleted" things cannot
be reinserted in this way.
C-w -> To cut the marked text
C-y -> to paste the cut text
M-y -> Something to do with previous content before cut

C-/    undo
c-_    redo

C-u    repeat an action


C-x C-f		Find file
C-x C-s		Save file
C-x s		Save some buffers
C-x C-b		List buffers
C-x b		Switch buffer
C-x C-c		Quit Emacs
C-x 1		Delete all but one window
C-x u		Undo
