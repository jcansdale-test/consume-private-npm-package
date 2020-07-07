# consume-private-npm-package
Consume a private npm package

1. Generate public/private rsa key pair

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

2. Go to Repository > Settings > Deploy keys and use contents of `id_rsa.pub` to add a deploy key

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDZkZefm6iJVMWaO7hBMKmnJCTxzN4u8Svg3IvTkVbRlYDrrMtYUL1FdO16C+x18pqHDBkyoe9khR8WkqRTAgk4NhZltJthqtkwrxl6xRCMwaD7zAaxdOKh8Y1jwu2nUf7wSYgpm2F3SHO8crwO4yXd/ZvStpqpD2bPt6bh+qXixZEkoJ5aJszgVvZ+VcsrCDD5k7vGNMS8PUTH32Q2lpo1gyzxMd/K7ENhTW/idfqyDublfQeceMbo2i4+RgyMAG9vo93l6wAqFQ2MZDvmObKdXcGylLWLdjdRs4iBm/hu59g/l3ca/9no25isAhixWtgVrfG844mV8qpl57/AGKRYdG6NsbC4xOSn0XiJMLLQ2kXWe/x+8bPKcFWyfAe8HA8idpQutf0e3fNANrEBVwgmpMMkQ3wBdzqm9dHp84yDyhDlRV3CARNn9JALXmjf6X2sc+Ahn5dl7tuG0XlFFPyIdAvu7trrBMzR9YT/7lLv9bt0IyfIsQqCOyDfmYsL3SfhP3ECmNcIdfgalOiCXDTnMIyuIc3zuznbHkGnemRti7Lm7oi7IqN6tHYR4SXr7qz+n948uGOyEYT8XGKRlv73GbF8llwDKSgKqBiLncqgF+o4R+zanJJhzDQ7e7qpPOs39egzGS+2yz1tKtabSVuF1l/XvGrKs/rp58mXQwkM1Q== your_email@example.com
```

3. Add contents of `id_rsa` as repository/org secret `SECRET_PRIVATE_DEPLOY_KEY`

4. Install SSH key in workflow step

```
- run: |
    mkdir ~/.ssh
    echo "${{ secrets.SECRET_PRIVATE_DEPLOY_KEY }}" > ~/.ssh/id_rsa
    chmod 600 ~/.ssh/id_rsa
```

5. Install private npm package

```
- run: npm install jcansdale/private-npm-package#1.0.2
```

6. Execute private npm package

```
- run: npx jcansdale/private-npm-package#1.0.2
```
