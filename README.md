# Fullstack Typescript Challenge

👋  Hey! We are glad you are excited about joining [Fig](https://fig.io).


## The challenge
Build a web app similar to [Explain Shell](https://explainshell.com/explain?cmd=git+push+origin+master) using data from [Fig's completion specs](https://github.com/withfig/autocomplete)

This challenge asks you to build an app very similar to Fig's [autocomplete app](https://fig.io): It takes a string input, tokenizes it, reconciles it to one of our declarative [completion specs](https://fig.io/docs/getting-started/first-completion-spec), and renders an output. In this case of the autocomplete app, the output is a list of autocomplete suggestions. In the case of this challenge, the output should be a list of tokens (subcommands, options, arguments) with descriptive information for each.

## Overview

Your web app should do the following:

1. **Parse a string**: Allow the user to input free text. Split this free text into
a sequence of tokens delimited by white space. _Note_: quoted text should be
treated as single token e.g. `echo "hello world"` has only two tokens.

    You can make the following assumptions about the user input:

    - The string will not contain nested quotes (e.g. `echo "hello \"world\""`).
    - The string will be a basic bash command where the first token is the name of a CLI tool. 
      You don't need to worry about command substitution, file redirection, pipes, boolean operators, or
      really any shell constructs besides single and double quoted strings.

    See the example inputs section below for the specific cases you should support.

2. **Load up a completion spec**: Load up the completion spec specified by the first token, using
[Skypack](https://www.skypack.dev/) and [dynamic
imports](https://javascript.info/modules-dynamic-imports#the-import-expression)

Completion specs are Fig's tree-like declarative schema for describing the
    structure of a CLI tool. They are documented at great length
    [here](https://fig.io/docs/handbook/completion-spec-rules) and
    [here](https://fig.io/docs/concepts/cli-skeleton) and many examples
    can be found in our [repo of public
    specs](https://github.com/withfig/autocomplete/blob/master/dev/ls.ts)

The following shows how to dynamically load up the `ls` spec from our public repo:

```javascript
const url = "https://cdn.skypack.dev/@withfig/autocomplete/build/ls.js"
const git = await import(/* webpackIgnore: true */ url);
```

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

    Finally, note that Fig's completion spec often don't have particularly good descriptions 
    for arguments. 


#### Languages and frameworks
The web app should be written in **Next.js or React** and must use **Typescript**. Besides that, you
may use whatever packages and libraries you'd like to achieve the final result.


#### Example inputs

Your app should handle the following inputs:
* `git push origin master --all`
* `ls -a -l -p`
* `echo "hello world"`
* `git commit -m "hello world"`
* `git commit --message "hello world"`
* `npm run dev`
* `npm install -g react`


## Deliverables

When you're ready to submit, please email brendan, matt, sean @fig.io with 
a zip file containing the following:

1. A Next.js or React app written in Typescript that implements the functionality detailed above.
2. A **README.md**. Please discuss your design decisions, how you handled
  (or decided not to handle) various edge cases, any product ideas you have
  to make this a more useful product, and what would you would do if you
  had more time.


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


## Evaluation Criteria

We will evalute your project based on the following critera. Note, we are weighting **code quality & design** and **product** most heavily:

1. ⭐️ **Code quality & design**
    1. Does the app use modern paradigms for typescript and web app frameworks?
    2. Is the code easy to follow? For instance, do you have good naming conventions, comments, component structure, folder hierarchy etc.
    3. Do you have tests? Do these tests assess behaviour rather than implementation([link 1](https://testing.googleblog.com/2013/08/testing-on-toilet-test-behavior-not.html), [link2](https://teamgaslight.com/blog/testing-behavior-vs-testing-implementation)) 
2. ⭐️ **Product**
    1. Does you app look and feel polished?
    2. Do you handle errors gracefully?
3. **Correctness of parser**
    1. Does it take the test inputs we gave and render the correct output for each token?
    2. Does it handle incorrect inputs / edge cases?
4. **Documentation:**
    1. Does your readme describe and justify your thought process, code functionality, and design choices?
    2. What other options were explored, if any?


## Finally
1. This challenge shouldn't take longer than a day to finish, likely less. Let us know if takes more or less so we can recalibrate our expectations.

2. If you have **ANY** questions, _please reach out_ (email brendan, matt, or sean @fig.io OR message us in our [Discord](https://fig.io/community) community). You are not annoying us. We want you to succeed. You get no points for guessing. Best to clarify early if you are unsure of something. We want to make sure this
is a realistic assessment of your skills as a developer. In the real world we'd be available as your teammates if you were blocked or felt stuck!


3. If you have time or want a challenge you can make sure the app handles the
following, more difficult inputs. These are strictly optional. Do not feel
stress or pressure if you don't get to handling these cases - we would much prefer you focus on product and code quality than this. However, if you're up for the challenge, here are some more examples:

* `git push origin --all` (the branch is not included as it is optional and `--all` is treated as an option)
* `git push origin --this-is-a-branch --all` (the branch starts with a `--`)
* `ls -alP` (chained options)
* `git commit -mmsg` (chained options were one takes an argument)
* `echo hello world abc def` (variadic arguments)
* `git add index.js deploy.sh package.json` (variadic arguments)









