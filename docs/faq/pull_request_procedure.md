---
icon: material/source-pull
title: Request changes: Pull Request Procedure
---

By default, **PGTEC VRAIN** is an open documentation portal where contributors can propose modifications.  
However, these changes must go through a **review process** using [*pull requests*](https://docs.github.com/pull-requests) to ensure quality and consistency.

---

## 1. Fork of the PGTEC VRAIN repo

The first step to editing the content of PGTEC VRAIN is to create a copy of the repository in your personal GitHub account.  
This is done by creating a **Fork** from the official [GitHub repository](https://github.com/pgtec-vrain/pgtec-vrain.github.io).

1. While logged into GitHub, click on the `Fork` button.
    1. (*Optional*) Deselect the checkbox if you do not need to copy all branches.
2. Confirm to create the fork.

![repo_fork](./img/1_fork-2_create_fork.png) 

---

## 2. Selecting the branch to edit

From your fork of the PGTEC VRAIN repository, you can switch to the branch that you need to edit.

![change_branch](./img/3_change_branch.png)

!!! success "Verification of the fork"

    You can verify that you are working in your own fork by checking that you are in **your GitHub account**.  
    Just below the repository name, it will state that it has been **forked from `pgtec-vrain/pgtec-vrain.github.io`**.

---

## 3. Editing the content  

Make the necessary modifications in your fork and commit the changes.

![commit_changes](./img/4_commit_changes.png)

---

## 4. Publishing the changes for review (Pull Request)

When you are ready, go to the `Pull requests` tab (1) in your forked repository and click on `New pull request` (2).

![create_new_pull_request](./img/5_create_new_pull_request.png)

!!! warning "IMPORTANT"

    Select the correct branches for the pull request:

    |                 |            *Repository name*                   |  *Branch name*  |
    |----------------:|:----------------------------------------------:|-----------------|
    | **Destination** |      `pgtec-vrain/pgtec-vrain.github.io`       | `<branch_name>` |
    |    **Origin**   | `<your_github_account>/pgtec-vrain.github.io`  | `<branch_name>` | 

    Ensure that the **branch names match** between the destination and your fork.

    ![comparing_changes](./img/6_comparing_changes.png)

---

## 5. Final step

Review that all the commits with your changes appear in the comparison view.  
Once confirmed, create the pull request.  

If everything is correct, your contribution will appear in the repository `pgtec-vrain/pgtec-vrain.github.io` where it will be reviewed and, if approved, published in the **official PGTEC VRAIN portal**.

![publish_pull_request](./img/7_publish_pull_request.png)
