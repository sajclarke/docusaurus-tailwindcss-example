# TailwindCSS in Docusaurus example

Use these 5 simple steps to setup TailwindCSS v3 in Docusaurus

## Step One - Setup Docusaurus

We'll get started by creating a default docusaurus setup using the following command:
`npx create-docusaurus@latest website classic`

## Step Two - Install TailwindCSS

Since Docusaurus leverages [ReactJS](www.reactjs.org), we'll use PostCSS and AutoPrefixer to manage the TailwindCSS configuration. We will do this by installing the necessary dependencies for setting up TailwindCSS using the following command:
`yarn add tailwindcss postcss autoprefixer`

As per the TailwindCSS docs, you'll need to create a `tailwind.config.js` file in order to initialize your configuration using the following command:
`npx tailwindcss init`

Open your `tailwind.config.js` file and edit it as follows:

```
module.exports = {
  content: ["./src/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

## Step Three - Setup Custom Plugin

We will now create a custom plugin so that TailwindCSS is included in the Docusaurus configuration options. We will do this by adding the `plugin` option to the `docusaurus.config.js` file using the following code:

```
 plugins: [
    async function myPlugin(context, options) {
      return {
        name: "docusaurus-tailwindcss",
        configurePostCss(postcssOptions) {
          // Appends TailwindCSS and AutoPrefixer.
          postcssOptions.plugins.push(require("tailwindcss"));
          postcssOptions.plugins.push(require("autoprefixer"));
          return postcssOptions;
        },
      };
    },
  ],
```

## Step Four - Load TailwindCSS

In order to actually load TailwindCSS with the custom CSS that Docusaurus utilizes by default, we will modify the `src/css/custom.css` file by including the following at the top of the file:

```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## Step Five - Test Locally

Now, let's test out our configuration so far by deploying the Docusaurus site locally (default on port `3000`) by running the following commands in the command line:

```
yarn clear
yarn start
```

Finally, we can test out TailwindCSS by modifying the homepage (`src/pages/index.js`) to replace JSX returned by the `HomepageHeader` function with the following:

```
<header className="bg-blue-500">
      <div className="container mx-auto text-center py-24">
        <h1 className="text-4xl font-bold text-white">{siteConfig.title}</h1>
        <p className="text-xl py-6 text-white">{siteConfig.tagline}</p>

        <div className="py-10">
          <Link
            className="bg-white rounded-md text-gray-500 px-4 py-2"
            to="/docs/intro"
          >
            Docusaurus Tutorial - 5min ⏱️
          </Link>
        </div>
      </div>
    </header>
```
