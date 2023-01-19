# Best practices

## Set your personal access token as a variable

Your Specify personal access token should always be private. We highly recommend you to set it in a private variable or in a `.env` variable.

### Using an .env variable in a config file in JavaScript

{% code title=".env" %}
```bash
SPECIFY_TOKEN=ab83f8f49f5c65456c7b1fe70efbc804aa08f87150214aa984d4125945ed8283bash
```
{% endcode %}

```javascript
const path = require('path');
const envFile = '.env';
require('dotenv').config({ path: path.resolve(process.cwd(), envFile) });

module.exports = {
  repository: '@workspace/repository',
  personalAccessToken: process.env.SPECIFY_TOKEN,
  rules: [],
};
```

### Using a variable in a flag with the CLI

Set your personal access token as an environment variable and interpolate it in the CLI wit [the flag `-p`](https://specify.gitbook.io/specify-documentation/usage/cli#p-personal-access-token).

```bash
specify pull -p $SPECIFY_TOKEN
```

{% hint style="info" %}
You can use this method to sync Specify with git repositories in [GitLab](https://specifyapp.com/blog/specify-to-gitlab#creating-the-merge-request) or [GitHub](https://specifyapp.com/blog/how-to-pull-design-tokens-from-several-specify-repositories-on-github#how-to-use-this-workflow-in-github).
{% endhint %}
