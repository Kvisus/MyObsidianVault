# Next.js

## nav+children

обернуть main, пассить children
``` jsx

//layout.js
import Nav from './Nav' //just nav component
  
export default function layout( {children} ) {
  return (
    <div className="">
      <Nav/>
      {/* pages */}
      <main>{children}</main>
    </div>
  )
};

//_app.js
import Layout from "../components/layout";
function MyApp({ Component, pageProps }) {
  return (
    <Layout>
      <Component {...pageProps} />
    </Layout>
  );
} 
export default MyApp;


```

## Add new Fonts etc

to add smth to root doc - create file **\_document.js** in ./pages
[Custom Document](https://nextjs.org/docs/advanced-features/custom-document)

A custom `Document` can update the `<html>` and `<body>` tags used to render a [Page](https://nextjs.org/docs/basic-features/pages). This file is only rendered on the server, so event handlers like `onClick` cannot be used in `_document`.

```jsx
import { Html, Head, Main, NextScript } from "next/document";
export default function Document() {
  return (
    <Html>
      <Head>
        <link rel="preconnect" href="https://fonts.googleapis.com" />
        <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
        <link
          href="https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,400;0,500;0,700;1,500&display=swap"
          rel="stylesheet"
        />
      </Head>
      <body>
        <Main />
        <NextScript />
      </body>
    </Html>
  );
}
```

**CLOSE LINK TAGS!**
