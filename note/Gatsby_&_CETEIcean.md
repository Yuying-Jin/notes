# Gatsby & CETEIcean in Gatsby

## Gatsby

Gatsby is a static website generator. It uses React Component module to build a website. 

### Install and Create a Website

https://www.gatsbyjs.com/docs/tutorial/part-1/

### React Component

#### What is React Component

React Component can create a series of components for the Gatsby site, including site pages, navigation bar, header, footer, links, images, etc. 

*Notice: The component name should start with a **capital** letter.*

#### How to create a component

```javascript
// Step 1: Import React
import React from 'react'

// Step 2: Define your component 
const IndexPage = () => {
  return (
    <main>
      <h1>Welcome to my Gatsby site!</h1>
      <p>I'm making this by following the Gatsby Tutorial.</p>
    </main>
  )
}

// Step 3: Export your component 
export default IndexPage
```

#### How to import a component 

```javascript
import React from "react"

// import a Layout component 
import Layout from "../components/layout" 

const IndexPage = () => {
 {
  return (
    <Layout>
      <h1>I’m in a layout!</h1>
    </Layout>
  );
}
export default IndexPage
```

#### How to import CSS 

```javascript
import React from "react"

// Import from a CSS file 
import "../styles/index.css"

// Import from an installed package 
import "bootstrap/dist/css/bootstrap.min.css"

export default function HomePage() {
  return <div>I'm styled by bootstrap & src/styles/index.css</div>
}
```

[*Learn more about React Components*](https://www.gatsbyjs.com/docs/tutorial/part-2/)

### GraphQL 

#### What is GraphQL 

GraphQL is a query language written in components to pull out the data in the Gatsby site. 

#### How to use GraphQL 

```js
import React from 'react'

// Step 1: Import the useStaticQuery hook and graphql tag 
import { useStaticQuery, graphql } from 'gatsby'

const Header = () => {
  /* Step 2: Use the useStaticQuery hook and graphql tag to query for data 
    (The query gets run at build time) */ 
  const data = useStaticQuery(graphql`
    query {
      site {
        siteMetadata {
          title
        }
      }
    }
  `)

  return (
    <header>
      {/* Step 3: Use the data in your component */}
      <h1>{data.site.siteMetadata.title}</h1>
    </header>
  )
}

export default Header
export default useSiteMetadata
```

This [link](http://localhost:8000/___graphql) is to explore the data layer.

[*Learn more about GraphQL*](https://www.gatsbyjs.com/docs/tutorial/part-4/) 

## CETEIcean in Gatsby

### What is CETEIcean

CETEIcean is a Javascript lib to display TEI documents in the browser. You should ensure you have the latest version of node.js.

#### Simple example

```javascript
// javascript script 
var CETEIcean = new CETEI()
CETEIcean.getHTML5("URL_TO_YOUR_TEI.xml", function(data) {
  document.getElementById("TEI").appendChild(data)
})
```

```html
<!-- HTML file -->
<html>
    <head><title></title></head>
    <body>
        <div id="TEI"></div>
    </body>       
</html>
```

TEI documents will be transferred to HTML format, and the result will be placed in the div with the id TEI.

[*Learn more about CETEIcean*](https://github.com/TEIC/CETEIcean)

#### How different is CETEIcean in Gatsby?

Gatsby has a plugin, `gatsby-theme-ceteicean`. 

> It re-implements parts of CETEIcean excluding behaviors; instead, to customize the behavior of specific elements, you can define React components with [React TEI Router](https://github.com/pfefferniels/react-teirouter).

#### Example

```javascript
import React from "react"

// import CETEIcean
import Ceteicean from "gatsby-theme-ceteicean/src/components/Ceteicean"
import {
  Tei,
  TeiHeader
} from "gatsby-theme-ceteicean/src/components/DefaultBehaviors"

// import components to customize the behavior of specific TEI element
import Pb from "./Pb"
import Note from "./Note"
import PlaceName from "./PlaceName"

// import the template
import Layout from "../../components/layout"

// import css files
import "./ceteicean.css"
import "./style.css"

const MyCeteicean = ({pageContext}) => {
  const routes = {
    "tei-tei": Tei,
    "tei-teiheader": TeiHeader,
    "tei-note": Note,
    "tei-placename": PlaceName,
    "tei-pb": (props) => <Pb {...props}/>,
  }

  return(
    <Layout>
      <Ceteicean pageContext={pageContext} routes={routes} />
    </Layout>
  )
}

export default MyCeteicean
```



[Adapting CETEIcean for static site building with React and Gatsby](https://zenodo.org/record/7085753#.Y_BH2nbMJPY)