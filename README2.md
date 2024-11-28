# github-actions-portfolio
Workflow: Managing Concurrency
Objective
The goal of this workflow is to demonstrate how to manage concurrency in GitHub Actions, ensuring that only one instance of a workflow runs at a time for a specific branch.
Workflow Structure
1. Trigger Event
The workflow is triggered manually using workflow_dispatch. This allows the workflow to be started only when you manually trigger it.

![ image alt ](https://github.com/cjhubgit/github-actions-portfolio/blob/411b38f0307c692f2854a9cf72dbf67ed5fc6979/concurrency.jpg)


Workflow Structure
Defining Concurrency





![ image alt](https://github.com/cjhubgit/github-actions-portfolio/blob/456186212325182dd71894098a28f5e140cefe14/Defining%20concurrency.jpg)

The concurrency feature is used to limit workflow runs. This prevents multiple instances of the workflow from running simultaneously.	

Explanation:
•	${{ github.workflow }}: Refers to the name of the workflow file (9-1 Managing Concurrency), ensuring the workflow name is part of the concurrency group.
•	${{ github.ref }}: Refers to the branch or tag reference (e.g., main). This ensures concurrency is scoped to a specific branch or tag.

Workflow Structure
Jobs section 

The ping job demonstrates how to use concurrency while performing a custom task like pinging a URL using a custom Docker action. 

![ image alt](https://github.com/cjhubgit/github-actions-portfolio/blob/e3b34a358779b2540d7ae9d1c9dc8b0659bb8ccf/workflow-structure.jpg)

Explanation:
•	runs-on: ubuntu-latest: Specifies the operating system where the job runs.
•	Concurrency Block: Ensures only one ping job runs at a time for the same workflow and branch.
•	Steps:
o	Checkout Code: Retrieves the repository code.
o	Ping URL: Uses a custom Docker action (docker-ping-url) to ping a specified URL.

1. url: The URL to ping (in this case, an intentionally invalid one).
2. max_trials: The maximum number of retry attempts.
3. delays: The delay (in seconds) between retry attempts.


Testing workflow

1.	Push to the Main Branch
Commit and push a change to the main branch to trigger the workflow.
Screenshot Opportunity:
Take a screenshot of the GitHub Actions page showing the triggered workflow.
2.	Trigger Another Workflow
Push another change while the first workflow is running to observe concurrency management.

![ image alt]( https://github.com/cjhubgit/github-actions-portfolio/blob/9f86262dc1c32b4cd771235ce4aa15721eeeb069/testing-workflow.jpg)

Testing the Workflow
In this example, I triggered the workflow 19-1 Managing Concurrency multiple times manually for the main branch. GitHub's concurrency feature took over and ensured that only one workflow runs at a time, while the others were either cancelled or queued. 

Here's what’s happening:
1.	Cancelled Workflows:
o	Runs #4, #5, and #6 were cancelled automatically because a newer workflow (#7) was triggered. GitHub doesn’t let multiple workflows from the same concurrency group run simultaneously.
2.	Running Workflow:
o	Run #7 is the most recent active workflow, so it’s currently running. GitHub allows this workflow to proceed because it’s the latest one in the group.
3.	Pending Workflow:
o	Run #8 is in a "Pending" state, waiting for Run #7 to finish before it can start. This ensures workflows don’t overlap and cause conflicts.

Why This Matters:
This screenshot is a great example of GitHub's concurrency feature in action. It shows how GitHub prevents redundant runs and ensures only the most relevant workflow continues, saving time and resources




