### 1. Branches  
- For a new Feature, use a new Branch: `git checkout -b <issuenumber>/description-here`  
- Example: `git checkout -b 3/add-readme`.


### 2. Commits  
- **small/'atomic' commits**
- commit messages 
  - should complete the sentence: **"When applied this commit will..."**,  
start with a **captial letter** and end with a **dot and reference** their issue
  - **not surpass 72 symbols** to still be displayed inline on github  
- Example: "When applied this commit will" `Add a signup button to the main page. Ref #24`

  - If you need more lines (should not be necessary with atomic commits but sometimes it happens). Make the first line a concise conclusion, with the dot and reference. And add more description in following lines.    
Multiline example:  
    ```
    Add profile pages. Ref #41  
    - Add path to profile /:user/profile
    - Add profile icons
    - Add fancy dashboard about user actions:
    - Displays status messages, follows and eaten cookies
    ```
### 3. Pull Requests  
- Open a PR on github and add reviewers

### 4. Add more commits  
- Until your Pull Request is accepted

### 5. Merge 
- After a succsessfull review: rebase your branch to the curent state of the master  
(`git fetch` and then: `git rebase -i origin/master`) 
- and merge with option: **Rebase and Merge**.
