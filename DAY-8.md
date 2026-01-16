GIT BRANCH STRATEGIES---------

1 FAST-FORWARD MERGE

2 THREE WAY MERGE OR RECURSIVE MERGE OR ORT[ Ostensibly Recursive's Twin ]

       ----------FAST-FORWARD MERGE----------
<img width="960" height="1280" alt="image" src="https://github.com/user-attachments/assets/14b36f99-2356-489c-8474-09264cebf458" />



------------------THREE WAY MERGE OR RECURSIVE MERGE OR ORT[ Ostensibly Recursive's Twin ]------------
<img width="960" height="1280" alt="image" src="https://github.com/user-attachments/assets/0fe5d922-6d93-4adc-815e-89ba30d3ca54" />

GIT CHERRY-PICK:--

Git cherry-pick selects specific commits from one branch and applies them to another, creating new commits with identical changes but different hashes. This enables precise integration of fixes or features without merging entire branches, ideal for DevOps scenarios like hotfixes or backporting security patches to stable releases.
![WhatsApp Image 2026-01-16 at 11 21 42](https://github.com/user-attachments/assets/3af85e78-3a43-4fd4-a305-2ad99ffb9f50)

    
    git log bugfix --oneline  # Find hash, e.g., e9763af
    
    git cherry-pick e9763af   # Applies bugfix-3 to main as new commit



