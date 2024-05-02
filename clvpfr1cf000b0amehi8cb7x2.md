---
title: "I wrote a script that starts the workday for me"
datePublished: Thu May 02 2024 16:03:28 GMT+0000 (Coordinated Universal Time)
cuid: clvpfr1cf000b0amehi8cb7x2
slug: i-wrote-a-script-that-starts-the-workday-for-me
tags: programming-blogs, development, bash-script

---

Every morning when I power up my work laptop, I have to open the same applications, go to the same websites, run the same commands in my terminal... It has started to feel a bit tedious, so I decided to write a bash script to do all of that for me automatically when I log in. 😄 Below are the steps I took. First, I should say that I am using Ubuntu 22.04, so if you want to try this and you are using a different OS, things might work differently for you. And second, I am completely new to writing bash scripts so this has been a great learning experience. But there might also be a more efficient way to do this, so if you have any tips, do let me know!

### **Creating the script**

First, I created a file and named it `start_work.sh`.

The first line of the file is a shebang `#!` followed by the bash shell path. In my case, this was `/usr/bin/bash`, but you can find yours by running the command `which bash` in your terminal.

```bash
#!/usr/bin/bash
```

Next, because I am using `zsh`, I needed to source my `.zshrc` because I was having issues running `npm run dev` due to `PATH` issues. You may or may not need this depending on what shell you are using and how it's configured.

```bash
source ~/.zshrc
```

Next, I wanted to open VSCode and start my development server with `npm run dev` in one terminal, and start up an ngrok domain with `ngrok http http://localhost:8080` in another terminal. Before adding this step to my script, I had to set up a couple of things:

1. In my project, I had to create a file in my `.vscode` folder called `tasks.json`. In this json file, I had to create tasks for running the two commands I need. The first task runs `npm run dev` in a new terminal, and the second task runs `ngrok http http://localhost:8080` in another new terminal. The final task, `start`, runs the previous two tasks consecutively. This is the one I will be using moving forward.
    
    ```json
    {
      "version": "2.0.0",
      "tasks": [
        {
          "label": "dev",
          "type": "shell",
          "command": "npm run dev",
          "presentation": {
            "reveal": "always",
            "panel": "new"
          },
          "problemMatcher": []
        },
        {
          "label": "ngrok",
          "type": "shell",
          "command": "ngrok http http://localhost:8080",
          "presentation": {
            "reveal": "always",
            "panel": "new"
          },
          "problemMatcher": []
        },
        {
          "label": "start",
          "dependsOn": ["dev", "ngrok"],
          "problemMatcher": []
        }
      ]
    }
    ```
    

2. Next, I added a keyboard shortcut for running the `start` task. For this, I went into `keybindings.json` within VSCode (<kbd>Ctrl</kbd> / <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>, type `keyboard`, and open `Preferences: Open Keyboard Shortcuts (JSON)`) and added:
    
    ```json
    {
      "key": "ctrl+shift+t",
      "command": "workbench.action.tasks.runTask",
      "args": "start"
    }
    ```
    

3. I installed [xdotool](https://github.com/jordansissel/xdotool) so that I could input the keyboard shortcut within my script.
    

Once all of that was ready, I was able to add the next part to my script. This opens my project in VSCode, waits for 3 seconds just to make sure everything is loaded up, then inputs the keyboard shortcut for my `start` task using xdotool, which will run the aforementioned `npm` and `ngrok` commands.

```bash
code ./my-project
sleep 3
xdotool key ctrl+shift+t 
```

The rest of the script is rather straightforward. Next I need to open Docker Desktop, which starts up all the containers I need for development.

```bash
systemctl --user start docker-desktop
```

Next I need to open a couple of links, in this case Gmail and Notion.

```bash
open https://mail.google.com/
open https://www.notion.so/
```

And last but not least, I need to open Slack, which is very straightforward. 🙂

```bash
slack
```

And that's it! Here is the final completed script:

```bash
#!/usr/bin/bash
​
# Source .zshrc file for correct PATH setup
source ~/.zshrc
​
# Open VSCode and run "start" task
code ./my-project
sleep 3
xdotool key ctrl+shift+t 
​
# Open Docker Desktop
systemctl --user start docker-desktop
​
# Open Gmail and Notion in Chrome
open https://mail.google.com/
open https://www.notion.so/
​
# Open Slack
slack
```

The final thing I had to do was make it so that this script gets executed on startup. For this, I went to my Startup Applications Preferences (<kbd>Alt</kbd> + <kbd>F2</kbd> and type `gnome-session-properties`), clicked `Add`, entered the command to be executed (`bash /path/to/script/start_work.sh`), saved and closed.

And there we go! Now when I login, this script will essentially start the workday for me, thus saving me some clicks and keystrokes. Of course, if you want to try this, you can change the script to open any application and/or website you want, and run whatever terminal commands you need in VSCode. This was just my personal use case. 😄

I hope this was an interesting read and hopefully you learned something new. Thank you and see you next time!