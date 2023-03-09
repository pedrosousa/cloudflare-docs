---
pcx_content_type: troubleshooting
source: https://support.cloudflare.com/hc/en-us/articles/4729826525965-Configuring-URL-forwarding-or-redirects-with-Page-Rules
title: Configuring URL forwarding or redirects with Page Rules
---

# Configuring URL forwarding or redirects with Page Rules



## Overview

If you want to forward or redirect traffic to a different URL, you have the following options using Cloudflare:

-   [Single Redirects](https://developers.cloudflare.com/rules/url-forwarding/single-redirects/): Create static or dynamic redirects at the zone level. Dynamic redirects are advanced URL redirects, such as redirects based on the source country of requests.
-   [Bulk Redirects](https://developers.cloudflare.com/rules/url-forwarding/bulk-redirects/): Define a large number (thousands or even millions) of essentially static URL redirects at the account level.
-   [Page Rules](https://support.cloudflare.com/hc/en-us/articles/4729826525965-Configuring-URL-forwarding-or-redirects-with-Page-Rules#how-to): Should only be used when the other two options do not meet your use case.

___

## Redirect with Page Rules

{{<Aside type="note">}}
Page Rule subdomains require an [\"Orange
Clouded\"](https://developers.cloudflare.com/dns/manage-dns-records/reference/proxied-dns-records)
DNS record for the Page Rule to work. Page Rules won\'t apply to
subdomains that don\'t exist in DNS or aren\'t being directed to
Cloudflare.
{{</Aside>}}

To configure URL forwarding or redirects using Page Rules:

1.  Log into your Cloudflare account.
2.  Click the appropriate Cloudflare account for the domain where you want to add URL forwarding.
3.  Go to **Rules** > **Page Rules**.
4.  Under **Page Rules,** click **Create Page Rule**. The _Create Page Rule for <your domain>_ dialog opens.
5.  Under **If the URL matches**, enter the URL or URL pattern that should match the rule. 
6.  In **Pick a Setting**, choose **Forwarding URL** from the drop-down menu.
7.  For **Select status code**, choose _301 (Permanent Redirect)_ or _302 (Temporary Redirect)_.
8.  Enter the _destination URL_.
9.  To finish, click **Save and Deploy**.

![Example Page Rule configuration for forwarding URLs with HTTP status code 301 (permanent redirect) or 302 (temporary redirect).](/support/static/hc-import-pagerules_urlforwarding_woptions_edited.png)

___

## Forwarding examples

{{<Aside type="warning">}}
Traffic must pass through Cloudflare for Page Rules to work. If you only
use Cloudflare for DNS, Page Rules are not active.
{{</Aside>}}

Imagine you want site visitors to easily reach your website for a variety of URL patterns.  For instance, the Page Rule URL patterns _\*www.example.com/products_ and _\*example.com/products_ match:


{{<raw>}}<pre class="CodeBlock CodeBlock-with-rows CodeBlock-scrolls-horizontally CodeBlock-is-light-in-light-theme CodeBlock--language-txt" language="txt"><code><span class="CodeBlock--rows"><span class="CodeBlock--rows-content"><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain"> http://example.com/products</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">
</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain"> http://www.example.com/products</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">
</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain"> https://www.example.com/products</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">
</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain"> https://blog.example.com/products</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">
</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain"> https://www.blog.example.com/products</span></div></span></span></span></code></pre>{{</raw>}}

but do not match:


{{<raw>}}<pre class="CodeBlock CodeBlock-with-rows CodeBlock-scrolls-horizontally CodeBlock-is-light-in-light-theme CodeBlock--language-txt" language="txt"><code><span class="CodeBlock--rows"><span class="CodeBlock--rows-content"><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">http://www.example.com/blog/products (extra directory before the +)  </span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">or</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">http://www.example.comproducts (no trailing slash)</span></div></span></span></span></code></pre>{{</raw>}}

Once you have created the pattern that matches what you want, click the **Forwarding** toggle. That exposes a field where you can enter the address I want requests forwarded to.


{{<raw>}}<pre class="CodeBlock CodeBlock-with-rows CodeBlock-scrolls-horizontally CodeBlock-is-light-in-light-theme CodeBlock--language-txt" language="txt"><code><span class="CodeBlock--rows"><span class="CodeBlock--rows-content"><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">https://example.com/products</span></div></span></span></span></code></pre>{{</raw>}}

If I enter the address above in the forwarding box and click **Add Rule**, within a few seconds any requests that match the pattern I entered will automatically be forwarded with a 302 Redirect to the new URL.

___

## Advanced forwarding options

If you use a basic redirect, such as forwarding the root domain to www.example.com, then you lose anything else in the URL.

For example, you could set up the pattern:\\


{{<raw>}}<pre class="CodeBlock CodeBlock-with-rows CodeBlock-scrolls-horizontally CodeBlock-is-light-in-light-theme CodeBlock--language-txt" language="txt"><code><span class="CodeBlock--rows"><span class="CodeBlock--rows-content"><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">example.com</span></div></span></span></span></code></pre>{{</raw>}}

And have it forward to:


{{<raw>}}<pre class="CodeBlock CodeBlock-with-rows CodeBlock-scrolls-horizontally CodeBlock-is-light-in-light-theme CodeBlock--language-txt" language="txt"><code><span class="CodeBlock--rows"><span class="CodeBlock--rows-content"><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">http://www.example.com</span></div></span></span></span></code></pre>{{</raw>}}

However, if someone entered: example.com/some-particular-page.html They would be redirected to:


{{<raw>}}<pre class="CodeBlock CodeBlock-with-rows CodeBlock-scrolls-horizontally CodeBlock-is-light-in-light-theme CodeBlock--language-txt" language="txt"><code><span class="CodeBlock--rows"><span class="CodeBlock--rows-content"><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">www.example.com</span></div></span></span></span></code></pre>{{</raw>}}

Instead of:


{{<raw>}}<pre class="CodeBlock CodeBlock-with-rows CodeBlock-scrolls-horizontally CodeBlock-is-light-in-light-theme CodeBlock--language-txt" language="txt"><code><span class="CodeBlock--rows"><span class="CodeBlock--rows-content"><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">www.example.com/some-particular-page.html</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">
</span></div></span></span></span></code></pre>{{</raw>}}

The solution is to use variables. Each wildcard corresponds to a variable when can be referenced in the forwarding address. The variables are represented by a $ followed by a number. To refer to the first wildcard you'd use $1, to refer to the second wildcard you'd use $2, and so on.

To fix the forwarding from the root to www in the above example, you could use the same pattern:


{{<raw>}}<pre class="CodeBlock CodeBlock-with-rows CodeBlock-scrolls-horizontally CodeBlock-is-light-in-light-theme CodeBlock--language-txt" language="txt"><code><span class="CodeBlock--rows"><span class="CodeBlock--rows-content"><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">example.com/*</span></div></span></span></span></code></pre>{{</raw>}}

You'd then set up the following URL for traffic to forward to:


{{<raw>}}<pre class="CodeBlock CodeBlock-with-rows CodeBlock-scrolls-horizontally CodeBlock-is-light-in-light-theme CodeBlock--language-txt" language="txt"><code><span class="CodeBlock--rows"><span class="CodeBlock--rows-content"><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">http://www.example.com/$1</span></div></span></span></span></code></pre>{{</raw>}}

In this case, if someone went to:


{{<raw>}}<pre class="CodeBlock CodeBlock-with-rows CodeBlock-scrolls-horizontally CodeBlock-is-light-in-light-theme CodeBlock--language-txt" language="txt"><code><span class="CodeBlock--rows"><span class="CodeBlock--rows-content"><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">example.com/some-particular-page.html</span></div></span></span></span></code></pre>{{</raw>}}

They'd be redirected to:


{{<raw>}}<pre class="CodeBlock CodeBlock-with-rows CodeBlock-scrolls-horizontally CodeBlock-is-light-in-light-theme CodeBlock--language-txt" language="txt"><code><span class="CodeBlock--rows"><span class="CodeBlock--rows-content"><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain"> http://www.example.com/some-particular-page.html</span></div></span></span></span></code></pre>{{</raw>}}

___

## Related resources

-   [Single Redirects](https://developers.cloudflare.com/rules/url-forwarding/single-redirects/)
-   [Bulk Redirects](https://developers.cloudflare.com/rules/url-forwarding/bulk-redirects/)
-   [Understanding and Configuring Cloudflare Page Rules (Page Rules Tutorial)](https://support.cloudflare.com/hc/en-us/articles/218411427-Understanding-and-Configuring-Cloudflare-Page-Rules-Page-Rules-Tutorial-)