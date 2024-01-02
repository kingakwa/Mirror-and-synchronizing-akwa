# Mirror-and-synchronizing
Mirror and synchronizing GitHub &amp; Bitbucket repository

# On GitHub, create a new repository (import or from scratch)
  - Importing a private repository from Bitbucket to Github
      Navigate to your Bitbucket repository Example "Mirroring-Repo" Create an access token under Repository settings > Security > Access tokens
      Create Repository Access Token with selecting all the "READ" Permission
      Copy the last Access token Example { "https://x-token-auth:ATCTT3xFfGN0TSG5xC5PMZex1aEWC2wMY7j1SiYTwLpR7WTpHQ4DJ1oRfevWbd-LVn9bRzmr3csDN4DEjT57KYlsxWcKXnk5zW17DLJ9ssRcOFFwegxzPTMS-MAfumre3yDmXup-z1nHb8XSRGI9N_McR6FRyHArzIoPIWiJSk6cQfYqfAkIw_w=65FC4ty63@bitbucket.org/demo-migration12/solstice_demo.git" }
      Navigate To Github and Import the Repository while keeping the same name "Mirroring-Repo"
    
  - On Bitbucket, Enable Pipelines under Repository settings > Pipelines > Settings
  - On Bitbucket, Generate keys under Repository settings > Pipelines > SSH keys. Copy the public key to clipboard
  - On the same page, under Known hosts enter github.com as the Host address and then click Fetch followed by Add host
  - On GitHub, add the public key under Settings > Security > Deploy keys > Add deploy key. Tick the checkbox to Allow write access
  - On Bitbucket, add the public key under Repository settings > Security > Access keys > Add key
  - On Bitbucket, Create an access tokens under Repository settings > Security > Access tokens. Create Repository Access Token with  selecting all the "READ" Permission and tick the checkbox of Webhooks
  - Copy the first Token Example { "ATCTT3xFfGN0TSG5xC5PMZex1aEWC2wMY7j1SiYTwLpR7WTpHQ4DJ1oRfevWbd-LVn9bRzmr3csDN4DEjT57KYlsxWcKXnk5zW17DLJ9ssRcOFFwegxzPTMS-MAfumre3yDmXup-z1nHb8XSRGI9N_McR6FRyHArzIoPIWiJSk6cQfYqfAkIw_w=65FC4ty63" }
  - On Bitbucket, Create a Repository variables under Repository Settings > Pipeline > Repository variable. Naming the variable Example " BITBUCKET_VARIABLE"
  - On Github, At the top right click on your Profile, Scroll down at the bottom click on settings
  - At the bottom left of the page click Developer Settings, Create a Personal access tokens Under Personal access tokens > Token (classic) > Generate new token > Generate new token (classic)
  - Check the "repo" box, "Workflow" box and the "write:package" box. Genarate Token and copy the token Example "ghp_zY5GxaeytuAZlR4tPcwqovPz7c2ZVy1kdfg"
  - On Bitbucket, Create a Repository variables with the Access Token from Github under Repository Settings > Pipeline > Repository variable. Naming the variable Example "GITHUB_VARIABLE"

# Inside the Bitbucket repo, create a bitbucket-pipelines.yml file containing the following:

  - git clone --mirror https://x-token-auth:"$BITBUCKET_VARIABL"@bitbucket.org/demo-migration12/Mirroring-Repo.git ## @bitbucket.org follow by your Bitbucket repository path
  - cd Mirroring-Repo.git ## cd follow by your Github repository Name
  - git push --mirror https://x-token-auth:"$GITHUB_VARIABLE"@github.com/asaphdanchi/Mirroring-Repo.git ## @github.com follow by your Github repositor path
  - On your code replace the "$BITBUCKET_VARIABL" and "$GITHUB_VARIABLE" with your corresponding variable names while keeping tha $ and the "" sign. Run the pipeline in Bitbucket
