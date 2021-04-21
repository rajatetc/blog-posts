## The Art Of Making A Navbar

Perhaps, after reading the title you are like - what's the art in it? Well, I for one, think that it takes skill to create simple components like a navbar. And eventually, if you want to create something amazing like [Stripe's ](https://stripe.com/en-in) navbar - it is important to get the basics right. 

If you are sold - let's start building the navbar.

We will follow the mobile-first design approach, ie, we will first design our website for the smaller screen and then set it up for a bigger screen.

The demo link for the final project: https://codesandbox.io/s/adoring-williams-mrmic

## HTML

Let's begin by writing some HTML. 

In this project, I will be using free icons from Font Awesome. We can easily use them by linking to the CDN or through download. We will be using the CDN. 

The HTML will contain a `<nav>` for better accessibility. This div will act as a container for all things. In this div, we will place our links to various pages in our website, navbar toggle button, and social media icons.

Don't worry about all the class names for now. Their use will become more clear when we write some CSS.

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Navbar Demo</title>
    <!-- font-awesome -->
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.14.0/css/all.min.css"
    />
    <!-- styles -->
    <link rel="stylesheet" href="../src/styles.css" />
  </head>
  <body>
    <nav>
      <div class="nav-center">
        <div class="nav-header">
          <img src="./js-logo.svg" alt="logo" />
          <button class="nav-toggle">
            <i class="fas fa-bars"></i>
          </button>
        </div>
        <ul class="links">
          <li>
            <a href="home.html">home</a>
          </li>
          <li>
            <a href="about.html">about</a>
          </li>
          <li>
            <a href="contact.html">contact</a>
          </li>
        </ul>
        <ul class="social-icons">
          <li>
            <a href="https://twitter.com">
              <i class="fab fa-twitter"></i>
            </a>
          </li>
          <li>
            <a href="https://linkedin.com"
              ><i class="fab fa-linkedin-in"></i
            ></a>
          </li>
          <li>
            <a href="https://github.com">
              <i class="fab fa-github"></i>
              </a>
          </li>
        </ul>
      </div>
    </nav>
    <!-- javascript -->
    <script src="../src/index.js"></script>
  </body>
</html>

```

**Points to note:**

- Don't forget to link the stylesheet, add the font awesome link, and finally the script source.
- Be careful with the relative file paths. If you have the files in the same directory, use `"./filename",` if it's in a different folder, like src, use `"../src/filename"`. Also, use file extension, for example, if it's a `.css` file - use `filename.css` and so on.

## CSS

Now that we have our HTML in place, let's write some CSS. 

Let's start with setting some variables. **CSS variables** work just like any other variable. We set a value and can use it anywhere.

You might ask why to bother with these variables. Well, if you are using a value say at 5 places in your program and you want to change its value. With the CSS variable, you can change the value at one place and it will be reflected all over. It will make more sense when we write the code.

```
:root {
  --transition: all 0.4s linear;
  --spacing: 0.1rem;
}
```
Now, we set some global styles. These are mainly for the look and feel of our website. You may skip this step - this won't affect the functionality.

```
*,
::after,
::before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

ul {
  list-style-type: none;
}

a {
  text-decoration: none;
}

nav {
  box-shadow: 0 4px 14px rgba(0, 0, 0, 0.1);
}
```

### Small Screen Layout 


![small_screen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1618916190958/6A0FswrDE.png)

Now, let set up styles for the small screen. We will set up the layout using flexbox. The way it will work is that on the small screen - we will have a nav header container that will contain the logo and toggle button. We will set up functionality through JS that such that when we click on the button - the links will be displayed. By, default links will not be displayed. Also, social icons will not be displayed on the small screen.


```
.nav-toggle {
  font-size: 1.5rem;
  color: black;
  background: transparent;
  border: transparent;
  transition: var(--transition);
  cursor: pointer;
}

.nav-toggle:hover {
  transform: rotate(90deg);
}

.links a {
  color: grey;
  font-size: 1rem;
  display: block;
  padding: 0.5rem 1rem;
  transition: var(--transition);
  letter-spacing: var(--spacing);
  text-transform: capitalize;
}

.links a:hover {
  background: black;
  color: white;
  padding: 1rem;
}

.social-icons {
  display: none;
}

.links {
  height: 0;
  overflow: hidden;
  transition: var(--transition);
}

.show-links {
  height: 7rem;
}
```

**Points to note:**
- We are using the transition and spacing variables.

### Big Screen Layout


![big_screen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1618916208842/_s_9DZK8I.png)

Now, we will set up a big-screen layout using media queries such that when the screen size goes above 800px - we will change our layout.

Now, we will use the nav center class. Within the nav center container - we will first show the logo, then the links, and finally the social media icons. 

```
@media screen and (min-width: 800px) {
  .nav-center {
    max-width: 1170px;
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1rem;
  }
  .nav-toggle {
    display: none;
  }

  .nav-header {
    padding: 0;
  }

  .links {
    height: auto;
    display: flex;
  }

  .links a {
    padding: 0;
    margin: 0 0.5rem;
    font-size: 1.2rem;
  }
  .links a:hover {
    padding: 0;
    background: transparent;
    color: black;
  }

  .social-icons {
    display: flex;
  }

  .social-icons a {
    margin: 0 0.5rem;
    transition: var(--transition);
    color: gray;
  }

  .social-icons a:hover {
    color: black;
  }
}
```

We had `height : 0` for links which we change to `height: auto`. And for social media icons, we had `display: none` which now becomes `display: flex`

We are done with the CSS. You might have noticed:

```
.show-links {
  height: 7rem;
}
```

This is the class we will use to toggle our links on a smaller screen through JS. By default, we have height as 0.

## Javascript

We select the nav toggle button and the links container. We add a `click` event listener on the nav toggle button and add `show-links` class using the inbuilt toggle method. The way it works is basically if the class is not there it adds it on click and vice-versa. The class will give height to the container if present. I recommend opening up the console and see how the class gets added and removed to the DOM.

```
const navToggle = document.querySelector('.nav-toggle')
const links = document.querySelector('.links')

navToggle.addEventListener('click', function () {
  links.classList.toggle('show-links')
})
```

Alternatively, we can set up if statements instead of the toggle method like this:

```
  if (links.classList.contains("show-links")) {
    links.classList.remove("show-links");
  } else {
    links.classList.add("show-links");
  }
```

And we are done. If you encounter any issues - you can check out the code sandbox link at the start.