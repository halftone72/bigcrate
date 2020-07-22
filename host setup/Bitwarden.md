# Bitwarden Client and enwarden

Download envwarden 
`wget https://raw.githubusercontent.com/envwarden/envwarden/master/envwarden`

make it executable and reachable
`chmod +x envwarden && sudo cp envwarden /usr/local/bin`

Download and install the bw CLI and jq version 1.6 and above!
`sudo snap install bw && sudo apt install jq `
 
 Extract secrets to .env
 
`envwarden -s bigcrate --dotenv > .env`

---

# Resources and Notes 

https://github.com/envwarden/envwarden

https://bitwarden.com

https://blog.gingerlime.com/2018/introducing-envwarden-manage-your-server-secrets-with-bitwarden/

### Adding secrets to Bitwarden

![](https://raw.githubusercontent.com/envwarden/envwarden/master/assets/bitwarden-item-screenshot.png "bitwarden item for envwarden")

* Create an item you'd like to use for storing secrets.
  Try to make its name unique, so envwarden can easily find it
  and not any unrelated items.
  You might want to define the name based on your server or environment
  (e.g. `staging`, `development`, `production`)
* Add custom fields for each secure environment variable you need
  (fields can be text, hidden or boolean)
* You can add as many fields as you need, and you can also create
  multiple items, as long as they match the same search term
  (their secrets would be combined)
* You can also copy attachments on the searched items to a destination folder
* You should use separate logins for each environment, and ideally limit server
  access to only the secrets it needs, but it's up to you how to manage it

### Getting secrets onto your server

* You can store your Bitwarden login credentials inside `~/.envwarden` if you wish
* Otherwise, you would be prompted for your email and password (or both)
* You can then use `eval $(envwarden)` to get your secrets `export`ed to your environment
* Alternatively, you can output your secrets into an `.env` file using `envwarden --dotenv`

```
Usage: envwarden [--help] [--search] [--dotenv] [--copy]

To export environment variables, use: `eval $(envwarden)`
To create an .env file, use: `envwarden --dotenv > .env`

Options:
    -h --help
    -s --search <keyword> (optional) define the search term for bitwarden items (defaults to 'envwarden')
    -d --dotenv (optional) outputs to stdout in .env format
    -k --dotenv-docker (optional) outputs secrets to stdout in a "docker-friendly" .env format (no quotes)
    -c --copy <destination folder> (optional) copies all attachments on the item to a folder

You can use ~/.envwarden to store your credentials (just email, or email:password)
```
