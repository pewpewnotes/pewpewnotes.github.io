### Intro 1
This one was a bit difficult, I mean its simple but I didnt had a clue on how to tackle it. I feel bad, but then thats how it is
The solution was to recognize how the prompt has been created, the prompt was created using a simple js code snippet inside the source

```
<script>
        var pass;
        pass=prompt("Password","");
        if (pass=="bc1490b82d") {
            window.location.href="?password=bc1490b82d";
        }
```
Basically All that remains is to take it and be done with it. I feel bad for messing it up



### Creds
```
Pass: bc1490b82d
```

### Tip
* Always use sources panel to observe the source code, as its easy to miss out on comments inside inspect element
* Make sure to use the New tab and current site, because its possible to disallow redirection to file from any other place in site.

