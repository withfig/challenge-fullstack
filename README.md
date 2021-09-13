# Fullstack Typescript Challenge

👋 Hey! We are glad you are excited about joining [Fig](https://fig.io).
This challenge aims to assess your competency in both frontend
and backend tasks, which we've broken down into two challenges:

1. **Frontend challenge**: Build a web app similar to [Explain Shell](https://explainshell.com/explain?cmd=git+push+origin+master) with data from [Fig's completion specs](https://github.com/withfig/autocomplete)
2. **Database schema design**: Design the schema for a database that can
account for users, teams, and authentication.

These should be submitted as two separate zip files, with the format
specified in more detail below.

Ideally, this whole challenge should take a day to finish. Let us know if takes more or less so we can recalibrate our expectations.

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

1. **Correctness:** How well does the implementation work? What edge cases were considered?
2. **Code quality and design:** Does the app use modern paradigms for typescript and web app frameworks? Is the code easy to follow?
3. **Research and documentation:** How well are engineering decisions justified? What options were explored?



## Database Schema Challenge

In this challenge, we want you to design a relational database schema (postgres recommended) as if you were building Fig's infrastructure from scratch. There are a list of constraints we want this schema to support outlined below. 

We would like you to submit a loom or a short, concise video walkthrough through your schema design + a little more in the video. We recommend using something like https://drawsql.app/ for the schema design but you could also walk through code in a .sql file.


### Constraints
TODO (Brendan) still to complete
Unless otherwise specified, assume values like "name" are not unique i.e. we recommend using unique IDs for foreign keys

* User: represents a single, unique Fig user. Like GitHub, a Fig user will use the same account for personal and work. 
    * Each user must have: at least one associated email (that is unique across all users), a unique username
    * Each user can have: multiple associated emails, first name, last name, salted password, last login date
* Organisation: 
    * Must have: a unique name, multiple domains (each domain is unique across all organisations)
* Teams
    * Must have: at least one owner. 



Organisation can have multiple domains associated with it
Organisation can have multile teams associated with it
an individual can host widgets personal to them
an organisation can host widgets for everyone in the organisation
a team can host widgets for everyone added to that team
users can be owner/member of an org (default member)
users can be owner/member of a team (default member)





**Note**
You don't necessarily have to use the organisation, team structure proposed above. If you can come up with a more elegant solution we are open to this. The general purpose of this challenge is to see how you could build the database for a GitHub like team management system.




**Optional Level 1**
* How could we allow users to sign into Fig using Google/GitHub/GitLab/Bitbucket etc OAuth
    * No need to write the code, just create relevant tables/columns + talk through it


**Optional Level 2**
* Encryption: How could we store confidential data
    * No need to write the code, just create relevant tables/columns + talk through it


Fig can also host scripts with the same pattern as widgets

In addition, explain how the auth should work



### Deliverables
1. A video walking through your database schema. Your schema should be designed visually using a tool like https://drawsql.app/ or can be a .sql file with the code to generate the schema

3. [Optional, but bonus points] Talk through Optional Level 1 and or Level 2

### Rubric

We will evalute your submission based on:

1. **Correctness:** Does the database schema satisy the specified constraints
2. **Design:** Is the schema designed in a performant and scalable way?
3. **Summary:** Is the summary video clear and concise

