---
layout: post
title: "Python 3: Encrypting Ansible Vault programmatically"
---

`ansible` is the only module needed for this script.  If you don't need to specify `vault_id`, below code would work.

```python
from ansible.parsing.vault import VaultEditor, VaultSecret

vault_password = 'vault_password123'
secret_value = 'super_secret_123'
vault_id = None

encrypted_secret = VaultEditor().encrypt_bytes(secret_value,
                                               VaultSecret(bytes(vault_password, 'utf-8')),
                                               vault_id=vault_id).decode("utf-8")

encrypted_text = 'secret_token: !vault |\n      ' + encrypted_secret.replace('\n', '\n      ')

print(encrypted_text)
```

Omits: 

```
secret_token: !vault |
      $ANSIBLE_VAULT;1.1;AES256
      66353534363061653436373834373430646336326336393732303863336561303061666366323539
      6362616464613735373537633931626639616137366139630a623238353331376632653039643333
      34356564343365383465363939613266646636653065656432313533386532306532663861353336
      6531383463386364320a396564653362303463663630636431316561333633616465363838303166
      30346237613037316239633366363864323433653838663363386264636637396462
```

If you specify `vault_id='test-vault1'`, it will be added to the text as well.

```
secret_token: !vault |
      $ANSIBLE_VAULT;1.2;AES256;test-vault1
      31623361633964316532383939313530333630316466386138353836653732663531333361613634
      3566356366663832393166376361336263333734663234320a386165393633633233366639396636
      36343666346365623133633264633537316262343239383265323738636633646534636564343830
      3039623764666134620a323231363465346238623163386534353536313235353563333533633363
      30313166366364336338383935393037643363653434393864633835393839303333
```

### Tags

- python
- ansible
