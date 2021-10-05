About the Project:

One of the initial challenges of this project was getting it all set and installing the appropriate plugins and packages. Because I typically work with larger projects that already have a lot of the set up accomplished by the time I get in there, it was a bit of a learning curve to set it up myself. I found some good documentation and was able to use Vue CLI to set it up pretty easily - though I did run into a couple of small packaging issues, mostly with package versions not playing nice with each other. I also read a helpful article later on to help me deploy this as a Github page (I had done so for other projects, but not a Vue project, so that was a new process as well). Overall, the setup process/deployment process probably took an hour and a half or so. 

Once set up was figured out, things started to move more quickly. Setting up my initial components was straightforward. The main objective of returning a specific contact from the contacts.json was also pretty straightforward - data mapping is a large part of the projects I work on regularly.

One of the tasks that took a bit longer was figuring out the best user experience when it came to the timing of showing the 'email not found' and invalid email errors, disabling the button, etc. I tried a few different ways before settling on what felt natural in my opinion. Here's a summary of what I ended up with: 

- I triggered an invalid email message @input (when the user interacts with the input), but I also set a timeout of 1 second so it would not constantly be triggering. The effect (or at least the hope of the effect) is that it waits until the user is done typing, or at least paused, before triggering the error message. I also decided to only show this if they had anything in the input - I felt that if the input was empty but they were 'clicked in', they could be thinking about what they wanted to type or just paused, and it felt jarring to display the message in that instance. 
- I also added the invalid email trigger @blur, so it would fire once they exit the input field. This includes both invalid entries and empty entries, so should catch everything before trying to submit.
- I disabled the button until there was a valid entry, so they couldn't try to submit before that.
- I also decided to clear the 'email not found' message @keydown, or when they started interacting with the input field again. This way the user could start with a 'fresh slate', and the message would linger. 

Overall, the above took probably an hour or two of just messing with different possibilities before landing on one that felt right. 

Finally, the last bit that took a little time was the styling. Since I am already familiar with Bootstrap, I decided to use Tailwind for this exercise so I could learn more about it. My approach was just to use their documentation to search whatever CSS I would want to use, and see if there was a class for that. In this instance it was slower and more tedious than if I would have just done my own CSS (it's hard to say exactly how long as I kind of added the styles in as I went, rather than one big style session), but of course I imagine the more I may use Tailwind, the faster that would become. I was impressed with their thorough documentation and how I was able to rely on their classes for the majority of the styling for this project. 

Thank you for your time!

Set Up Notes::

# bisnow-project

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
