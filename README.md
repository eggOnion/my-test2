# My Portfolio Webpage using React

This project was built for my Coursera's assignment - React Advance with Meta. Here are some of my learnings, as well as the scope of this project.
<br />
\*\*{Update new Url}

---

## The "things" used in the project:

- JavaScript map function
- useRef, useEffct, useState, useContext hooks
- Custom hooks - useSubmit
- chakra-ui/react package
- FontAwesome

### JavaScript Map Function
In any programming languages, data structures and algorithms are fundamental concepts used to store, organize, and manipulate data efficiently.

* Maps are often used when you need to maintain an association between keys and values.

* A function to execute for each element in the array. Its return value is a copied version of the original version. Any chages to this copied will not affect the origin.


## Header Component
This component is responsible for:

* The **icons (emails, github, linkedin, medium & stackoverflow)** on the top panel
  of the webpage.

* The **Projects** and **Contact Me** Url

* Hiding or Revealing the header when scrolling down or up.

* Providing the scrolling movements to the **Projects** or **Contact Me** section when clicked.
<br />

### The Icons
First, We declare an array of objects to store the icons & urls.

```
const socials = [
  {
    icon: faEnvelope,
    url: "mailto: hello@example.com",
  },
  {
    icon: faGithub,
    url: "https://github.com",
  },
  {
    icon: faLinkedin,
    url: "https://www.linkedin.com",
  },
  {
    icon: faMedium,
    url: "https://medium.com",
  },
  {
    icon: faStackOverflow,
    url: "https://stackoverflow.com",
  },
];
```

---

By using the **Map** function, we can easily retrieve the data again.
```
<nav>
  {/* Add social media links based on the `socials` data */}
    <HStack spacing="24px">
      {socials.map((social, index) => (
        <a
          href={social.url}
          key={index}
          target="_blank"
          rel="noopener noreferrer"
        >
          <FontAwesomeIcon icon={social.icon} size="2x" />
        </a>
      ))}
    </HStack>
</nav>
```
In the console log, this is how the data are stored:
<insert image>

The data can then be retrieve easily using the dot notation. Eg; ***social.url*** & ***social.icon***

The images of the icon is from **_fortawesome/free-brands-svg-icons_** package.

---

### The Urls

The ***handleClick*** function perform scrolling movement to the corresponding section, inside the webpage when either the ***Projects*** or ***Contact Me*** link is clicked.
```
const handleClick = (anchor) => () => {
    const id = `${anchor}-section`;
    const element = document.getElementById(id);
    const offset = 100;

    if (element) {
      const elementPosition =
        element.getBoundingClientRect().top + window.pageYOffset;
      const offsetPosition = elementPosition - offset;

      window.scrollTo({
        top: offsetPosition,
        behavior: "smooth",
        block: "start",
      });
    }
  };
  ```

The ***handleClick*** function takes in a anonymous function and a parameter name ***anchor*** which serve as an identifier later when searching for the corresponding sections. 

The **element** variables checks if the id exist using the **document.getElementById(id)** method to interact with the DOM. The id will be stored it it exists, else it will be null.

The **offset** variable adjust the pixels of 100 for precision so that the corresponding section can be reached.

The **if (element)** condition will be execute if the id exisits. Meaning, when someone clicks the url. The members inside will provide the scrolling motion to the corresponding section of the webpage.
<br />

---

Rendering of the ***Projects*** & ***Contact Me*** urls are below.
```
<nav>
  <HStack spacing="24px">
    {/* Add links to Projects and Contact me section */}
    <
      href="#projects"
      onClick={handleClick("projects")}
      key="projects-link"
    >
      Projects
    
    {/* Link to the Contact Me section */}
    <a
      href="#contact-me"
      onClick={handleClick("contactme")}
      key="contactme-link"
    >
      Contact Me
    </a>
  </HStack>
</nav>
```

Here, we passed in the String argument **projects** or **contactme** to the ***handleClick function*** which controls the ***onClick evenHandler***. The String will be passed to the **anchor** parameter as mentioned previously.

---

### Hiding & Revealing the Header when scrolling up or down
This portion of the code handles the hiding/revealing of the header panel on the webpage. 

```
 const [scrollDirection, setScrollDirection] = useState("up");
  const prevScrollY = useRef(0);
  const headerRef = useRef(null);

  const handleScroll = () => {
    const currentScrollY = window.scrollY;

    if (currentScrollY > prevScrollY.current) {
      // Scrolling down
      setScrollDirection("down");
    } else {
      // Scrolling up
      setScrollDirection("up");
    }

    prevScrollY.current = currentScrollY;
  };

  useEffect(() => {
    window.addEventListener("scroll", handleScroll);

    return () => {
      window.removeEventListener("scroll", handleScroll);
    };
  }, []);

  useEffect(() => {
    if (headerRef.current) {
      headerRef.current.style.transform =
        scrollDirection === "down" ? "translateY(-200px)" : "translateY(0)";
    }
  }, [scrollDirection]);
```

#### Hooks
* ***useState*** stores a String of the scrollDirection either "up" or "down".
* ***useRef*** stores the value of the previous scroll position (Y-axis).
* ***useEffect*** runs everytime when the scroll direction changes.

***scrollDirection*** is the state that tracks the current scroll direction (up or down).

**prevScrollY** using the previous value as a reference to compare against the current scroll position using ***window.scrollY***, a property in the Js DOM.

#### handleScroll Function
* As mentioned earlier, this function takes in the value of the current scroll position and compared it against the previous scroll position.

* If the value of the current scroll is bigger, it means that the webpage is being scrolled down. 

* The final scroll position, regardless of the direction (up or down) will then be stored.

* The whole process repeats itself when user began scrolling again.

#### useEffect & Event Listner 

* The first ***useEffect*** adds an ***Event Listner*** to the scroll event. 

* This means, the ***handleScroll*** function will be called when user scrolls.

* The second ***useEffect*** runs when the ***scrollDirection*** changes. The ***headerRef.current.style.transform*** directly manipulate the CSS style, hiding/revealing the header.

---

### How it works?

* The ***handleScroll*** function is triggered everytime a user scrolls. It compares the value of ***prevScrollY*** against ***currentScrollY*** to determine the direction of the scroll (up or down).

* The ***scrollDirection*** state is updated to either "up or "down" depending on where the user scrolls.

* When the ***scrollDirection*** changes, updating the ***headerRef*** and manipulate the CSS, hiding the header by 200px when scrolling down, and revealing it when scrolling upwards.

---

### LandingSection Component
This section renders the greeting and bio-info of the person on the webpage.

* Three variables declared are ***greeting***, ***bio1*** & ***bio2***.

* Next, we passed those variables through JSX to render the data.

```
<h1>{greeting}</h1>    
<p style={{ fontSize: "45px" }}>{bio1}</p>
<p style={{ fontSize: "45px" }}>{bio2}</p>
```

---

## Featured Projects
This section of the webpage consists of multiple components working together.

* ProjectsSection
* Cards
* FullScreenSection

The ***ProjectsSection*** is the parent to both the child; ***FullScreenSection*** & ***Cards***

### ProjectsSection Component
It consists of an array of objects storing all the projects on this webpage.
* The ***projects*** array stores all the projects as an object.

* Data in the ***projects*** array pass down to its child, ***Cards*** through props using map function and dot notation to access the value in the object. 

* Next, we set the CSS layout of this section by passing of props to its child, ***FullScreenSection***.
> The Cards Component also play a part in the CSS styling. We will come to that later.

### Cards Component
* Received the props that were passed down from its parent component, ***ProjectsSection***.

* Rendered the props using the ***Box***, ***Image***, ***Heading***, and ***Text*** components from ***chakra-ui/react*** to better manage the layout and styles.

### FullScreenSection Component
* Manage the height & width of each section using the ***VStack*** components from ***chakra-ui/react***.


## ContactMeSection Component

* Using ***useFormik*** & ***yup*** for validating the form inputs.

* ***Chakra-ui/react*** for styling the UI layout of form, input, buttons 

* Using of custom hooks like the ***useSubmit*** & ***useAlertContext*** for handling the form submission and displaying the alert-box.

---

## Media

* chakra-ui 
<br />https://www.npmjs.com/package/@chakra-ui/react

* Fontawesome
<br />https://www.npmjs.com/package/@fortawesome/free-brands-svg-icons

* yup
<br />https://www.npmjs.com/package/yup

* formik
<br />https://www.npmjs.com/package/formik

* Map function
<br />https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map