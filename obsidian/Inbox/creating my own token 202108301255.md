---
status:
  - in_progress
  - writing_idea
tags:
  - code
  - project
---

Goal: Deploy my own token named razzle-dazzle

Here I'll write down my experience creating my own token. I'll be following few tutorials, and will try to link to all of them.

1. Install brownie as suggested in their docs page ([link](https://eth-brownie.readthedocs.io/en/stable/install.html))
2. Start a token project via `brownie bake token`
3. Rename the `token` folder to whatever you want (e.g. `razzle-dazzle`)
4. Do `poetry init`
	1. set the project version to `^3.8`, as is requires by `eth-brownie`
	2. do pyenv `local 3.9.6`
5. upgraded the pytest version (required by `eth-brownie`)  via `poetry add -D pytest@latest`
6. add `eth-brownie` as a dep via `poetry add eth-brownie@^1.10.0`