## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

### Features of Next.js

#### Create New NextJS Project

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
- Apply a font to the body tag in app/layout.tsx to have default base font for application.
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
- Use the **<Link>** component from **next/link**.
- Next uses **automatic code-splitting**. Code is split by route segments so pages become isolated and not dependent to load on other pages. Different than React SPA where browser loads all app code on inital load.
- Next prefetches the link routes in the background. Code for destination page already loaded in the background making routing page transitions near instant.

- Showing active navigation links achieved by using usePathname() hook from **next/navigation**.
- The component that uses it must be a Client Component since it uses a hook.
- Use example for how to use clxs and pathname to set active link styles from other links.

#### Database

- Next example uses **Vercel** for deployment and **PostgreSQL** for database (@vercel/postgres).
- You can use whatever database you'd like though.

- **Deploy project to Vercel**:

  - Create github repository for project code.
  - Create Vercel account.
  - Connect repository and deploy project.

- Vercel will automatically redeploy whenever you push changes to the main branch.

- **Create Postgres Database**:

  - During this process you will copy secrets and paste them in the .env file (file should be in gitignore).
  - Install Vercel Postgres SDK by runnning `npm i @vercel/postgres`.

- **Seed Database**:

  - The example for Next has a script to create and populate the database w/pre-created data.
  - The seed action is completed adding then running the seed script added to package.json.
  - Once the database is completed you can run SQL queries in Vercel interface.

#### Fetching Data

- Next allows you to create API endpoints using Route Handlers.
- Database queries can be done w/relational database by using SQL or something like Prisma.
- Write queries if you're creating API endpoints or using server components, you can query your database directly.

- **Fetch Data using Server Components**

  - Less expensive since fetching is happening on server side.
  - Less dangerouse for the same reason.
  - Can use async/await since server components support promises.
  - No need for additional API layer since you are requesting the the server from the server side.

- **Fetch Data using SQL**

  - SQL is industry standard for relational databases.
  - The NextJS example uses the Vercel Postgres SDK.
  - Can use promise combinators like Promise.all() or Promise.allSettled() to get performance gains on multiple requests by doing requests in parallel rather than sequential (waterfall).

#### Static and Dynamic Rendering

- **Static Rendering**:

Static rendering is best for pages with no data or data that is shared across users (static blog or product page). Not recommended for dashboard type pages with personalized data that is regularly updated.

- Data fetching and rendering happen on server side at build time (deployment), or revalidation.
- Results can be stored in a CDN (Content Delivery Network).
- When user visits your app, cached result is served.
- Benefits:

  - 1. Faster website
  - 2. Reduced server load
  - 3. Better SEO rankings.

- **Dynamic Rendering**:

Content is rendered on the server for each user at request time (when user visits the page).

- Benefits:

  - 1. Real time data
  - 2. User specific content.
  - 3. Request time information - like cookies, or URL search parameters

- NextJS has an API called **unstable_noStore** in its **next/cache** module that can be used inside a Server Component or data fetching function to opt out of static rendering.
- Suspense is used as a boundary between the static and dynamic parts of your route. (It doesn't doesn't itself make the component dynamic).
- So by adding it at the top of a function, it will change the function to be dynamically rendered.
- With dynamic rendering your app is only as good as your slowest data fetch.

#### Streaming

Streaming allows you to break down routes into smaller chunks and progressively stream them from the server to the client as they become ready.

- **Ways to Implement Streaming**:

1. At page level with loading.tsx file.
2. For specific components with <Suspense>

   - This is a special Next file built on top of Suspense.
   - If the page it's on is static it will show immediately.
   - You can interact with other elements of the page while it's showing.

- **Adding Loading Skeletons**:

Simplified version of the UI. Used as loading state.

- **Route Groups**:

Organize files into logical groups w/out affecting the URL path structure. The folder with parenthesis prevents that name from being included in URL path. So `/dashboard/(overview)/page.tsx` becomes `/dashboard`. Loading.tsx will only apply to the page in the route group.

- **Streaming a component**:

  - Wrap the component in the Suspense tag.
  - Give it a fallback prop pointing to a skeleton component.
  - Good for longest loading data component.

- **Grouping a component**:

  - For components you'd like to create a group stream for, create a wrapper component.
  - Create a skeleton component for the wrapper.
  - Wrap the wrapper component in Suspense element.
  - Give that suspense a fallback component to the skeleton.
  - Inside your component wrapper, fetch the data for each grouped item.

#### Partial Prerendering(experimental feature)

Static route shell is served and leaves holes for dynamic content that will load asynchronously. These async holes are streamed in parallel, reducing load time.

#### Adding Search and Pagination
