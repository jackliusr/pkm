- Autolink references
- pricing comparison: github vs azure devops
- data framework:
- template repository: make an existing repository a template, so you and others can generate new repositories with the same directory structure, branches, and files.
- actions
	- workflow concepts: events, workflow, jobs, steps, **actions**, runner,  artifacts, secret, environment, matrix build, caching, workflow dispatch, scheduled workflow, contexts, filter patterns, concurrency
	- action concepts: workflow commands, type,
	- action vs app
	- Best Practices
	- starter workflow
	- [Reusing workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows#overview)
	  collapsed:: true
		- Reusable workflows
		  ``` yaml
		  on:
		    workflow_call:
		  ```
		- Calling a reusable workflow
		  ``` yaml
		  jobs:
		    call-workflow-passing-data:
		      uses: octo-org/example-repo/.github/workflows/reusable-workflow.yml@main
		      with:
		        config-path: .github/labeler.yml
		      secrets:
		        envPAT: ${{ secrets.envPAT }}
		  ```
		- Using outputs from a reusable workflow
		  
		  ``` yaml
		  name: Reusable workflow
		  
		  on:
		    workflow_call:
		      # Map the workflow outputs to job outputs
		      outputs:
		        firstword:
		          description: "The first output string"
		          value: ${{ jobs.example_job.outputs.output1 }}
		        secondword:
		          description: "The second output string"
		          value: ${{ jobs.example_job.outputs.output2 }}
		  
		  jobs:
		    example_job:
		      name: Generate output
		      runs-on: ubuntu-latest
		      # Map the job outputs to step outputs
		      outputs:
		        output1: ${{ steps.step1.outputs.firstword }}
		        output2: ${{ steps.step2.outputs.secondword }}
		      steps:
		        - id: step1
		          run: echo "firstword=hello" >> $GITHUB_OUTPUT
		        - id: step2
		          run: echo "secondword=world" >> $GITHUB_OUTPUT
		  
		  ```
	- issues
		- [How do I get the output of a specific step in GitHub Actions?](https://stackoverflow.com/questions/59191913/how-do-i-get-the-output-of-a-specific-step-in-github-actions)
			- three things:
				- Add an [`id`](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions#jobsjob_idstepsid) to the step you want the output from
				- Create the outputs using the [`GITHUB_OUTPUT`](https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions#setting-an-output-parameter) environment variable
				- [Use the id](https://docs.github.com/en/actions/reference/context-and-expression-syntax-for-github-actions#steps-context) and the output name in another step to get the outputs and then [join](https://docs.github.com/en/actions/learn-github-actions/expressions#join) them into one message for slack
			- example
			  ``` yaml
			  - name: Run tests
			    run: |
			      echo "mix-compile--warnings-as-errors=$(mix compile --warnings-as-errors)\n" >> $GITHUB_OUTPUT
			      echo "mix-format--check-formatted=$(mix format --check-formatted)\n" >> $GITHUB_OUTPUT
			      echo "mix-ecto_create=$(mix ecto.create)\n" >> $GITHUB_OUTPUT
			      echo "mix-ecto_migrate=$(mix ecto.migrate)\n" >> $GITHUB_OUTPUT
			      echo "mix-test=$(mix test)\n" >> $GITHUB_OUTPUT
			    id: run_tests
			    env:
			      MIX_ENV: test
			      PGHOST: localhost
			      PGUSER: postgres
			  
			  - name: Slack Notification
			    uses: rtCamp/action-slack-notify@v2
			    env:
			      SLACK_MESSAGE: ${{join(steps.run_tests.outputs.*, '\n')}}
			      SLACK_TITLE: CI Test Suite
			      SLACK_WEBHOOK: ${{ secrets.SLACK_WEBHOOK }}
			  ```