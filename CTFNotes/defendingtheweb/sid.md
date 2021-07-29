### Sid / Intro
This one was a simple one, just had to modify the `cookie i3_access = false` to true and done.
My approach was basically using a sniffer, but it seems that better solution was to use jsconsole 
`document.cookie` `console.log(document.cookie)` and `document.cookie = 'i3_access = true'`
