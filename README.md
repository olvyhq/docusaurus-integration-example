# Olvy Docusaurus Demo

This website is built using [Docusaurus 2](https://docusaurus.io/), a modern static website generator.

## Installing and Running Docusaurus

### Installation

```
$ yarn
```

### Local Development

```
$ yarn start
```

This command starts a local development server and opens up a browser window. Most changes are reflected live without having to restart the server.

## Integrating Olvy

1. Create a widget on the Olvy dashboard on [https://app.olvy.co/widgets/announcements](https://app.olvy.co/widgets/announcements). Customize it according to your needs. Decide the target element you want to use to open your widget and its selector.

   By default it is `#olvy-whats-new` which means Olvy will look for an element with where `id="olvy-whats-new"` to link to your widget.

2. First, let's add a "What's New" button to the Navbar. To do this, we've added the following in our `docusaurus.config.js` in themeConfig -> navbar -> items

```

themeConfig:
    /** @type {import('@docusaurus/preset-classic').ThemeConfig} */
    ({
      navbar: {
        title: "My Site",
        logo: {
          alt: "My Site Logo",
          src: "img/logo.svg",
        },
        items: [
          ...
          {
            href: "#",
            id: "olvy-whats-new",
            docId: "olvy",
            position: "left",
            label: "What's New",
          },
          ...
        ],
      },
      ...

```

Now you'll be able to see a What's New link on Docusaurus site navbar.

**NOTE: The id of the navigation item here is `olvy-whats-new`. You will need it to the Target Element selector you've added for your Widget on Olvy Dashboard. (in step 1 above)**

3. Next let's add the Olvy script. In `docusaurus.config.js` add the following scripts in the `script` key

```

const config = {
  title: "Olvy Demo",
  tagline: "Integrating Olvy script in Docusaurus",
  url: "https://your-docusaurus-test-site.com",
  baseUrl: "/",

  ...

  scripts: [
    {
      src: "/olvyConfig.js",
    },
    {
      src: "https://app.olvy.co/scriptV2.js",
      async: true,
    },
  ],
};

module.exports = config;

```

The `olvyConfig.js` file we've referenced above doesn't exist yet. So in the next step let's create it.

4. Inside the `static` directory of your Docusaurus site create a new file called `olvyConfig.js` and paste the following inside it.

```
window.OlvyConfig = {
  workspaceAlias: "<your-subdomain>",
};
```

Replace `<your-subdomain>` with your real subdomain. For example, if your Olvy releases page is on acme.olvy.co then this file for you would look like this.

```
window.OlvyConfig = {
  workspaceAlias: "acme",
};
```

That's it. If you reload your site now you'll be able to
