# Mirror-and-synchronizing (BITBUCKET TO GITHUB MIGRTION AND SYNCRONIZATION)
Mirror and synchronizing GitHub & Bitbucket repository.

# OBJECTIVE: Migrating your existing bitbucket repo to GitHub repo, synchronizing them in shuch a way that when ever a change is made in the source repository(Bitbucket) the same change will be replecated in GitHub without any manuel intervention.
https://github.com/kingakwa/Mirror-and-synchronizing-akwa/blob/main/migration-bitbucket-github.jpg

#1. On GitHub, create a new repository
  - On your Bitbucket
      Navigate to your Bitbucket repository Example "Mirroring-Repo" Create an access token under Repository settings > Security > Access tokens
      Create Repository Access Token with selecting all the "READ" Permission
      Copy the last Access token Example { "https://x-token-auth:ATCTT3xFfGN0TSG5xC5PMZex1aEWC2wMY7j1SiYTwLpR7WTpHQ4DJ1oRfevWbd-LVn9bRzmr3csDN4DEjT57KYlsxWcKXnk5zW17DLJ9ssRcOFFwegxzPTMS-MAfumre3yDmXup-z1nHb8XSRGI9N_McR6FRyHArzIoPIWiJSk6cQfYqfAkIw_w=65FC4ty63@bitbucket.org/demo-migration12/solstice_demo.git" }
    
    ![Screen Shot 2024-01-04 at 00 27 57](https://github.com/asaphdanchi/Mirror-and-synchronizing/assets/112729006/666aed90-75a8-4c57-bbe0-fe4f266ad578)
    
      Navigate To Github and Import the Repository while keeping the same name "Mirroring-Repo"
    
  - On Bitbucket, Enable Pipelines under Repository settings > Pipelines > Settings
    
    ![Screen Shot 2024-01-04 at 00 30 21](https://github.com/asaphdanchi/Mirror-and-synchronizing/assets/112729006/bb456d6f-1f72-44c4-b2a4-7b9ef099718a)
    
  - On Bitbucket, Generate keys under Repository settings > Pipelines > SSH keys. Copy the public key to clipboard
  - On the same page, under Known hosts enter github.com as the Host address and then click Fetch followed by Add host
  - On GitHub, add the public key under Settings > Security > Deploy keys > Add deploy key. Tick the checkbox to Allow write access
    
    ![Screen Shot 2024-01-04 at 00 35 39](https://github.com/asaphdanchi/Mirror-and-synchronizing/assets/112729006/2545afe7-52c3-4934-a181-6a1a9b06e447)
    
  - On Bitbucket, add the public key under Repository settings > Security > Access keys > Add key
    
    ![Screen Shot 2024-01-04 at 00 36 53](https://github.com/asaphdanchi/Mirror-and-synchronizing/assets/112729006/39271cf9-d5f6-4488-abe4-5fd91dcecb08)
    
  - On Bitbucket, Create an access tokens under Repository settings > Security > Access tokens. Create Repository Access Token with  selecting all the "READ" Permission and tick the checkbox of Webhooks
  - Copy the first Token Example { "ATCTT3xFfGN0TSG5xC5PMZex1aEWC2wMY7j1SiYTwLpR7WTpHQ4DJ1oRfevWbd-LVn9bRzmr3csDN4DEjT57KYlsxWcKXnk5zW17DLJ9ssRcOFFwegxzPTMS-MAfumre3yDmXup-z1nHb8XSRGI9N_McR6FRyHArzIoPIWiJSk6cQfYqfAkIw_w=65FC4ty63" }
    
   ![Screen Shot 2024-01-04 at 00 37 47](https://github.com/asaphdanchi/Mirror-and-synchronizing/assets/112729006/0af2b9ef-5063-49fa-8170-88dae0d09844)

  - On Bitbucket, Create a Repository variables under Repository Settings > Pipeline > Repository variable. Naming the variable Example " BITBUCKET_VARIABLE"
    
    ![Screen Shot 2024-01-04 at 00 39 25](https://github.com/asaphdanchi/Mirror-and-synchronizing/assets/112729006/ede419ec-4553-4dd4-adb6-649f2fe56602)
    
  - On Github, At the top right click on your Profile, Scroll down at the bottom click on settings
    
    ![Screen Shot 2024-01-04 at 00 45 35](https://github.com/asaphdanchi/Mirror-and-synchronizing/assets/112729006/68a20ce1-ad1e-44cb-8b84-1729dbc8b212)
    
  - At the bottom left of the page click Developer Settings, Create a Personal access tokens Under Personal access tokens > Token (classic) > Generate new token > Generate new token (classic)
    
    ![Screen Shot 2024-01-04 at 00 49 19](https://github.com/asaphdanchi/Mirror-and-synchronizing/assets/112729006/88398cca-a40f-4afd-ba11-50f2a7ee1ecf)
    
  - Check the "repo" box, "Workflow" box and the "write:package" box. Genarate Token and copy the token Example "ghp_zY5GxaeytuAZlR4tPcwqovPz7c2ZVy1kdfg"
   
    ![Screen Shot 2024-01-04 at 00 52 09](https://github.com/asaphdanchi/Mirror-and-synchronizing/assets/112729006/a0237460-df31-480e-b2df-136dab880c68)
    
  - On Bitbucket, Create a Repository variables with the Access Token from Github under Repository Settings > Pipeline > Repository variable. Naming the variable Example "GITHUB_VARIABLE"

# Inside the Bitbucket repo, create a bitbucket-pipelines.yml file containing the following:

```
  pipelines:
    default:
      - step:
          name: Sync GitHub Mirror
          image: alpine/git:latest
          clone:
            enabled: false
          script:
            - git clone --mirror https://x-token-auth:"$BITBUCKET_VARIABLE"@bitbucket.org/demo-migration12/Mirroring-Repo.git ## @bitbucket.org follow by your Bitbucket repository path
            - cd Mirroring-Repo.git ## cd followed by your Github repository Name
            - git push --mirror https://x-token-auth:"$GITHUB_VARIABLE"@github.com/asaphdanchi/Mirroring-Repo.git ## @github.com followed by your Github repository path
```

On your code replace the "$BITBUCKET_VARIABLE" and "$GITHUB_VARIABLE" with your corresponding variable names while keeping the $ and the "" sign. 

# Run the pipeline in Bitbucket


![Screen Shot 2024-01-04 at 02 57 05](https://github.com/asaphdanchi/Mirror-and-synchronizing/assets/112729006/4b9e2dab-e59c-41a8-9b1f-9a09db958d75)


# HAPPY LEARNING 🙂
