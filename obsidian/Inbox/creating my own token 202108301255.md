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
	> Note: if you ever run into an issue with dependency versioning like below try installing the exact version that is "requested". This is because `eth-brownie` is somewhat strict on versions it uses for some packages.![[poetry versioning error 202108301718.png]]
		
5. added `wallets` key to the brownie-config file to be able to access private_key in the console. Add via ${PRIVATE_KEY} syntax. 
	> ! Warning it will be seen in console when compiled
6. Add the account [locally](https://eth-brownie.readthedocs.io/en/stable/account-management.html#local-accounts) like this `poetry run brownie accounts new {account name you want}`. Replace `{account name you want}` with an account name you want. You will be asked for a PRIVATE_KEY and PASSWORD. For the PRIVATE_KEY use the the key that you saved in .env file. For password, come up with a password (preferrably with a password generator like BitWarden and save it).
7. added unlock key to brownie config to "unlock" the new account, in development: 
```yaml
networks:
    default: development
    development:
        cmd_settings:
          port: 7545
          unlock: # new
            - 0x7E1E3334130355799F833ffec2D731BCa3E68aF6 # new
```

1. Now also, let's load the wallet we have created into the token creation script like so:
	```python
#!/usr/bin/python3
import os

from brownie import Token, accounts

def main():
    account = accounts.load('razzle-dazzle-wallet') #new
    return Token.deploy("Razzle Dazzle", "RD", 18, 1e20, {"from": account})
	```
> Note: 18 in the function above refers to the number of digits the token will have and the second number refers to the amount of token you want to be produced. In my case there should be 100 tokens created.
1. Let's test this on the Rankeby network. Run `poetry run brownie run token.py --network rinkeby` in your terminal. You will be asked for the wallet password that we created earlier.
2. Once the request completes, take the address from `Token deployed at:`line and copy it. Go to your Metamask wallet and click on Add Token. There enter token address and other info should auto populate. Click Add and Et Voila! You have created a token!
3. If you are happy with how this turned out you can try deploying your token on the Polygon Network, next.
4. To do that first run on the polygon test networks like so `poetry run brownie run token.py --network polygon-test`
	1. if you receving an error like this:
	> HTTPError: 403 Client Error: Forbidden for url: https://polygon-mumbai.infura.io/v3/0f07ea70a44c46a8b5b205226e91750f

	This could be because infura server is experienceing latency issues. Give this another try a little later, or check their status page ([link](https://status.infura.io)) 