# steamed-llc.github.io
Website of STEAM Education Supply, LLC.

## Domain

Two domains are purchased from https://porkbun.com

- steamed.llc (expires in 2036, auto renewal disabled)
- steamed.supply (expires in 2036, auto renewal inabled)

Both have been verified on https://github.com/organizations/steamed-llc/settings/pages so that others cannot claim them on GitHub. The verification process is shown on https://github.com/organizations/steamed-llc/settings/pages_verified_domains/steamed.supply, which requires creating a TXT record on https://porkbun.com by clicking the pencil icon near "DNS RECORDS".

The second domain has been selected on https://github.com/steamed-llc/steamed-llc.github.io/settings/pages for the company's landing page: https://steamed.supply. Other repos under the same organization automatically inherit this domain.

https://porkbun.com provides a "Quick Setup" for GitHub Pages when one tries to set up new DNS records. Use this one instead of manual setup.

## Email

### Receiving

https://porkbun.com can forward 20 fake addresses to a real one. For example, any email sent to contact@steamed.supply is forwarded to steamed.supply@gmail.com.

### Sending

https://app.brevo.com is used to enable sending emails through a fake address. Both domains have been authenticated on https://app.brevo.com/senders/domain/list. There is no need to set up a branded subdomain there.

Every address forwarded from https://porkbun.com need to be set up as a sender on https://app.brevo.com/senders/list before it can be used to send out emails.

The last step is to add those fake addresses on https://mail.google.com/mail/u/0/#settings/accounts as "Send mail as"-addresses. Keep "Treat as an alias" checked. The SMTP server settings are shown on https://app.brevo.com/settings/keys/smtp, and the SMTP key is saved in Apple Passwords.

