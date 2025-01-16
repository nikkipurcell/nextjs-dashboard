## Next.js App Router Course - Starter

This is the Next.js App Router Course. It is from the Next.js learning section of the website. It introduces the featuers of Next.js in a beginner course (2024). This includes CSS, Fonts, Images, Layouts, Pages, Database, Fetching Data, Static and Dynamic Rendering, Streaming, Partial Prerendering, Search and Pagination, Mutating Data, Handling Errors, Improving Accessibility, Authentication and Metadata.

![Next.js Official Training Course](next-training.jpg)

### Project tools used:

- [Next.js Training Course](https://nextjs.org/learn) on the Next.js Website.
- Language: TypeScript (.tsx files)
- Type Definition: [Prisma](https://www.prisma.io/) (suggested)
- CSS: [Tailwind](https://tailwindcss.com/), [clsx](https://www.npmjs.com/package/clsx) (toggle classnames)
- Deployment: [Vercel](https://vercel.com/nikkis-projects-72ca6090/nextjs-dashboard)
- Database: Postgres (setup on Vercel website above)
- Authentication: [NextAuth.js](https://authjs.dev/reference/nextjs)
- Form Validation: [Zod](https://zod.dev/)
- Local Hosting: http://localhost:3000/

### Next.js Modules include:

- next/font,
- next/image,
- next/link,
- next/navigation,
- next/cache

#### How To Create A New NextJS Project

- Use `create-next-app` to create new project.
- Written in TypeScript.
- To install project packages, run `npm i`.
- Start the development server on port 3000, run `npm run dev`.
- This will open open http://localhost:3000/

#### Repo Architecture

- **config** files -> at root, webpack, babel, etc are abstracted away for simplicity
- **public** folder -> contains image files
- **scripts** folder -> contains any js scripts (like seeding postgres database)
- **app** folder -> contains all react files
- **app/page.tsx** -> home page associated with root at /.
- **app/layout.tsx** -> contains html and body tags and imports global css file.
- **app/ui** -> contains all CSS files, fonts and reusable components.
- **app/lib** -> contains mock data, type definitions, functions and requests.
- **app/myfirstroute** -> A nested route app/myfirstroute.
- **app/myfirstroute/layout.tsx** -> Shared components for base route and any sub-routes.

#### Placeholder Data

Use placeholder data in JSON format or as JS objects:

```
const invoices = [
  {
    customer_id: customers[0].id,
    amount: 15795,
    status: 'pending',
    date: '2022-12-06',
  },
  {
    customer_id: customers[1].id,
    amount: 20348,
    status: 'pending',
    date: '2022-11-14',
  },
  // ...
];
```

### Next Training Topics:

#### CSS

- Folder: **app/ui** - CSS files are contained here.
- File: **global.css** -
- File: **app/layout.tsx** - Global css can be imported to top level component in this file.
- Choose any CSS solution:
  - **Tailwind CSS** is default choice - framework where you write utility classes in your file.
  - **CSS Modules** is another option - scope CSS to component using unique class names.
  - **CSS-in-JS** is another option (styled-components, emotion, etc).
  - **SASS** is another option (.css and .scss files).
- **clsx** is a library that lets you toggle classnames that have different css styles.

#### Fonts

**next/font** module: optimizes fonts to help prevent layout shift.

- Create file called **fonts.ts**
- Can use Google font - **next/font/google**
- May have to specify a subset for google fonts.
- Apply a font to the body tag in app/layout.tsx to have default base font for application.
- Add antialiased to the body from Tailwind CSS (if using it).

- Benefits: Performance -> Fonts are downloaded at build time and hosted w/static assets.

#### Images

**next/image** module: uses the Image component to optimize images.

- Image component should have an src value pointing to image in the public folder.
- Include width and height to prevent layout shift.
- Use a classname as needed.
- Include alt text for SEO.

To toggle between a desktop image and a mobile image:

- Add desktop Image with className="hidden md:block":
  - when you want to show desktop image and hide the mobile image.
- Add mobile Image with className="block md:hidden":

  - when you want to show mobile image but hide the desktop image.

- Benefits: Performance -> The module automatically optimizes images for responsiveness, devices, layout shift and lazy loading.

#### Layouts and Pages

Next uses file-system routing where folders create the **nested routes**.

- **page.tsx** is file that exports React component and required for route to be accessible.

  - Ex: **app/page.tsx** is the home page associated with the root page at /.

- Layout file page is a special file that is used to share UI between multiple pages.

  - Always located in the same root folder as a page.tsx.
  - Root layout file **app/layout.tsx** is required. (any UI used will be shared with ALL pages of app).
  - Root layout file contains html and body tags.
  - Other layout files can use components you'd like to share on all child pages (example a SideNav).
  - Layout components use partial rendering - only page components update, layout ones won't re-render.
  - So when you change navigation for child pages only the child sections of the page are rendered.

- Benefits: **PARTIAL RENDERING** -> Layouts allow so that on navigation, only page components update while layout won't re-render.

#### Navigation

**next/link** module: uses the Link component to optimize navigation.

- Add key, href, classname and children to Link component.

- Benefits: Entire page won't re-render when you click anchor tag.
  - **Automatic code-splitting** -> Code is split by route segments so pages become isolated and not dependent to load on other pages. _Different than React SPA where browser loads all app code on inital load_.
  - **Prefetching** -> Next prefetches the link routes in the background. Code for destination page already loaded in the background making routing page transitions near instant.

**next/navigation** modue: used to show active links using **usePathname()** hook.

- Since it's a hook, component is required to be a client component.
- **clxs** library can be used to conditionally apply class names for active links. _Using link.href and pathname_.

#### Database

Next example uses **Vercel** for deployment and **PostgreSQL** for database (@vercel/postgres). You can use whatever database you'd like though.

- **Pre-requisites**:

  - Create Github repo for your project.
  - Create a Vercel account.

- **Deploy project to Vercel**:

  - Import the Github repo on Vercel website.
  - Name your project.
  - Click Deploy.

Vercel will automatically redeploy whenever you push changes to the main branch.

- **Create Postgres Database**:

  - Create, name and select region for your database.
  - Copy secrets from .env.locals tab and paste them in .env.example file. Rename to .env.
  - Go to .gitignore and and add .env to prevent secrets from being exposed in Github.
  - Install Vercel Postgres SDK by runnning `npm i @vercel/postgres`.

- **Seed Database**:

  - The example for Next has a script to create and populate the database w/pre-created data.
  - Add the seed script to package.json so you can run it.
  - Run `npm run seed`.
  - Once the database is completed you can run SQL queries in Vercel interface.

#### Fetching Data

- Next allows you to create API endpoints using Route Handlers.
- Database queries can be done w/relational database by using SQL or something like Prisma.
- Write queries if you're creating API endpoints or using server components, you can query your database directly.

- **Fetch Data using Server Components**

  - Less expensive since fetching is happening on server side.
  - Less dangerouse for the same reason.
  - Can use async/await since server components support promises.
  - No need for additional API layer since you are requesting the server from the server side.

- **Fetch Data using SQL**

  - SQL is industry standard for relational databases.
  - The NextJS example uses the Vercel Postgres SDK.
  - Can use promise combinators like Promise.all() or Promise.allSettled() to get performance gains on multiple requests by doing requests in parallel rather than sequential (waterfall).

#### Static Rendering

Static rendering is best for pages with no data or data that is shared across users (static blog or product page). Not recommended for dashboard type pages with personalized data that is regularly updated.

- What is it?:

  - Data fetching and rendering happen on server side at build time (deployment), or revalidation (purging data cache and re-fetching latest data).
  - Results can be stored in a CDN (Content Delivery Network).
  - When user visits your app, cached result is served.

- Benefits:

  - Faster website
  - Reduced server load
  - Better SEO rankings.

#### Dynamic Rendering

- What is it?:

  - Content is rendered on the server for each user at request time (when user visits the page).
  - With dynamic rendering your app is only as good as your slowest data fetch.

- Benefits:

  - Real time data
  - User specific content.
  - Request time information - like cookies, or URL search parameters

- Differentiate between static and dynamic rendering:

  - NextJS has an API called **unstable_noStore** in its **next/cache** module that can be used inside a Server Component or data fetching function to opt out of static rendering.
  - Suspense is used as a boundary between the static and dynamic parts of your route. (It doesn't itself make the entire component dynamic, just the parts wrapped in Suspense).

#### Streaming

When parts of your application are dynamic, slow data fetches can affect performance. Streaming (data transfer technique) can help prevent slow data requests from blocking your whole page.

Streaming allows you to break down routes into smaller "chunks" and progressively stream them from the server to the client as they become ready.

- **Two Ways to Implement Streaming**:

  - At page level with **loading.tsx** file.
  - For specific components with the **Suspense** wrapper component.

Streaming a whole page with loading.tsx:

- A special file built on top of Suspense that allows you to create fallback UI to show as replacement while page content loads.
- Any static content will load immediately while dynamic content loads.
- Improve the UI experience by using Loading Skeletons. These are simplified version of the UI used as loading state.
- Loading skeleton will apply to sub route pages. To prevent that use route groups.

- **Route Groups**:

  - This is a way to apply loading state to a part of a route rather than the whole page.
  - Organize files into logical groups w/out affecting the URL path structure. The folder with parenthesis prevents that name from being included in URL path. So `/dashboard/(overview)/page.tsx` becomes `/dashboard`. Loading.tsx will only apply to the page in the route group.

Streaming a component:

- Wrap the component in the Suspense tag.
- Give it a fallback prop pointing to a skeleton component.
- Good for longest loading data component.

- **Grouping a component**:

  - Good pattern for when you want multiple components to load in at the same time.
  - For components you'd like to create a group stream for, create a wrapper component.
  - Create a skeleton component for the wrapper.
  - Wrap the wrapper component in Suspense element.
  - Give that suspense a fallback component to the skeleton.
  - Inside your component wrapper, fetch the data for each grouped item.

#### Partial Prerendering(experimental feature)

Static route shell is served and leaves holes for dynamic content that will load asynchronously. These async holes are streamed in parallel, reducing load time.

#### Adding Search

To implement search using URL search params:

- Capture users input.
- Update URL w/seach params
- Keep URL in sync with input field.
- Update table to reflect the search query.

To do this we use next.js client hooks:

- **useSearchParams** - to access params of the current URL.
- **usePathname** - lets you read the current URL's pathname.
- **useRouter** - enables navigation between routes w/in client components.

To optimize the search function requests we can use debouncing.
**Debouncing** is a programming practice that limits the rate at which a function can fire.
We use the module use-debounce in the project to limit the search to every 3 seconds.

#### Adding Pagination

Implementation consists of:

- get total number of pages based on search query and pass to pagination component.
- **usePathname** and **useSearchParams** hooks to get current page and set new page.
- **useSearchParams** in a function to set new page number and **pathName** to create URL string.
- If user types new search string reset the page number to 1.

#### Server Action

Server Actions allow you to run asynchronous code directly on the server. Very safe!

CREATE ITEM implementation:

- Create a form to capture the user's input.
- Create a Server Action and invoke it from the form.
- Inside your Server Action, extract the data from the formData object.
- Validate and prepare the data to be inserted into your database.
- Insert the data and handle any errors.
- Revalidate the cache and redirect the user back to invoices page.

#### Dynamic Route Segments

Create Dynamic Route Segments when you don't know the exact segment name and want to create routes based on data. Example href={`/dashboard/invoices/${id}/edit`}

UPDATE ITEM implementation:

- Create a new dynamic route segment with the invoice id.
- Read the invoice id from the page params.
- Fetch the specific invoice from your database.
- Pre-populate the form with the invoice data.
- Update the invoice data in your database.

DELETE ITEM implementation:

- To delete an invoice using a Server Action, wrap the delete button in a <form> element and pass the id to the Server Action using bind.

#### Error Handling

- Can use try catch in Server Actions to catch errors.
- error.tsx file can be used to serve fallback error UI.
- can create not-found.tsx file if want to specify 404 error. Will precede over error.tsx

#### Accessibility

- Use next lint in package.json scripts with the included eslint-plugin-jsx-ally
- Can add server side validation using Zod and updating server actions.
- Can use React useFormState hook to handle form errors, and display to user.

#### Authentication

Authentication checks who you are, and authorization determines what you can do or access in the application.

