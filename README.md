# Hooks deployment automation

### created by Winckell benjamin 
### what are git hooks: https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks
### source for the hook-chain.sample here: http://stackoverflow.com/a/8734391

# Explanation
This folder will contain every hook scripted by Companeo for developers pc or preproduction/release servers
those hooks will be triggered at some specific git actions like checkout or commit etc...

# files tree

    ```shell
    .
    ├── createNewHook.sh // script for automaticly deploying a new hook
    ├── deployHooks.sh // script for automaticly deploying every hook from inside a folder
    ├── dev // folder used in dev env
    │   ├── post-checkout // copy of hook-chain.sample with only the good hookname
    │   ├── post-checkout.01_pull // first sub hook to be called
    │   ├── post-checkout.02_gruntComposer // second
    │   ├── post-checkout.03_npmInstall // etc
    │   ├── post-checkout.04_tasksRunner //last sub hook which contain every grunt build cmd you want to run after every checkout
    │   ├── pre-commit
    │   └── pre-commit.01_esLint_js_files
    ├── hook-chain.sample // root file for create sub hooks
    ├── preProd // folder for preprod hooks
    ├── README.md
    └── toolsScript
        ├── check_and_run.sh
        ├── color.sh
        └── logHook.sh
    ```
# How To Deploy hooks for Dev or Staging
	
Run `deployHooks.sh` with one param `development` or `staging`

## Params explanation

1. development: use this params on developers pc only.
2. staging: use this params on preprod and release servers only.


    ```shell

    /bin/bash deployHooks.sh  # don't forget one of the two params available

    ```

# How to create a new hook from scratch

1. Copy `hook-chain.sample` and rename it with the good git hook name targeted

		```shell
			/bin/bash createNewHook.sh // and follow the script
		```
2. Create new files inside your previously selected directory with this pattern: `myHookName.xx_taskToDo`

    - myHookName: 	is the same as the one you choosed for hook-chain.sample copy name
    - xx:  			incremental number to be sure of execute you hook in a good order
    - taskTodo: 		replace by the name of what this sub hook will do
3. Run `deployHooks.sh` like explained before at How to Deploy section

		```shell
			/bin/bash deployHooks.sh
		```
