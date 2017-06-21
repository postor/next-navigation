# next-navigation

navigation for next, auto highlight menu item of current route

## usage 

routes.js, use next-routes for both server side and client side route

``` 
const nextRoutes = require('next-routes')
const routes = module.exports = nextRoutes()

routes.add('index', '/')
routes.add('login', '/login')
routes.add('about', '/about')
routes.add('posts', '/posts')
routes.add('post', '/p/:title')
```

Header.js use nav in your page

```
import { default as routes, Link } from './routes'
import getNavigation from 'next-navigation'

const MyNav = getNavigation(routes)

export default (props)=>{

  var { url } = props
  var links = [{
    linkProps: { route: "index" },
    children: <a style={linkStyle}>Home</a>,
  }, {
    linkProps: { route: "about" },
    children: <a style={linkStyle}>About</a>,
    activeStyle: { color: 'blue', },
  }, {
    linkProps: { route: "posts" },
    children: <a style={linkStyle}>Posts</a>,
    checkIsActive: ({ pathname }) => {
      return ('/post' === pathname) || ('/posts' === pathname)
    }
  }]

  const activeStyle = {
    color: 'red',
    backgroundColor: '#ddd',
  }

  {
    ulProps: {
      className: 'mynav',
    },
    links,
    activeStyle,
    activeClassName: 'on',
    url,
  }
  
  return (<div className="nav-wrap">
    <MyNav {...navProps} />
    <style jsx>{`
        .nav-wrap :global(.mynav) {
          border: 1px solid black;
        }

        .nav-wrap :global(.mynav .on a) {
          font-weight: bold;
        }
      `}</style>
  </div>)
}

```

## full code example

https://github.com/nextjs-boilerplate/nextjs-boilerplate


