### Intro 1
This is a fun one, had me looking and the giving up. ALMOST! 
hehe, 
well just search for password in the file and you will come across a small script inside the code
```
<script type='text/javascript'>
            $(function() {
                $('.level form').submit(function(e) {
                    e.preventDefault();
                    if (document.getElementById('password').value == correct) {
                        document.location = '?pass=' + correct;
                    } else {
                        alert('Incorrect password')
                    }
                })
            })
        </script>
```
Basically checking if value is equal to correct, dumbass me went ahead and included correct for password but it was wrong
The searched for correct, and its value is the password.

### Creds
```
 <script>
            var correct = '69c394de05';
        </script>
```

### Tip
* Always use sources panel to observe the source code, as its easy to miss out on comments inside inspect element
* Make sure to use the New tab and current site, because its possible to disallow redirection to file from any other place in site.

