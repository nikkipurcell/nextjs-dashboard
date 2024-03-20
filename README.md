## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

### Features of Next.js

#### Create New Next Project

- Use `create-next-app` to create new project.
- The **app/lib** folder is where mock data, type definitions, functions and requests can live.
- Written in TypeScript.
- To install project packages, run `npm i`.
- Start the development server on port 3000, run `npm run dev`.

#### CSS

- CSS files contained in **app/ui** folder.
- Global css file can be imported to top level component **app/layout.tsx**.
- Can choose a CSS solution:
  - **Tailwind CSS** is default choice - framework where you write utility classes in your file.
  - **CSS Modules** is another option - scope CSS to component using unique class names.
  - **CSS-in-JS** is another option (styled-components, emotion, etc).
  - **SASS** is another option (.css and .scss files).
- **clsx** is a library that lets you toggle class names that have different css styles.

#### Font and Images

- Use **next/font** module to automatically optimize fonts.
  - How? - downloads at build time, hosts with other static assets.
  - Can use Google font - **next/font/google**
  - May have to specify a subset for google fonts.
- Apply a font to the body tag in app/layout to have default base font for application.
- Add antialiased to the body from Tailwind CSS (if using it).

- Use **next/image** component to automatically optimize images.
  - Static assets like images live in the **public** folder.
  - Can use **<Image>** component from next/images and apply an src value to point to image.
  - Apply width and height to avoid layout shift.
  - Class hidden will remove image from DOM on mobile.
  - md:block will show image on desktop screens.

#### Layouts and Pages

- Next uses file-system routing where folders create the **nested routes**.
- **page.tsx** is file that exports React component and required for route to be accessible.
- app/page.tsx is the home page associated with the root page at /.

- For dashboard pages in Next, layout.tsx page is a special file that is used to share UI between multiple pages.
- The component in this file you create would be named Layout.
- Inside you can use components you'd like to share on all child pages (example a SideNav).
- Layout components use partial rendering - only page components update, layout ones won't re-render.
  - So when you change navigation for child pages only the child sections of the page are rendered.
- Root layout file is required. (any UI used will be shared with ALL pages of app).
- Good if you need to add to the html or body tags.

#### Navigation

- Navigation needs optimization so that the entire page doesn't re-render when you click anchor tag.
- Use the link component from **next/link**.
- Next uses **automatic code-splitting**. Code is split by route segments so pages become isolated and not dependent to load on other pages. Different than React SPA where browser loads all app code on inital load.
- Next prefetches the link routes in the background. Code for destination page already loaded in the background making routing page transitions near instant.
