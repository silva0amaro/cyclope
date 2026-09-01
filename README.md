# Cyclope website

Two static pages and their assets. No build step and no dependencies: every
file here is served exactly as it is.

```
index.html      the presentation page, with the enquiry form
guide.html      the field guide
assets/         screenshots, stylesheets and the icon
.nojekyll       tells GitHub Pages to serve the files unprocessed
```

## Publishing on GitHub Pages

1. Create a repository and copy these files into its root.
2. Push to the default branch.
3. In the repository, open **Settings -> Pages**, choose **Deploy from a
   branch**, pick that branch and the `/ (root)` folder, and save.
4. The site appears at `https://<user>.github.io/<repository>/` within a
   minute or two.

For a domain of your own, add a `CNAME` file containing the domain and point
the domain's DNS at GitHub Pages.

## The enquiry form

GitHub Pages serves files; it cannot run anything. The form therefore works in
one of two ways, chosen by the `ENDPOINT` constant at the top of the script at
the end of `index.html`.

**Left empty, as it ships.** The form checks the answers and then opens the
visitor's own mail program with the message already written. Nothing is sent
anywhere else and no account is needed — but the address becomes visible in
the visitor's mail window, and someone with no mail program set up cannot
send.

**Set to a form service's endpoint.** The message is posted straight to that
service and the address is never shown. Any service accepting a JSON `POST`
will do; the fields sent are `name`, `email`, `kit` and `message`. Note that
the enquiry then passes through that company.

### What stops automated submissions

Three checks, none of which asks anything of a person:

- **An empty field they cannot see.** Automated submitters fill in every field
  they find, including one hidden off-screen. A submission with it filled in
  is answered as though it had succeeded, so there is nothing to learn from
  and nothing to retry against.
- **A minimum of four seconds.** Faster than anyone can read the form.
- **A sum written in words**, made fresh on every load, so the answer is not
  in the page source and cannot be memorised from a previous visit.

This stops the automated traffic that submits every form it meets, which is
almost all of it. It will not stop somebody who decides to target this page
specifically; nothing that runs entirely in the visitor's browser can. If the
form is ever abused in earnest, the answer is a service that checks
submissions on its own side.

The address itself is assembled by the script rather than written in the page,
so an address harvester reading the source finds nothing to collect.

## Before it goes public

- The sharing preview (`og:image`) uses a relative path, which some services
  will not follow. Once the address is known, change the `og:image` tag in
  both pages to the full `https://.../assets/observatory.jpg`.
- The screenshots are of the working application. Regenerate them when the
  interface changes.
