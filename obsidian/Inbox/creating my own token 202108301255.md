---
status:
  - in_progress
  - writing_idea
tags:
  - code
  - project
---

Goal: Deploy my own token named razzle-dazzle
Repo: https://github.com/rasulkireev/razzle-dazzle

Here I'll write down my experience creating my own token. I'll be following few tutorials, and will try to link to all of them.

1. Install brownie as suggested in their docs page ([link](https://eth-brownie.readthedocs.io/en/stable/install.html))
2. Start a token project via `brownie bake token`
3. Rename the `token` folder to whatever you want (e.g. `razzle-dazzle`)
4. Do `poetry init`
	1. set the project version to `^3.8`, as is requires by `eth-brownie`
	2. do `pyenv local 3.9.6`
5. upgraded the pytest version (required by `eth-brownie`)  via `poetry add -D pytest@latest`
6. add `eth-brownie` as a dep via `poetry add eth-brownie`
7. add `vyper` as a dependency `poetry add vyper`
	1. If there are any poetry versioning issue (e.g. `eth-brownie` depends on `vyper {version something, something}` ) install vyper like this: `poetry add vyper@^{required version}`
8. (Optional) install pre-commit and add pre-commit yaml file.
9. open up the brownie console
	1. Open up ganache ui ([download link](https://www.trufflesuite.com/ganache)) 
	2. see what port is the server on.
	3. in `brownie-config.yaml` modify the following block:
		```yaml
		networks:
			default: development
			development:
				...
				cmd_settings: null
		```
				to this
		```yaml
		networks:
			default: development
			development:
				...
				cmd_settings:
				  port: 7545
		```
	4. Run `poetry run brownie console` to start exploring
	5. in the console run `accounts` and you should see the same list as in the ganache ui
	6. try doing some actions on [accounts](https://eth-brownie.readthedocs.io/en/stable/core-accounts.html), transaction and [contracts](https://eth-brownie.readthedocs.io/en/stable/core-contracts.html)

1. created a project on infura.io, created a new wallet on metamask
2. created a .env file in the root of the project and added it to .gitignore
3. added the infura.io project id and metamask wallet private key as env variables in .env file
4. added python-dotenv dependency to make it easy to work with env variables
	1. if you ever run into an issue with dependency versioning like below try installing the exact version that is "requested". This is because `eth-brownie` is somewhat strict on versions it uses for some packages.![[poetry versioning error 202108301718.png]]
	2. load in env variables like so ([commit](https://github.com/rasulkireev/razzle-dazzle/commit/1c2bcdba52bf5e4d54301787b765b1edda815c03)) :
		```python
		#!/usr/bin/python3
		import os
		from dotenv import load_dotenv

		load_dotenv()
		INFURA_PROJECT_ID = os.getenv("INFURA_PROJECT_ID")
		```
			
1. added `wallets` key to the brownie-config file to be able to access private_key in the console. Add via ${PRIVATE_KEY} syntax. 
	> ! Warning it will be seen in console when compiled
2. 