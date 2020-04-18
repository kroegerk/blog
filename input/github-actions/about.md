---
css: '/blog/assets/github-actions.css'
eleventyNavigation:
  key: About
  parent: GitHub Actions
layout: layout.njk
---

GitHub Actions enable registering "jobs" to run on a cloud server
in response to GitHub commands completing.
The cloud server must have the GitHub Actions runner application is installed.
GitHub provides these servers for free,
but it is also possible to use your on servers.

For example, an workflow can build an application after every push.
This can include running linters, code formatters, and tests.
Executed workflows and their output appear in the
"Actions" tab of the GitHub repository.

A "workflow" defines a set of jobs using a YAML file.
A job defines a set up steps
to run in a given environment (ex. `ubuntu-latest');
A step is a single task runs a predefined action or a shell command.

## Configuring Workflows

Workflows for a repository are configured by YAML files
in the `.github/workflows` directory.
Here is a simple example defined in a file named `demo.yml`.
It uses an action defined at
<https://github.com/actions/hello-world-javascript-action>.

```yaml
name: My Demo
on: [push]
jobs:
  build: # a job id
    name: DemoJob # a job name
    runs-on: ubuntu-latest
    steps:
      - name: Hello
        id: hello
        uses: actions/hello-world-javascript-action@master
        with:
          who-to-greet: 'Mark Volkmann'
      - name: Time
        run: echo 'The time was ${{ steps.hello.outputs.time }}.'
```

This executes on every push to the repository.

For workflows that will run on a GitHub-hosted server (a.k.a. runner),
the operating system of the server can be specified.
This can be the latest version of a particular OS or a specific version.
Current options include:

- `ubuntu-latest`
- `windows-latest`
- `macos-latest`.
- `ubuntu-18.04`
- `ubuntu-16.04`
- `windows-2019`
- `macos-10.15`.

Workflows can also be self-hosted.
An example of specifying this is:

```yaml
runs-on: [self-hosted, linux]
```

In the example above, `build` is a job id.
TODO: Where are job ids displayed in the web UI?
This workflow only defines one job.
Defining multiple jobs is useful to allow some steps
to run on a server that uses a different operating system.

Each step (a.k.a. action) is defined by a number of properties.

| Property Name | Meaning                                                          |
| ------------- | ---------------------------------------------------------------- |
| `name`        | step name that appears in the web UI that shows workflow results |
| `uses`        | a predefined action to use                                       |
| `with`        | arguments to pass to the action                                  |
| `id`          | name that will be used to refer to action result properties      |

The property with the name specified by `id`
is an object with an `outputs` property
that is an object that holds all the output values.
Actions typically document their outputs.
In this case the only output is a `time` property
which is the time at which the action executed.

## Viewing Action Results

The "Actions" tab of a GitHub repository is shown below.

![GitHub Actions web UI #1](/blog/assets/github-actions-web-ui-1.png)

The workflows that have been executed can be filtered on
the event that triggered them (ex. "push"),
their status (ex. "success" or "failure"),
the targeted branch,
and the GitHub user name that triggered it.

Clicking a workflow row displays details about its execution.

![GitHub Actions web UI #1](/blog/assets/github-actions-web-ui-2.png)

Click a job name (ex. "DemoJob") in the left nav to see details.
This displays information about the steps
"Set up job", "Complete Job", and
each named step in the workflow, "Hello" and "Time" in this example.
Click the disclosure triangle in front of a step name
to see its detail.

Here we see the "Set up job" and "Hello" steps expanded.

![GitHub Actions web UI #1](/blog/assets/github-actions-web-ui-3.png)

The "Set up job" step shows the operating system that was used
and actions that were downloaded (ex. "hello-world-javascript-action").

Here we see the "Time" and "Complete Job" steps expanded.
In this example the "Time" step shows the
time at which the "Hello" step was executed.

![GitHub Actions web UI #2](/blog/assets/github-actions-web-ui-4.png)

## Workflow Templates

A workflow can be created from the GitHub web UI.
Click the "Actions" tab and press the "New workflow" button.
This presents a series of boxes that describe workflow templates.
Click the "Set up this workflow" button inside one of the boxes
to create a workflow based on that template.

Here is an example workflow file that does this.
For example, the "Node.js" template contains the following:

```yaml
name: Node.js CI

on:
  push:
    branches: [master]
  pull_request:
    branches: [master]

jobs:
  build:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [10.x, 12.x]

    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v1
        with:
          node-version: ${{ matrix.node-version }}
      - run: npm ci
      - run: npm run build --if-present
      - run: npm test
        env:
          CI: true
```

It offers to save this a `.github/workflows/nodejs.yml` in your repository.
You can customize the file name and the workflow definition if desired.
When ready to save it, press the "Start Commit" button in the upper-right.
A dialog will appear.
Optionally enter a commit comment and press the "Commit new file" button.
Do a "git pull" to get the new workflow file in your local repository.
The new workflow will be scheduled to run immediately.
Click the "Actions" tab to see the results.

## Executing Shell Commands

GitHub Actions do not have to use an existing action
such "hello-world-javascript-action".
They can also execute shell commands.

## Defining Actions