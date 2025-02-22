---
pcx_content_type: troubleshooting
title: WordPress Loopback error
weight: 0
---

# WordPress Loopback error

{{<render file="_wordpress-loopback-definition">}}
<br/>

In **WordPress 6.0.1** with no additional plugins or themes, the page generated the following 3 requests:

| Error | Method | URI | User-Agent |
| ---- | ---- | ---- | ---- |
| The REST API encountered an unexpected result | `GET` | `/wp-json/wp/v2/types/post` | WordPress/6.0.1 < site-hostname > |
| Your site could not complete a loopback request | `GET` | `/` | WordPress/6.0.1 < site-hostname > |
| Your site could not complete a loopback request | `POST` | `/wp-cron.php` | WordPress/6.0.1 < site-hostname > |

These requests all come from the origin IP and not a Cloud service.  As a result, Cloudflare does not have an easy way to add these types of requests to verified bots. 

When these requests are blocked, WordPress’s block editor screen, Cron events, and automated tests that third-party themes and plugins use cannot function.

Many different WordPress components perform different loopback tests beyond the original one, making it a complex problem to create exceptions for. 

### Resolution

Enterprise customers can [write an allow rule](/firewall/cf-dashboard/create-edit-delete-rules/#create-a-firewall-rule) for their origin IP to fix the issue. 

Self-serve customers can turn off Super Bot Fight Mode or edit `/etc/hosts` file to have loopback requests resolve locally. Refer to this guide on [how to fix WordPress Loopback errors](https://codeopolis.com/posts/wordpress-loopback-error/). 

{{<Aside type="note" header="Note:">}}

Cloudflare Support cannot assist with the host's file configuration changes or other specific server configurations.

{{</Aside>}}