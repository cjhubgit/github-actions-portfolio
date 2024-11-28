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





![ image alt](https://github.com/user-attachments/assets/82fafb46-75de-4c93-807e-04fe9d6b0e20)

The concurrency feature is used to limit workflow runs. This prevents multiple instances of the workflow from running simultaneously.	

Explanation:
•	${{ github.workflow }}: Refers to the name of the workflow file (9-1 Managing Concurrency), ensuring the workflow name is part of the concurrency group.
•	${{ github.ref }}: Refers to the branch or tag reference (e.g., main). This ensures concurrency is scoped to a specific branch or tag.
