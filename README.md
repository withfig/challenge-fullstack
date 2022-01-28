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
    - Assume that all arguments are mandatory. Arguments like `git push` take two 
    [optional arguments](https://fig.io/docs/reference/arg#isoptional), but unless you are doing the challenge implementation of the parser at the bottom, just  disregard the `isOptional: true` and treat these arguments as mandatory.

    See the example inputs section below for the specific cases you should support.

2. **Load up a completion spec**: Load up the completion spec specified by the first token, using
[Skypack](https://www.skypack.dev/) and [dynamic
imports](https://javascript.info/modules-dynamic-imports#the-import-expression)

Completion specs are Fig's tree-like declarative schema for describing the
    structure of a CLI tool. They are documented at great length
    [here](https://fig.io/docs/handbook/completion-spec-rules) and
    [here](https://fig.io/docs/concepts/cli-skeleton) and many examples
    can be found in our [repo of public
    specs](https://github.com/withfig/autocomplete/blob/master/src/ls.ts)

The following shows how to dynamically load up the `ls` spec from our public repo:

```javascript
const url = "https://cdn.skypack.dev/@withfig/autocomplete/build/ls.js"
const git = await import(/* webpackIgnore: true */ url);
```

3. **Annotate each token** with information from the completion spec and
**visualize** the annotations in an appealing way that could ultimately be a live Fig product.

    You can take inspiration for visualization from [Explain
    Shell](https://explainshell.com/explain?cmd=git+push+origin+master) but
    please don't copy this exactly -- this is an opportunity to show off
    your creativity. It is up to you what information from the completion spec you include
    in the annotation, but a good starting point is the `description` field.

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


__To be abundantly clear__, we expect you to correctly tokenize the input then annotate it with the correct description. This includes annotating arguments. e.g. you should provide an annotation for the `"hello world"` part of `echo "hello world"`.


## Deliverables

When you're ready to submit, please create a zip file of the below and upload it to the following form: https://airtable.com/shrFwTaQFMqvzKYLX

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

PLEASE READ THIS SECTION AND THE FOCUS AREA SECTION CAREFULLY. EMAIL IF YOU HAVE QUESTIONS

We will evalute your project based on all of the following critera. 

1. **Code quality & design**
    1. Does the app use modern paradigms for typescript and web app frameworks?
    2. Is the code easy to follow? For instance, do you have good naming conventions, comments, component structure, folder hierarchy etc.
    3. Do you have tests? Do these tests assess behaviour rather than implementation([link 1](https://testing.googleblog.com/2013/08/testing-on-toilet-test-behavior-not.html), [link2](https://teamgaslight.com/blog/testing-behavior-vs-testing-implementation)) 
2. **Product**
    1. Does you app look and feel polished?
    2. Do you handle errors gracefully?
3. **Parser**
    1. Does it take the test inputs we gave and render the correct output for each token?
    2. Does it handle incorrect inputs / edge cases?
4. **Documentation / README:**
    1. Does your readme describe and justify your thought process, code functionality, and design choices?
    2. What other options were explored, if any?

When evaluating, we will apply the most weight to the **code quality and design** and the section relevant to your chosen **focus area**. This means your code quality should be really good either way, you should still have a good readme, you should base line have a good product and parser, and then you should put more time and effort into your chosen focus (as outlined below).

## Focus Area

In order to show off your strengths, we would like you to pick a focus area in this challenge. The two focus areas are **Product** and **Parser**. When submitting, you will be asked which focus you chose so we can evaluate you accordingly.

**⭐️ Product**

If you choose **Product**, we expect you to go above and beyond with your UX and UI. You should do the minimum needed for the parser to work. Otherwise, the app should look and feel production ready. It should show your own flare.

**⭐️ Parser**

If you choose **Parser**, we expect you to go above and beyond with your parser implementation. You likely should use an AST (or some other smart representation). You should at least account for the easier edge cases below, maybe some of the hard ones, and build your parser in such a way that it could account for future edge cases.
* Easier edge cases
    * `echo hello world abc def` (variadic arguments)
    * `git add index.js deploy.sh package.json` (variadic arguments)
    * `git push origin --all` (the branch is not included as it is optional and `--all` is treated as an option)
    * `git push origin --this-is-a-branch --all` (the branch starts with a `--`)
    * `ls -alP` (chained options)
    * `git commit ---message="hello world"` (argument to long option using equals
* Harder edge cases
    * `git commit -mmsg` (short option were one takes an argument)
    * `git commit -ammsg` (chained options were one takes an argument)
    * `git add index.js deploy.sh package.json --refresh` (variadic arguments that can be stopped by an option)
    * `echo -n hello world -n` (variadic arguments that cannot be stopped by an option)
    * `ls index.js -` (use a single dash `-` to use stdin instead of a file name - read more [here](https://unix.stackexchange.com/questions/16357/usage-of-dash-in-place-of-a-filename))
    *  `grep -- -v file` (use a double dash `--` to indicate the end of options and the start of arguments - read more [here](https://unix.stackexchange.com/questions/11376/what-does-double-dash-mean))
    * `git sfsfsf` (Invalid subcommand, option, or arg)

You can see a bunch more examples here: http://docopt.org/


**Why do we have focus areas?**

Some programmers are fantastic at design. Some are fantastic at logic and traditional computer science. The best are talented at both. We would like you to play to your strengths.

## Finally
1. This challenge shouldn't take longer than a day to finish, likely less. Let us know if takes more or less so we can recalibrate our expectations.

2. If you have **ANY** questions, _please reach out_ (email brendan, matt, and sean @fig.io. You are not annoying us. We want you to succeed. You get no points for guessing. Best to clarify early if you are unsure of something. We want to make sure this
is a realistic assessment of your skills as a developer. In the real world we'd be available as your teammates if you were blocked or felt stuck!










