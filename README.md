# DEV NOTES

## Install dev tools:
- documentation: <https://github.com/nvm-sh/nvm>
```sh
# ensure consistent local version of node and npm are used:
nvm use
# install npm packages:
npm install
```

## Serve site locally:
- documentation: <https://github.com/http-party/http-server#readme>
```sh
# use node to execute locally-installed http-server package:
npx http-server -p 8080
```

## Check locally-served site for broken links:
- fast, errors-only, limited details (no line numbers)
```sh
# use node to execute locally-installed http-server package:
npx http-server -p 8080

# use node to execute locally-installed linkinator package against local site:
npx linkinator http://127.0.0.1:8080 --recurse --verbosity error
```

## Check production site for broken links and save results to a local file:
- fast, errors-only, limited details (no line numbers)
- see package details: <https://github.com/JustinBeckwith/linkinator#readme>
```sh
# use node to execute locally-installed linkinator package against remote site:
npx linkinator https://cornermotorsales.com --recurse --verbosity error --format json &> linkinator-results.json
```

## Use W3C's online tool to check for broken links:
- slow, warnings and errors, complete details, unstructured results.
- see documentation: <https://validator.w3.org/checklink/docs/checklink.html>

```sh
# open a pre-configured URL in a browser:
xdg-open https://validator.w3.org/checklink?uri=https%3A%2F%2Fcornermotorsales.com%2F&summary=on&hide_type=all&recursive=on&depth=2&check=Check
```

## Install and use a python-based tool for link checking (on Ubuntu):
- medium-speed, errors-only, complete details, structured results (csv or json)
- see documentation: <https://wummel.github.io/linkchecker/man1/linkchecker.1.html>
```sh
# ensure pip is installed:
sudo apt update
sudo apt install python3-pip
# use pip to install LinkChecker:
sudo pip install LinkChecker
# use LinkChecker to check remote site:
linkchecker https://cornermotorsales.com --file-output=csv --check-extern
```

- alternatively, using Docker:

```
sudo docker run --rm -it -u $(id -u):$(id -g) --log-driver=none -a stdout -a stderr  linkchecker/linkchecker https://cornermotorsales.com --check-extern --no-status &> results.txt
```

## Validate HTML locally:

```sh
# use node to execute locally-installed http-server package:
npx http-server -p 8080

# crawl and validate local site:
npx site-validator http://localhost:8080 --local --verbose

# alternatively, validate a single page:
npx site-validator http://localhost:8080/ignitions --local --page --verbose

```
