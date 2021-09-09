# Fullstack Typescript Challenge

👋 Hey! We are glad you are excited about joining [Fig](https://fig.io). This fullstack challenge aims to assess your competency with frontend/backend typescript, database schemas, a bit of logic, and  

The challenge is separated into two parts but should be submitted together:

1. **Frontend challenge**: Build a web app similar to [Explain Shell](https://explainshell.com/explain?cmd=git+push+origin+master) but using the data from [Fig's completion specs](https://github.com/withfig/autocomplete)
2. **Database schema design**: Design the schema for a database that can account for users, teams, authentication,  

Ideally, this whole challenge should take a day to finish. Let us know if takes more or less so we can recalibrate our expectations.

Finally, if you have **ANY** questions, just email brendan, matt, or sean @fig.io OR message us in our [Discord](https://fig.io/community) community. You are not annoying us. We want you to succeed. You get no points for guessing. Best to clarify early if you are unsure of something. 


# Frontend Challenge
TODO (Sean to clean up + add more info)

Your aim is to build a web app similar to [Explain Shell](https://explainshell.com/explain?cmd=git+push+origin+master), however, using the data from [Fig's completion specs](https://github.com/withfig/autocomplete) + your own style.

### The app should have
* input:
  * a way for users to input a free text string
  * a button to click to output the list of explanations (or other creative way to trigger event)
* output:
  * a list of all user input tokens
  * an explanation and categorization of each token based on data from Fig's completion specs

### Data
TODO You can get all of Fig's completion data from this skypack /endpoint: 

### Fig's completion spec standard
* You can read more about how Fig thinks about CLI tools here here: https://fig.io/docs/concepts/cli-skeleton
* TODO - talk them through walking down the tree


### Parser Assumptions
* You can safely split the input string on spaces and assume item in the array is a token
* Items that are quoted should be treated as one token e.g. `echo "hello world"` -> `[echo, "hello world"]`
* The first token will always be the name of a CLI tool
* 
* No bash parsing required e.g. you won't be expected to account for things like command substitution (`$()`), file redirectors `>`, `<`, etc 
* Quotes will not be nested e.g. `echo "Alice's nested quotes"` is invalid
* You ca



### What we are looking for
* A beautiful looking app (nice UX and UI)
* Correctly working parser
  * Correct explanation of each token 
  * Accounts for all cases in **must support** section below and optionally the additional cases


### Tools you should use
* **Frontend**: preferably next.js, but you may also use react.js
* State management: Up to you
* Hosting: Up to you. We recommend vercel or netlify


### Inputs you must support
* `git push origin master --all`  
* `ls -a -l -p`
* `echo "hello world"`
* `git commit -m "hello world"`
* `git commit --message "hello world"`
* `npm run dev`
* `npm install -g react`

**[Optional Level 1]**

* `git push origin --all` (the branch is not included as it is optional and `--all` is treated as an option)
* `git push origin --this-is-a-branch --all` (the branch starts with a `--`)

**[Optional Level 2]**

* `ls -alP` (chained options)
* `git commit -mmsg` (chained options were one takes an argument)
* `echo hello world` (variadic arguments)
* `git add index.js deploy.sh package.json` (variadic arguments)


### Final
In your submission, please also include a readme answering the following questions:
1. How long did this take you (split up by challenge)
2. What are some common edge cases your parser does not account for? Do you have any ideas how you would account for them?
3. What other ideas do you have for how to make this a more useful tool?
4. If you had more time, what else would you have done?
5. Anything else you think we should know?




### Database schema Challenge
TODO: Brendan to write up

Want to make sure you can design database schemas that can cater to a growing application

Recommend using something like https://drawsql.app/ to make it visual

Create a loom or a short video walking through your design and talking through any edge cases

* Should have an 
* Users can have multiple emails
* Users can be associated with multiple teams
* Teams can share scripts across teams






