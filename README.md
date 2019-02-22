An empty web site hosted by Firebase to perform redirects for the
old flutter.io domain.

There's no CI set up for this project; it's intended to be used
for only a few days while we set up DNS redirection for flutter.io.

You can deploy this using

```
firebase login
firebase deploy
```

Assuming that you have access permissions to the
`sweltering-fire-2088` Firebase project.

## Verifying that we redirect correctly

The `old-sitemap.txt` file has a list of over a 100 URLs that should redirect
properly. This is in no way exhaustive, especially since it includes
URLs with fragments (like 
`flutter.dev/docs/development/ui/layout#material-apps`). But it's a good
sample.

You can run the `linkcheck` tool to make sure all those URLs redirect
properly.

1. Install `linkcheck` with `pub global activate linkcheck`
2. Start the local server with `firebase serve --port=3474` 
   (or `superstatic --port=3474` if you don't have permissions to the 
   Firebase project)
3. Run the link checker with `linkcheck -i old-sitemap.txt -e`
   * This tries to access all URLs listed in `old-sitemap.txt`
   * It follows redirects, even when they're external (`-e`)

When successful, no broken links will be reported. The tool will still report
one error:

> Error. Couldn't connect or find any links. Have you started the server?

This is okay. The tool is confused that there are no pages at the domain
we are testing, just redirects.
