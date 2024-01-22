---
layout: post
title: "Send emails with SendGrid with Python 3"
---

I wanted to send emails with Twillio SendGrid. It offers a generous free tier. Set up the domain and authenticate the identity. You have to generate an API key with "Mail Send" privileges. 

Set up your environment variables. My script will pick up credentials from the environment variables.

```bash
export SMTP_USER="apikey"
export SMTP_PASSWORD="<replace_the_api_key>"
export SMTP_SERVER="smtp.sendgrid.net"
export SMTP_PORT=465
```

This snippet only uses Python standard libraries.

```python
import os
import smtplib
from email.message import EmailMessage


def send_mail(
    subject,
    body,
    from_address,
    to_address,
    cc_address=[],
    file_list=[],
    message_id="",
):

    msg = EmailMessage()
    msg["Subject"] = subject
    msg["From"] = from_address
    msg["To"] = to_address

    if cc_address != []:
        msg["Cc"] = cc_address

    if message_id != "":
        msg["In-Reply-To"] = message_id
        msg["References"] = message_id

    msg["Bcc"] = from_address
    msg.set_content(body)

    for file_path in file_list:
        with open(file_path, "rb") as file_reader:
            file_data = file_reader.read()
        msg.add_attachment(
            file_data,
            maintype="application",
            subtype="octet-stream",
            filename=os.path.basename(file_path),
        )

    smtp_user = os.environ.get("SMTP_USER")
    smtp_password = os.environ.get("SMTP_PASSWORD")
    smtp_server = os.environ.get("SMTP_SERVER")
    smtp_port = os.environ.get("SMTP_PORT")

    with smtplib.SMTP_SSL(smtp_server, smtp_port) as server:
        server.login(smtp_user, smtp_password)
        server.send_message(msg)
```

Now we can simply send an email like this.

```python
from email.utils import formataddr

send_mail(
    subject="Planet Express order status",
    body="We have to deliver a package!",
    from_address= formataddr(('Fry', 'fry@futurama.com')),
    to_address=[formataddr(('Leela', 'leela@futurama.com'))]
)
```

### Tags

- email
- twillio
- python
- smtp
