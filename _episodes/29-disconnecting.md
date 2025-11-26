---
title: "Disconnecting properly"
teaching: 5
exercises:
questions:
objectives:
- Preventing any orphan processes from running on login nodes indefinitely
- Preventing VSCode from overloading the login nodes
- Preventing VSCode from consuming your quota in the file system
keypoints:
- 
---

## Preventing any orphan processes from running on login nodes indefinitely

You should always end a remote session by clicking the `SSH connection status` box in the lower left corner of VSCode and selecting the `Close Remote Connection` option.


## Additional good practice

There are additional good practice steps you should take as a user of VSCode on HPC systems like Setonix. These are listed below, and [described in more detail here](https://pawsey.atlassian.net/wiki/spaces/US/pages/51931360/Visual+Studio+Code+for+Remote+Development). 

1. Regularly remove any leftover orphan processes on the login nodes.
2. Prevent VSCode from overloading the login nodes by:
   - Avoiding the use of VSCode filewatcher and file searcher to pay attention to directories with large number of files: they will index all the files that you have access to in your workspace, which can consume significant resource on the login nodes.
   - Disabling both TypeScript and JavaScript Language Services in VSCode.
3. Prevent the unnecessary consumption of quota in the file system by moving the `.vscode-server` directory located in `$HOME` to a "fakeHome" directory (i.e. `/software/projects/<project>/<username>/fakeHome`).


### Acknowledgements

Content adapted with permission from Pawsey Supercomputing Research Centre user support documentation: [`Visual Studio Code for Remote Development`](https://pawsey.atlassian.net/wiki/spaces/US/pages/51931360/Visual+Studio+Code+for+Remote+Development).