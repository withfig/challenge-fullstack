# Fullstack Typescript Challenge

👋 Hey! We are glad you are excited about joining [Fig](https://fig.io).
This challenge aims to assess your competency in both frontend
and backend tasks, which we've broken down into two challenges:

1. **Frontend challenge**: Build a web app similar to [Explain Shell](https://explainshell.com/explain?cmd=git+push+origin+master) with data from [Fig's completion specs](https://github.com/withfig/autocomplete)
2. **Database schema design**: Design the schema for a database that can
account for users, teams, and authentication.

These should be submitted as two separate zip files to brendan, matt, and sean @fig.io. More information below

This challenge shouldn't take longer than a day to finish, likely less. Let us know if takes more or less so we can recalibrate our expectations.

Finally, if you have **ANY** questions, just email brendan, matt, or sean @fig.io OR message us in our [Discord](https://fig.io/community) community. You are not annoying us. We want you to succeed. You get no points for guessing. Best to clarify early if you are unsure of something. 

## Frontend Challenge

To provide suggestions to users, Fig has to reconcile a string the user
has typed with one of our declarative [completion specs](https://fig.io/docs/getting-started/first-completion-spec).

Fig's completion specs are very powerful though, and with just
a completion spec and a string, we can do more than just offer suggestions
to the user.

Your task is to build a web app that breaks down a string into tokens and
uses a Fig completion spec to annotate these tokens with descriptive information.

### Overview

Your web app should do the following:

1. **Parse a string**, input by the user through a free text input, into
a sequence of tokens delimited by white space. Quoted text should be
treated as single token e.g. `echo "hello world"` has only two tokens.

    You can make the following assumptions about the user input:

    - The string will not contain nested quotes (e.g. `echo "hello \"world\""`).
    - The string will be a basic bash command, you don't need to worry about
      command substitution, file redirection, pipes, boolean operators, or
      really any shell constructs besides single and double quoted strings.

    See the example inputs section below for specific cases you should support.

2. **Load up a completion spec** specified by the first token, using
[Skypack](https://www.skypack.dev/) and [dynamic
imports](https://javascript.info/modules-dynamic-imports#the-import-expression)
(e.g.
`import("https://cdn.skypack.dev/@withfig/autocomplete/specs/ls.js")` to
load the `ls` spec from our public repo)

    Completion spec's are Fig's declarative schema for describing the
    structure of a CLI tool. They are documented at great length
    [here](https://fig.io/docs/handbook/completion-spec-rules) and
    [here](https://fig.io/docs/concepts/cli-skeleton) and many examples
    can be found in our [repo of public
    specs](https://github.com/withfig/autocomplete/blob/master/dev/ls.ts)

3. **Annotate each token** with information from the completion spec and
**visualize** the annotations in an appealing way.

    You can take inspiration for visualization from [Explain
    Shell](https://explainshell.com/explain?cmd=git+push+origin+master) but
    please don't copy this exactly -- this is an opportunity to show off
    your creativity. It is up to you what information from the completion spec you include
    in the annotation, but a good starting point is the `description` field.

    For simplicity you can assume any options or subcommands used in the
    string will only contain _mandatory_ arguments: don't worry about handling 
    [optional arguments](https://fig.io/docs/reference/arg#isoptional)

#### Example inputs

Your app should handle the following inputs:
* `git push origin master --all`
* `ls -a -l -p`
* `echo "hello world"`
* `git commit -m "hello world"`
* `git commit --message "hello world"`
* `npm run dev`
* `npm install -g react`

If you have time or want a challenge you can make sure the app handles the
following, more difficult inputs. These are strictly optional, don't feel
stress or pressure if you don't get to handling these cases:

**Optional Level 1**

* `git push origin --all` (the branch is not included as it is optional and `--all` is treated as an option)
* `git push origin --this-is-a-branch --all` (the branch starts with a `--`)

**Optional Level 2**

* `ls -alP` (chained options)
* `git commit -mmsg` (chained options were one takes an argument)
* `echo hello world` (variadic arguments)
* `git add index.js deploy.sh package.json` (variadic arguments)

### Deliverables

The final deliverable for this part of the challenge should be a zip file
containing the following:

1. A Next.js or React app that implements the functionality detailed above.
2. A **README.md**. Please discuss your design decisions, how you handled
  (or decided not to handle) various edge cases, any product ideas you have
  to make this a more useful product, and what would you would do if you
  had more time.

The web app should be written in Typescript, besides that, you may use
whatever packages and libraries you'd like to achieve the final result.

We will run your project locally as follows:

```bash
unzip your_submission.zip
cd your_submission
npm ci
npm run start
```

So you should include a `package.json` and `package-lock.json` but do not
need to include `node_modules/` in the zip file. Please make sure your
submission will run if we follow these steps.

If you are stuck on something, _please reach out_! We want to ensure this
is a realistic assessment of your skills as a developer and in the real
world we'd be available as your teammates if you were blocked or felt stuck.

### Rubric

We will evalute your project based on:

1. **Correctness:** How well does the implementation work? What edge cases were considered? Were there any bugs? 
2. **Code quality and design:** Does the app use modern paradigms for typescript and web app frameworks? Is the code easy to follow?
3. **Research and documentation:** How well are engineering decisions justified? What options were explored?
4. **Product & UI**: Does this feel like a great product? Does it have unique and beautiful UX/UI? Is it simple and clear how to perform actions? If there are errors, are they handled gracefully?


### Database schema Challenge
TODO: Brendan to write up

Want to make sure you can design database schemas that can cater to a growing application

Recommend using something like https://drawsql.app/ to make it visual

Create a loom or a short video walking through your design and talking through any edge cases

* Should have an 
* Users can have multiple emails
* Users can be associated with multiple teams
* Teams can share scripts across teams
