This is a starter template for [Learn Next.js](https://nextjs.org/learn).

# This is the page with the Next.js

# Navigating Pages Next JS
* Pages are associated with a route based on their `filename`
* for example `pages/index.js` is associated with the `/` route.
* `pages/posts/first-post.js` is associated with the route `/posts/first-post`
* Thus basically you just have to write a components in the first post and `export default funcname (){}`
* In a way, this is similar to building websites using HTML or PHP files. Instead of writing HTML you write JSX and use React Components.


## React Fragments
* [React Fragments](https://reactjs.org/docs/fragments.html)
* Helps with returning multiple items in the JSX without creating a new DOM element
    * Shorthand syntax `<><ChildA /><ChildB /><ChildC /></>`
    * Usual Way syntax `<React.Fragment><ChildA /><ChildB /><ChildC /></React.Fragment>`


## Link Component
* When Linking between pages on websites you use the `<a>` tag
* In Next.js you use the `Link` Component from `next/link` to wrap the `<a>` tag. `<Link>` allows you to do client side navigation to different pages in the application
* `import Link from 'next/link'` for using the links
    * Usual H1 tag
        * <h1 className="title">
        Learn <a href="https://nextjs.org">Next.js!</a>
        </h1>

    * Now with Link
        * `<h1 className="title">
            Read{' '} `Adds an empty space used to divide text over multiple lines`
                <Link href="/posts/first-post">
                    <a>this page!</a>
                </Link>
            </h1>`
        * This Link is similar to putting <a></a> but without the href

## Client Side Navigation
* The `Link` component enables client side navigation between the two pages in the same Next.js app
* THe Navigation happens with Javascript which makes in faster
* [Client Side Navigation](https://nextjs.org/learn/basics/navigate-between-pages/client-side)
* Here’s a simple way you can verify it:

    * Use the browser’s developer tools to change the background CSS property of <html> to yellow.
    * Click on the links to go back and forth between the two pages.
    * You’ll see that the yellow background persists between page transitions.
* `Next.js` does code splitting automatically so each page loads what's necessary for that page
* This ensures the homepage loads quickly even if you have hundred of pages
* Only the page you requested become loaded. Hence if a certain page throws an error everywhere else still works 
* Furthermore, in a production build of Next.js, whenever Link components appear in the browser’s viewport, Next.js automatically prefetches the code for the linked page in the background. 
    #### Summary
    * Next.js automatically optimizes your application for the best performance by code splitting, client-side navigation, and prefetching (in production).

    * You create routes as files under pages and use the built-in Link component. No routing libraries are required.

    * You can learn more about the Link component in the API reference for next/link and routing in general in the routing documentation.

### Note for loading the app
* `npm run start` is only for production
* `npm run dev`
* https://nextjs.org/learn/basics/create-nextjs-app/setup




## Assets, Metadata, Css
* https://nextjs.org/learn/basics/assets-metadata-css
* Now we will look at how Next JS handles static assets like images, page metadata like the `<title>` tag
* assets are stored in `public` directory at the toplevel
* files can be refered to from the root here
* The public directory is also useful for robots.txt, Google Site Verification, and any other static assets. Check out the documentation for Static File Serving to learn more.

    ### Curl
    * `curl https://github.com/vercel/next-learn-starter/blob/master/basics-final/public/images/profile.jpg -o profile.jpg` for the profile pic
    * https://linuxconfig.org/download-file-from-url-on-linux-using-command-line

### The Images were Unoptimized in Regular HTML
* <img src="/images/profile.jpg" alt="Your Name"/>
* You had to manually handle responsiveness
* optimizing images with a third-party tool or library
* Only loading images when they enter the viewport
* Instead Next.js provides an `Image` component out of the box to handle this for you

### The Image COmponent and Image Optimization
* `next/image` is an extension of the HTML `<img>` in the modern web
* Next.js has support for Image Optimization by default
* It allows for reszing, optimizing and serving images in modern formats and browsers 
* Even if the image source is external Automatic Image Optimization takes place


### Using the Image COmponent
* Instead of optimizing is done at build time , Next.js optimizes images on-demand as users request them
* Images are lazy loaded by default. That means your page speed isn't penalized for images outside the viewport. Images load as they are scrolled into viewport.
* [Layout shifts](https://web.dev/cls/) when an element that is visible within the viewport changes its start position between two frames
* [Core Web Vital](https://nextjs.org/learn/basics/assets-metadata-css/assets) for loading stuff memory


## MetaData
* Modifying the `<title>` or `<head>`
* `<Head>` is a React component built in Next.js
* For customize `<html>` tag for example `lang` attribute you can do so by creating `pages/_document.js`
* [Custom Document](https://nextjs.org/docs/advanced-features/custom-document)

* For the CSS styling
    * `styled-jsx`which is a "CSS-in-JS" library
    * lets you write CSS within a React component
    * the CSS styles will be scoped (meaning other components are not affected)
    * Next.js has built-in support for styled-jsx, but you can also use other popular CSS-in-JS libraries such as styled-components or emotion.
    *Using CSS and Sass is supported as well as Tailwind css

### Layout Component
* this will be shared across all pages
* create a top-level directory called `componets` and then make `layout.js`
* it has the props `children` and `home`
* Layout({children, home}) # home is a boolean it does not have to be hoem
* Lets say I am building a component
    * function Home(){
        return (
            <>
                <Layout home> Whatever here...</Layout>
            </>
            )
    }

* What is it?
    * [Layout COmponents](https://www.gatsbyjs.com/docs/how-to/routing/layout-components/)
    * Layout components are for sections of your site that you want to share across multiple pages. `For example, Gatsby sites will commonly have a layout component with a shared header and footer.` `Other common things to add to layouts are a sidebar and/or navigation menu`. On this page for example, the header at the top is part of gatsbyjs.com’s layout component.

#### Component Level CSS
* [CSS module support](https://nextjs.org/docs/basic-features/built-in-css-support#adding-component-level-css)
* Next.js supports CSS Modules using the `[name].module.css` file naming convention.
* Allows the creation of the same CSS modules without worrying about collision
* `import styles from './Button.module.css'`
    * `className={styles.error}`
    * note the module does not have to be name styles
* Note regular css links can be used,
* Note that the `div` rendered by the layout automatically has a class name `layout_container__....`
* CSS modules automatically generate unique class names
* styled components do not have build in support hence we did the module stuff

#### GLobal Styles
* [Global Styles](https://nextjs.org/learn/basics/assets-metadata-css/global-styles)
* CSS modules are useful for component level styles. But what if you want some css to be loaded by every page
* To load a global CSS file create a file called `pages/_app.js`
* `export default function App({ Component, pageProps }) {
  return <Component {...pageProps} />
}`
* This `App component` is the top-level component which will be common across all the different pages. You can use this App component to keep state when navigating between pages, for example.
* restart server after doing this `npm run dev`

##### Adding the GLobal CSS
* In ext js you can add the global css via `pages/_app.js`. You `cannot` import global CSS anywhere else
* The Reason is that global CSS can't be imported outside `pages/_app.js` is that global CSS affects all elements on the page
* If you were to navigate from the homepage to the /posts/first-post page, global styles from the homepage would affect /posts/first-post unintentionally.
* You can place the global CSS file anywhere and use any name. So let’s do the following:
    * Create a top-level styles directory and create global.css inside.
    * Add the following content to `styles/global.css`. It resets some styles and changes the color of the a tag:
    * import it into `pages/_app.js` (THIS IS HOW IT LOADS)

### Polishing
* [https://nextjs.org/learn/basics/assets-metadata-css/polishing-layout]()
* Here’s what’s new: meta tags (like og:image), which are used to describe a page's content
* Boolean home prop which will adjust the size of the title and the image
“Back to home” link at the bottom if home is false
* Added images with next/image, which are preloaded with the priority attribute