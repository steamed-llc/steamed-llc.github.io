# Website of STEAM Education Supply, LLC.

## Deployment

Pages of private repos under a free GitHub account cannot be hosted on GitHub. That's why this repo is kept public.

CloudFlare, Netlify, Vercel, etc., can host pages of private repos from GitHub for free, but each repo need a domain or subdomain. Setting a path like url, such as https://steamed.supply/beard, requires additional routing.

`steamed-llc-github-io` on CloudFlare is used to test this kind of deployment. Note that one needs to choose the "Legacy Pages Workflow" instead of the integrated "Workers & Pages" one with the build command `jekyll build` and build output `_site` and environment variable `RUBY_VERSION=3.2.3`.

## Domain

Two domains are purchased from https://porkbun.com

- steamed.supply (expires in 2036, auto renewal enabled)
- steamed.llc (expires in 2036, auto renewal disabled)

Both have been verified on the [organization's pages settings[(https://github.com/organizations/steamed-llc/settings/pages) so that others cannot claim them on GitHub. The verification requires creating a TXT record in the DNS manager.

### Domain for Customers

The 1st domain is customer-facing. It has been selected in this [project's pages settings](https://github.com/steamed-llc/steamed-llc.github.io/settings/pages) as the company's landing page: https://steamed.supply. Other repos under the same organization automatically inherit this domain, for example, https://steamed.supply/beard.

This domain's DNS records are managed by Porkbun, which provides a "Quick Setup" for GitHub Pages when one tries to set up new DNS records, which was used instead of the manual configuration detailed in [GitHub Docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain).

### Domain for the Company

The 2nd domain is government-facing. It is used for registration, verification, etc. Its DNS records are managed by https://www.cloudflare.com, where a worker named `change-hostname` is used to convert all request to the 2nd domain to the 1st so that both domains points to the same deployed GitHub Pages through `worker.js`:

```javascript
export default {
  async fetch(request, env, ctx) {
    const url = new URL(request.url);
    url.hostname = 'steamed.supply';

    const modifiedRequest = new Request(url.toString(), {
      method: request.method,
      headers: request.headers,
      body: request.body,
      redirect: 'manual',
    });

    modifiedRequest.headers.set('Host', 'steamed.supply');

    return fetch(modifiedRequest);
  }
};
```

The worker has a custom route `*steamed.llc/*` to Zone `steamed.llc`.

## Email

### Receiving

https://porkbun.com can forward 20 fake addresses to a real one. For example, any email sent to contact@steamed.supply is forwarded to steamed.supply@gmail.com.

### Sending

https://app.brevo.com is used to enable sending emails through a fake address. Both domains have been authenticated on https://app.brevo.com/senders/domain/list. There is no need to set up a branded subdomain there.

Every address forwarded from https://porkbun.com need to be set up as a sender on https://app.brevo.com/senders/list before it can be used to send out emails.

The last step is to add those fake addresses on https://mail.google.com/mail/u/0/#settings/accounts as "Send mail as"-addresses. Keep "Treat as an alias" checked. The SMTP server settings are shown on https://app.brevo.com/settings/keys/smtp, and the SMTP key is saved in Apple Passwords.

