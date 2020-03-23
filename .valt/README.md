# Valt: how to create new vars

See https://docs.ansible.com/ansible/latest/user_guide/vault.html

```bash

$ ansible-vault encrypt_string --vault-password-file .valt/pass 'foobar' --name 'the_secret'
the_secret: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          39393430353930366665636166663239303230653032343833643431323335663135306666323234
          6663663634313162633439346434333731386463653262330a333831383765633132323733393462
          66666335366239386333613661653435343833396261663236363136393333356530616162663536
          3032616439626338330a313163353332623166626235663063373236306130626630393935636565
          6563
Encryption successful
```

ansible-vault encrypt_string --vault-password-file .valt/pass 'xxxxx' --name ''