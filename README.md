# Auth0 - GitHub Source Control Integration

Unused features such as custom database tables have been removed.  The original repo is located: https://github.com/auth0-samples/github-source-control-integration

Under [Extensions](https://manage.auth0.com/#/extensions) you'll find the GitHub Deploy extension which allows you to manage your Datbase Connections and Rules in a GitHub repository.

## Deploying Pages

For Hosted Pages you'll created an html file and a json file (for enabled/disabled status) under `pages`. Supported hosted pages:


```
error_page
guardian_multifactor
login
password_reset
```

##  Deploying Rules

For rules you'll create 1 JavasSript file for every rule you want to deploy under the `rules` directory. Eg: `rules/set-country.js`.

When creating the rule the name in Auth0 will be set to `set-country`. If you plan to use Source Control integration for an existing account, make sure you rename your rules in Auth0 first to the same name of the files you'll deploy to this directory.

In addition to that you might want to control the rule **order**, **status** (enabled/disabled) and **stage** (`login_success`, `login_failure`, `user_registration`).

These can be controlled by creating a JSON file next to your Javascript file. Eg:

**set-country.js**

```js
function (user, context, callback) {
	if (context.request.geoip) {
		user.country = context.request.geoip.country_name;
	}

	callback(null, user, context);
}
```

**set-country.json**

```json
{
  "enabled": false,
  "order": 15,
  "stage": "login_success"
}
```

> Note:
>  - Having multiple rules with the same order is not allowed. Make sure you don't have any collisions.

A few examples can be found [here](rules).
