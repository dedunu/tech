---
layout: post
title: Create PrivateBin using Python 3
---

I wanted to create a PrivateBin note with Python. It looks so easy at a glance. But request has to be encrypted properly. 

Luckily, I found this python repository <https://github.com/r4sas/PBinCLI>. I stripped out things needed for creating post. You might need below dependencies to be installed in order to make it work.

- requests
- base58
- pycryptodome

```python
"""
This script creates a PrivateBin using Python 3. 
Code is based on https://github.com/r4sas/PBinCLI repository. 
Thanks a lot @r4sas!
Below modules should be installed in the environment.
requests
base58
pycryptodome
"""

import json
import requests
import traceback
import zlib
from Crypto.Cipher import AES
from Crypto.Hash import HMAC, SHA256
from Crypto.Protocol.KDF import PBKDF2
from Crypto.Random import get_random_bytes
from base58 import b58encode
from base64 import b64encode


def json_encode(string):
    return json.dumps(string, separators=(',', ':')).encode()


def compress(data):
    compressor = zlib.compressobj(wbits=-zlib.MAX_WBITS)
    return compressor.compress(data) + compressor.flush()


def initialize_cipher(key, iv, adata, tagsize):
    cipher = AES.new(key, AES.MODE_GCM, nonce=iv, mac_len=tagsize)
    cipher.update(json_encode(adata))
    return cipher


class PrivateBin:
    def __init__(self, message):
        self._server = "https://bin.idrix.fr/"
        self._version = 2
        self._compression = 'zlib'
        self._data = ''
        self._password = ''
        self._formatter = 'plaintext'
        self._message = message
        self._expiration = "7day"
        self._discussion = False
        self._burn_after_reading = False
        self._iteration_count = 100000
        self._salt_bytes = 8
        self._block_bits = 256
        self._tag_bits = 128
        self._key = get_random_bytes(int(self._block_bits / 8))

    def __get_hash(self):
        return b58encode(self._key).decode()

    def __derive_key(self, salt):
        return PBKDF2(
            self._key + self._password.encode(),
            salt,
            dkLen=int(self._block_bits / 8),
            count=self._iteration_count,
            prf=lambda password, salt: HMAC.new(
                password,
                salt,
                SHA256
            ).digest())

    def __encrypt(self):
        iv = get_random_bytes(int(self._tag_bits / 8))
        salt = get_random_bytes(self._salt_bytes)
        key = self.__derive_key(salt)

        adata = [
            [
                b64encode(iv).decode(),
                b64encode(salt).decode(),
                self._iteration_count,
                self._block_bits,
                self._tag_bits,
                'aes',
                'gcm',
                self._compression
            ],
            self._formatter,
            int(self._discussion),
            int(self._burn_after_reading)
        ]

        cipher_message = {
            'paste': self._message
        }

        cipher = initialize_cipher(key, iv, adata, int(self._tag_bits / 8))
        cipher_text, tag = cipher.encrypt_and_digest(compress(json_encode(cipher_message)))

        self._data = {
            'v': 2,
            'adata': adata,
            'ct': b64encode(cipher_text + tag).decode(),
            'meta': {
                'expire': self._expiration
            }
        }

    def create_post(self):
        session = requests.Session()
        self.__encrypt()
        result = session.post(
            url=self._server,
            headers={
                'X-Requested-With': 'JSONHttpRequest'
            },
            proxies={},
            data=json_encode(self._data).decode()
        )

        try:
            response = result.json()

            print("PasteID: " + response['id'])
            print("Password: " + self.__get_hash())
            print("Delete token: " + response['deletetoken'])
            
            link = "{}?{}#{}".format(self._server,
                                     response['id'],
                                     self.__get_hash())
            print("Link: " + link)

            return link
        except:
            print(traceback.format_exc())
            print("Error creating paste")


private_bin = PrivateBin("Sample Text")
print("Link returned: " + private_bin.create_post())
```

#### Gists

- <https://gist.github.com/dedunumax/75bff57e34ebf4a39356c8560434daef>

### Tags

- python
- privatebin