# strapi-provider-email-amazon-ses-sdk

Amazon Simple Email Service provider based on AWS SDK for Strapi email plugin.

## Benefits

- You can send emails from your Amazon Simple Email Service external provider
- Uses official AWS SDK for JavaScript http://aws.amazon.com/javascript

## Version

- Strapi 3.0.0-beta support

## Installation

`npm install strapi-provider-email-ses`

## Programmatic usage

```javascript
"use strict";

/**
 * `Emails` service.
 */

module.exports = {
  send: async () => {
    const options = {
      to: "somebody@example.com",
      from: "sender@example.com",
      replyTo: "no-reply@example.com",
      subject: "Use strapi email provider successfully",
      text: "Hello world!",
      html: "Hello world!"
    };

    // Retrieve provider configuration.
    const config = await strapi
      .store({
        environment: strapi.config.environment,
        type: "plugin",
        name: "email"
      })
      .get({ key: "provider" });

    // Verify if the file email is enable.
    if (config.enabled === false) {
      strapi.log.error("Email is disabled");
      return false;
    }

    return await strapi.plugins.email.services.email.send(options, config);
  }
};
```

## Configure the plugin

- Open Strapi admin panel
- Click on Plugins in the left menu
- Click on the cog button on the Email plugin line
- Create Amazon SES username (if you did not do that yet https://docs.aws.amazon.com/ses/latest/DeveloperGuide/sign-up-for-aws.html)
  - AWS SES Default Reply-To - default reply-to email address
  - AWS Access Key ID - your AWS SES Access Key - you will need to create a IAM user with SES write access
  - AWS Secret Access Key
  - AWS Region - SES region
  - AWS SES Configuration Set - write "none" if not configured

## Resources

- [MIT License](LICENSE.md)

## Links

- [Package homepage](https://github.com/bashconsole/strapi-provider-email-amazon-ses-sdk)
- [Strapi website](http://strapi.io/)
