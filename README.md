<p align="center">
  <a href="http://runnerty.io">
    <img height="257" src="https://runnerty.io/assets/header/logo-stroked.png">
  </a>
  <p align="center">Smart Processes Management</p>
</p>

[![NPM version][npm-image]][npm-url] [![Downloads][downloads-image]][npm-url] [![Dependency Status][david-badge]][david-badge-url]
<a href="#badge">
<img alt="code style: prettier" src="https://img.shields.io/badge/code_style-prettier-ff69b4.svg">
</a>

# Mail notifier for [Runnerty]:

Email notification module with [ejs] template support.

### Installation:

Through NPM

```bash
npm i @runnerty/notifier-mail
```

You can also add modules to your project with [runnerty]

```bash
npx runnerty add @runnerty/notifier-mail
```

This command installs the module in your project, adds example configuration in your [config.json] and creates an example plan of use.

If you have installed [runnerty] globally you can include the module with this command:

```bash
runnerty add @runnerty/notifier-mail
```

### Configuration sample:

Add in [config.json]:

```json
{
  "notifiers": [
    {
      "id": "mail_default",
      "type": "@runnerty-notifier-mail",
      "disable": false,
      "from": "Runnerty <my@mail.com>",
      "transport": "smtps://my%40mail.com:mypass@smtp.mail.com/?pool=true",
      "templateDir": "/etc/runnerty/templates",
      "template": "alerts",
      "to": ["to@mail.com"],
      "ejsRender": true
    }
  ]
}
```

```json
{
  "notifiers": [
    {
      "id": "mail_default",
      "type": "@runnerty-notifier-mail",
      "disable": false,
      "from": "Runnerty <my@mail.com>",
      "to": ["NAME <to@mail.com>"],
      "transport": {
        "host": "smtp.mailhost.com",
        "port": 465,
        "secure": true,
        "auth": {
          "user": "USER_SAMPLE",
          "pass": "PASS_SAMPLE"
        }
      },
      "templateDir": "templates",
      "template": "template_one",
      "attachments": [
        {
          "filename": "runnerty.png",
          "path": "templates/imgs/runnerty.png",
          "cid": "cid_img_sample@runnerty.png"
        }
      ],
      "ejsRender": true,
      "maxConcurrents": 2,
      "minInterval": 25
    }
  ]
}
```

To use AWS SES [transport]:

```json
{
  "notifiers": [
    {
      "id": "mail_aws_ses_role",
      "type": "@runnerty-notifier-mail",
      "from": "Runnerty <hello@runnerty.io>",
      "to": ["Support <support@mail.com>"],
      "transport": {
        "service": "SES",
        "region": "us-east-1",
        "ses": {
          // optional extra arguments for SendRawEmail
          "Tags": [
            {
              "Name": "tag_name",
              "Value": "tag_value"
            }
          ]
        }
      },
      "templateDir": "templates",
      "template": "mail-notification",
      "ejsRender": true
    }
  ]
```

### Plan sample:

Add in [plan.json]:

```json
{
  "notifications": {
    "on_fail": [
      {
        "id": "mail_error",
        "subject": "ERROR - PROCESS @GV(PROCESS_ID) CHAIN @GV(CHAIN_ID)",
        "message": "CMD:<br> @GV(PROCESS_EXEC_COMMAND_EXECUTED)<br>ERROR:<br>@GV(PROCESS_EXEC_ERR_OUTPUT)"
      }
    ]
  }
}
```

[runnerty]: https://www.runnerty.io
[downloads-image]: https://img.shields.io/npm/dm/@runnerty/notifier-mail.svg
[npm-url]: https://www.npmjs.com/package/@runnerty/notifier-mail
[npm-image]: https://img.shields.io/npm/v/@runnerty/notifier-mail.svg
[david-badge]: https://david-dm.org/runnerty/notifier-mail.svg
[david-badge-url]: https://david-dm.org/runnerty/notifier-mail
[config.json]: http://docs.runnerty.io/config/
[plan.json]: http://docs.runnerty.io/plan/
[transport]: https://nodemailer.com/transports/ses/
[ejs]: https://ejs.co
