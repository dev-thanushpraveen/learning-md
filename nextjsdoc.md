# Next.js

what is next js?

- React framework for production (A fullstack framework for ReactJs).
- it enhances react you build and structure your applications - there are multiple ways to build applications with React. Next.js provides a framework to structure your application, and optimizations to help
- next js creates fast search engine optimized zero configuraion.

![alt text](./intro.png)

## Key features & Benefits

- built-in server side rendering support.
  Automatic page pre-rendering: Great for SEO and performance
  Blending client-side and server-side rendering:Fetch data on the server and render finished pages.
  <br>

- file based routing
  Define pages and routes with files and folders instead of code.
  <br>

- Fullstack compatablity
  Easily add backend(server-side) code to your Next / React app
  storing data,getting data,authentication,etc.can be added to your Next / React app.

## creating a next js app

```javascript
   npx create-next-app
   npm i
   npm run dev
```

## pages and filebased routing

<pre>
      /pages
        |  index.js --> this is the main page(/)
        |  about.js --> this is the about page(/about)
        |__/products
            index.js --> this is the products page(/products/)
            [id].js  --> this is the product page(/products/[id])
</pre>

- demo : (pages,nestedpages,dynamic paths,nested dynamic paths,catch-all routes)

- navigating with the link component

- 404.js --> this is the 404 page(/404)

## page pre-rendering & Data Fetching

- Next.js can help us with a concept called pre-rendering.

- Good for SEO and performance.
<pre>
      Request --> /some-route
                       |
                       |
            return pre-rendered page + JS Code  -->   Hyderate with react code 
</pre>

- two forms of pre-rendering:
  - static Generation
  - server side rendering

### static generation

- pre-generate a page (with data prepared on the server side) during build time.
- Pages are prepared ahead to time and can be cached by the server / CDN serving the app.

```javascript
export async function getStaticProps(context) { ... }
```

- can do backend codes.

### incremental static generation

<pre>
                                  pre-generate page
                                          |
                                          |
                              Re generate it on every request,
                                  at most every X seconds.
                                          |
                                          |
                       ________________________________________
                      |                                        |
  serve old page if re-generate is not needed    Generate,store and serve "new" page otherwise. 
</pre>

```javascript
return {
  props: {
    products: data.products,
  },
  revalidate: 10,
};
```

- not found page && redirect

```javascript
return {
  props: {
    products: data.products,
  },
  revalidate: 10,
  notFound: true,
  redirect: "/products",
};
```

### Pre-generated paths

- Dynamic pages don't just need data : you also need to know which [id] values will be available.
- Multiple concrete [id] page instances (e.g id=1, id=2 etc) are pre generated.

```javascript
export async function getStaticPaths() {...}
```

- fallback key

### server side rendering

- sometimes you need to pre-render for every request or you need access to the request object.(e.g for cookies).
- Next.js allows you to run "real server side code" as well

```javascript
 export async function getServerSideProps(context) {...}
```

## client side data fetching

- some data doesn't need to be pre-rendered.<br>
  Data changing with high frequency.(eg:stock data)<br>
  Highly user specific data.(eg:last orders in an online shop)<br>
  Partial data.(eg:data that's only used on a part of an page)

## Nextjs optimization

- concepts:

  - Adding Meta and <head> Tags.
  - Re-using components,Logics and configurations.
  - Optimizing images.

- Meta and <Head> Tag:

  ```javascript
  import Head from "next/head";
  <Head>
    <title>Next.js</title>
    <meta
      name="description"
      content="Find a lot of great events that allow you to evolve..."
    />
  </Head>;
  ```

- reusing logic:
  same as react
