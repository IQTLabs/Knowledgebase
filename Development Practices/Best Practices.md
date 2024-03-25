# Source Code

1. **Dependency pinning** - Specific versions of all dependencies for proper reproducibility - Relevant tools: Poetry, NPM, Nix
2. **Lockfiles** - goes with dependency pinning to ensure that the entire web of transitive dependencies are fixed and mutually compatible - Relevant tools: Poetry, Pip-compile, NPM
3. **Unit Tests** - ensure that an atomic unit of code (function or class) functions correctly. Ideally each addition or change to the code should have a corresponding unit test to show that it is working correctly. - Relevant tools: Pytest, mocha, Jest, rhino, mock
4. **Integration Tests** - Show that units of code work together properly. Not every change will require modifications to integration tests, but it is important to maintain appropriate coverage levels and to monitor breaking changes in interfaces
5. **Code Style** - This is fancy talk for readability. Use tools to monitor this to ensure consistency within your codebase. - relevant tools: Flake8, black, prettier
6. **Linting** - linting is the process of checking the source code of a file looking for anti-patterns or artifacts that may indicate the presence of bugs - related tools: lint, eslint, pylint
7. **Doc Comments** - comments that are placed at the top of classes and methods to allow generation of documentation - related tools: Sphinx,PyDoc, Doxygen
8. **Containerization** - Where applicable it is nice to have container(s) for your code. Containers can also make a great platform for certain types of testing. Remember that you can have multiple different `Dockerfile`s and that you can specify the `Dockerfile` to use with the `-f` flag. Containers can also be used ephemerally to perform tasks and generate output. Avoid having containers that need to be managed by containers as this requires using the `--privileged` flag/exposing the docker socket which opens the way to conatiner escape techniques. Base images are your friend.

# Code Structure

**Object Oriented Programming (OOP)** - Use when writing code you intend to re-use or creating complex systems, benefits include: 
   1. **Modeling real-world entities:**  OOP is helpful when representing real-world components as objects.  An object can group data (attributes) that describe the component, along with functions (methods) that define its behavior. 
   2. **Code reusability:**  Classes act as blueprints for creating objects. You can create multiple objects (instances) from a single class, each with its own data to promote code reuse and redundancy reduction.
   3. **Maintainability and scalability:**  OOP helps organize complex code into manageable chunks.  As your application grows, you can add new functionalities by extending existing classes or creating new ones. This makes the code easier to maintain and update in the long run.
   
> Do not use OOP in cases where OOP adds burdensome complexity.  If the problem you're solving doesn't inherently benefit from objects and their relationships, it might be better to keep things simpler. Generally, for Labs projects, especially those that involve system development, we recommend using OOP. 

> When using OOP, only include 1 class per file. 


# Repo Level

I'm trying to build out a repo template that will help with creating huge chunks of this and just allow you to fill in the blanks relevant to your project, but i'm not 100% there yet.

1. **Community Standards** - All repos should include and have regularly updated:
   - README
   - License
   - Security Policy
   - Code of Conduct
   - Contributor guide
  If possible it is also desirable to have issue and PR templates to make it easier for outside contributors.
2. **Maintainers** - each repo should have at least 2 top line maintainers who are familiar with the codebase as a whole and who are willing to take on the work of reviewing/merging PRs
3. **Ignore files** - `.gitignore` and `.dockerignore` are the 2 main ones, but depending on purpose and tooling you may need others. May require a `.semgrepignore` for certain scenarios
4. **Pre-commit hooks** - setup tools that you want run locally by contributors before code is commited. You need to install pre-commit on your machine for this to work but it can be a real time saver to not have to invoke an entire CI loop to find out that unit tests fail or Flake8 has flagged a bunch of code. This is also a good place to run things like Black to clean up code.
5. **Workflows** - There will probably be some overlap with pre-commit on these since pre commit can be unreliable. The goal of these is to simplify the lives of PR reviewers so add workflows that give good heuristics about whether or not a PR is valid. 2 specific workflows will be provided before a repo is made public. One to Scan for any kinds of secrets within the repo and another to look for anti-patterns in the code. You don't need to worry about building these out. They will eventually be part of the standard template. 
6. **Codeowners** - having this in place will allow GitHub to automatically tag appropriate reviewers. do this by adding a file called `CODEOWNERS` underneath of the `.github` directory. it uses a similar syntax to the `.gitignore` file. The first entry should be `*` followed by the usernames of the repo's maintainers. Subsequent entries should call out reviewers with specialized expertise on particular types of files or specific areas of the code. Please go in increasing order of specificity as the most specific rule to match is what will be used. 