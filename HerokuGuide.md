```
 _   _                _             ____       _     _      
| | | | ___ _ __ ___ | | ___   _   / ___|_   _(_) __| | ___ 
| |_| |/ _ \ '__/ _ \| |/ / | | | | |  _| | | | |/ _` |/ _ \
|  _  |  __/ | | (_) |   <| |_| | | |_| | |_| | | (_| |  __/
|_| |_|\___|_|  \___/|_|\_\\__,_|  \____|\__,_|_|\__,_|\___|
                                                            
```

### Concept

Heroku is git + running mechanism, running is facilited through use of Workers. 
The workers are basically defined using dyno hours (currency). They are of 3-4 types. 
Web, Webworker, UrgentWorker, Worker and stuffs like that. Nothing of huge significance, 
Lets launch a tg hello world bot using heroku 

### Pre requisites

1. Git
2. Python
3. Vim (or your favourite editor)
4. Coffee (its going to short but fun)

### Start
1. Create a virtualenv (very important) `python3 -m venv helloWorld`
2. Activate the venv, `cd helloWorld;cd /bin;source activate` (if you are on fish activate the correct respective file)
3. Now lets install requirements for tg bot. `pip install botogram`
4. Create bot token using botfather, (Simple process just message @botfather on telegram)
5. Now create a python file with following code

```python
bot = botogram.create("YOUR-API-KEY")

@bot.command("hello")
def hello_command(chat, message, args):
    """Say hello to the world!"""
    chat.send("Hello world")

if __name__ == "__main__":
    bot.run()
```
6. Notice the "YOUR-API-KEY", thats where you are supposed to put api key obtained from botfather
7. Next step is simple, test it with `python helloworld.py`
8. Hope it works, if it shows something like this, consider it a success
```
INFO    - Your bot is now running!
INFO    - Press Ctrl+C to exit.
```
9. While its running ping your bot on telegram and see if it responds hello world. 
10. next step is to deal with heroku deployment, using your system package manager install heroku. 
11. `heroku login` at promp, should ask you to allow launching a browser and logging in.
12. Once logged in, you will be all set to "push" your code on heroku and deploy it
13. Now inside the project repo, `git init` this should initialize an empty repo. 
14. Do `git add . && git commit -m "first commit"` to stage it, please note we havent pushed our code yet.
15. Now the next step is to define how Heroku is supposed to cater to dependencies and how it is going to run it. 
16. For that, we are going to do this: `pip freeze > requirements,txt` this takes care of dependencies. 
17. For the Execution we are going to simply define procfile, `echo "worker: python helloworld.py" > Procfile` notice there is no 
    txt extension and also P is capital :P
18. Do `git add . && commit -m "Added requirement.txt and Procfile"` this should help you fix it.
19. Now from the same directory, do `heroku create` this will create a heroku master for you.
20. `git remote -v` should show something with heroku in its name (verification)
21. You can rename using `heroku apps:rename newname` if you feel like it.
22. Now you are ready to pus to master, `git push heroku master` this will basically push it.
23. Now goto heroku page on browser, then your app, then deploy and then deployment method.
24. From there you can connect it with github if you want to. :P
25. So as to run it, `Heroku > Heroku dashboard > Choose your app > Resources > Edit > Enable worker > Confirm`. This should start running it
26. you can now, `heroku logs` to see the logs and errors if any.

Note: you can create Runtime.txt for specific version of python. 
Note 2: Ofcourse, there is a lot mroe that can be done, just explore docs.
