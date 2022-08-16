# Simple Repository with External Redirects

## Issues
- Redirect is not working in production as expected.
- Unique Deploy URL doesn't work as expected.

### Steps to Reproduce

- Clone this repository
- Run `ntl deploy --prod`

Output I Received

```shell
This folder isn't linked to a site yet
? What would you like to do? +  Create & configure a new site
? Team: keith-kevin99's team
Choose a unique site name (e.g. super-cool-site-by-keith-kevin99-yahoo-com-7564d.netlify.app) or leave it blank for a random name. You can update the site name later.
? Site name (optional): undefined

Site Created

Admin URL: https://app.netlify.com/sites/super-cool-site-by-keith-kevin99-yahoo-com-7564d
URL:       https://super-cool-site-by-keith-kevin99-yahoo-com-7564d.netlify.app
Site ID:   93f53f84-27c6-49f0-b342-6de3379bcdaa

Linked to super-cool-site-by-keith-kevin99-yahoo-com-7564d in /Users/kunal/Desktop/myfolder.nosync/oss/p-cli-test/with-redirects/.netlify/state.json
Please provide a publish directory (e.g. "public" or "dist" or "."):
/Users/kunal/Desktop/myfolder.nosync/oss/p-cli-test/with-redirects
? Publish directory /Users/kunal/Desktop/myfolder.nosync/oss/p-cli-test/with-redirects
Deploy path:        /Users/kunal/Desktop/myfolder.nosync/oss/p-cli-test/with-redirects
Configuration path: /Users/kunal/Desktop/myfolder.nosync/oss/p-cli-test/with-redirects/netlify.toml
Deploying to main site URL...
✔ Finished hashing
✔ CDN requesting 1 files
✔ Finished uploading 1 assets
✔ Deploy is live!

Logs:              https://app.netlify.com/sites/super-cool-site-by-keith-kevin99-yahoo-com-7564d/deploys/62fb8b0df2c0d31f7a8eecf7
Unique Deploy URL: https://62fb8b0df2c0d31f7a8eecf7--super-cool-site-by-keith-kevin99-yahoo-com-7564d.netlify.app
Website URL:       https://super-cool-site-by-keith-kevin99-yahoo-com-7564d.netlify.app
```

- Go to the Unique Deploy URL: `https://62fb8b0df2c0d31f7a8eecf7--super-cool-site-by-keith-kevin99-yahoo-com-7564d.netlify.app/`
    - See a "This site can’t be reached" or similar message in browser. **Unexpected Behaviour**
- Go to Website URL: `https://super-cool-site-by-keith-kevin99-yahoo-com-7564d.netlify.app/`.
    - See "Hi" on the page. As expected.
- Go to `https://super-cool-site-by-keith-kevin99-yahoo-com-7564d.netlify.app/test`.
    - See "This page isn’t working" or "HTTP ERROR 500" error **Unexpected Behaviour**
        - Should've gone to `https://www.netlify.com` as per the redirect rule specified.
    - Note: Redirect works in CLI
        - Run `ntl dev`
        - Go to `http://localhost:8888/test`. Be redirected to `netlify.com` as expected.



System Config

```
npx envinfo --system --binaries --npmPackages netlify-cli --npmGlobalPackages netlify-cli

  System:
    OS: macOS 12.4
    CPU: (8) arm64 Apple M1
    Memory: 322.84 MB / 16.00 GB
    Shell: 5.8.1 - /bin/zsh
  Binaries:
    Node: 16.15.1 - ~/.nvm/versions/node/v16.15.1/bin/node
    npm: 8.11.0 - ~/.nvm/versions/node/v16.15.1/bin/npm
    Watchman: 2022.08.08.00 - /opt/homebrew/bin/watchman
```