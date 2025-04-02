---
layout: "../../layouts/BlogPost.astro"
title: "Creating a Digital Resume with HTML, CSS, and GitHub Pages"
pubDate: "2025-03-01 14:21:40.959094"
youtubeVideoID: "clwpf3VwCZQ"
index:
---

# Creating a Digital Resume with HTML, CSS, and GitHub Pages

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/clwpf3VwCZQ" frameborder="0" allowfullscreen></iframe>


## Introduction

This chapter will guide you through the process of creating a digital resume using web technologies and deploying it online for free. We will transform a traditional resume into an interactive and shareable digital format using HTML (HyperText Markup Language) for structure and content, CSS (Cascading Style Sheets) for styling and visual appeal, and GitHub Pages for hosting. This digital resume will not only be more engaging than a static document but also easily accessible via a unique URL that you can share with potential employers and on social media platforms.

> **HTML (HyperText Markup Language)**
> The standard markup language for documents designed to be displayed in a web browser. It provides the structure and content of a webpage.

> **CSS (Cascading Style Sheets)**
> A style sheet language used for describing the presentation of a document written in a markup language like HTML. CSS controls the layout, colors, fonts, and overall visual aesthetics of a webpage.

While a digital resume can be a valuable tool, it is important to note that it is generally recommended to also maintain a separate portfolio website for showcasing more in-depth projects and work. Consider linking your digital resume from your portfolio site. However, if you do not yet have a portfolio, this digital resume is an excellent starting point to establish your online presence.

## Project Overview and Demonstration

Before diving into the development process, let's understand what we aim to build. This project will result in a live, web-based version of a resume, complete with both light and dark mode themes. You will be able to choose your preferred theme and deploy it online.

Here's a breakdown of the key features and content elements:

*   **Live URL:** Your resume will be accessible through a unique and shareable web address.
*   **Stylish Design:** Utilizing CSS, the resume will be visually appealing and more modern than a typical document.
*   **Light and Dark Mode Themes:** You can select either a light or dark theme to suit your preference.
*   **Content Parallels Traditional Resume:** The digital resume will include all essential sections found in a standard resume, such as:
    *   Social Links and Contact Information
    *   Bio/Summary
    *   Skills and Qualifications
    *   Technical Stack
    *   Work History
*   **Optional Image:** You have the option to include a personal image for added personalization.
*   **Projects and Accomplishments Section (Optional):**  An expandable section to showcase specific projects with more detail, source code links, images, and live demos.

Let's take a look at a demonstration of the final product:

[Demonstration of the digital resume interface, showcasing both light and dark mode, social links, bio, skills, tech stack, work history, and projects section.]

As you can see in the demo, the digital resume presents information in a structured and visually engaging manner.  The content is drawn directly from a traditional resume, but enhanced for the web format.

## Sponsorship Acknowledgment: Agora

Before we proceed with building the digital resume, let's take a moment to acknowledge our sponsor, Agora.

Agora is a real-time engagement platform that provides developers with Software Development Kits (SDKs) and low-code tools to easily integrate real-time communication features into applications.

> **SDK (Software Development Kit)**
> A set of software development tools that allows the creation of applications for a certain software package, software framework, hardware platform, computer system, video game console, operating system, or similar development platform.

Agora's offerings include:

*   **Audio and Video Calling SDKs:**  Enabling features like group chats, screen sharing, and recording within applications.
*   **Real-time Data Signaling:**  Facilitating the transmission of data in real-time.
*   **Real-time Messaging SDK:** Simplifying the implementation of real-time messaging, often a complex task when configuring websockets or socket servers manually.
*   **Streaming to Third-Party Platforms:**  Allowing direct streaming to platforms like YouTube.

Agora's tools streamline the development of real-time engagement features, saving developers significant time and effort.  For those interested in exploring real-time communication capabilities, Agora offers a comprehensive suite of tools and resources. You can find more information on their website, agora.io.

> **Websockets**
> A communication protocol that provides full-duplex communication channels over a single TCP connection. It enables real-time, two-way communication between client and server in web applications.

## Setting Up the Project Structure

To begin building our digital resume, we need to set up the project file structure. This organized structure will keep our files manageable and ensure that our website functions correctly.

Here's the recommended file structure:

```
resume-website/
├── index.html        // Main HTML file for the resume
├── assets/            // Folder for static assets
│   ├── images/        // Folder for images (profile picture)
│   │   └── profile-pic.jpg
│   └── resume.pdf    // PDF version of your resume (optional)
└── styles/           // Folder for CSS stylesheets
    └── main.css      // Main CSS file for styling
```

Let's create this structure on your local machine:

1.  **Create a new folder:** Name it `resume-website` (or any name you prefer).
2.  **Inside `resume-website`, create:**
    *   `index.html` file
    *   `assets` folder
    *   `styles` folder
3.  **Inside `assets`, create:**
    *   `images` folder
4.  **Inside `styles`, create:**
    *   `main.css` file

If you have a profile picture and a PDF version of your resume, place them in the `assets/images` and `assets` folders respectively, naming the image `profile-pic.jpg` and the PDF `resume.pdf` for consistency with the example project. You can use placeholder images and PDFs initially if you don't have these ready.

## Building the HTML Structure (index.html)

Now, let's construct the HTML structure of our digital resume in the `index.html` file. This file will define the content and basic layout of our webpage.

Start with the basic HTML boilerplate:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Digital Resume</title>
    <link rel="stylesheet" href="./styles/main.css">
</head>
<body>

</body>
</html>
```

This provides the basic structure for an HTML document, including:

*   `<!DOCTYPE html>`:  Declares the document type as HTML5.
*   `<html lang="en">`:  The root element of the HTML page, specifying the language as English.
*   `<head>`: Contains meta-information about the HTML document, such as character set, viewport settings, title, and links to stylesheets.
    *   `<meta charset="UTF-8">`: Sets the character encoding for the document to UTF-8, supporting a wide range of characters.
    *   `<meta name="viewport" content="width=device-width, initial-scale=1.0">`: Configures the viewport for responsive design, ensuring proper scaling on different devices.
    *   `<title>Digital Resume</title>`: Sets the title that appears in the browser tab or window title bar.
    *   `<link rel="stylesheet" href="./styles/main.css">`: Links the external CSS file (`main.css`) to style the HTML document.
*   `<body>`: Contains the visible content of the HTML document.

### Structuring the Body Content

Within the `<body>` tags, we will add the content sections of our resume.  We will use semantic HTML elements and `div` elements with IDs and classes for styling and organization.  We will also employ the BEM (Block, Element, Modifier) naming convention for CSS classes to enhance maintainability and clarity.

> **BEM (Block, Element, Modifier)**
> A methodology for naming CSS classes to create reusable and organized stylesheets. It helps to improve code readability and maintainability, especially in larger projects.

**1. Main Container:**

Wrap all the resume content within a main container `div` to control the overall width and centering of the page content.

```html
<div id="container--main">
    </div>
```

**2. Hero Section:**

This section will typically be at the top of the resume and include your profile picture, name, bio, and contact information.

```html
<section id="wrapper--hero" class="section--page">
    <img id="profile--pic" src="./assets/images/profile-pic.jpg" alt="Profile Picture">
    <div>
        <h1 id="user-name">Your Name</h1>
        <p id="bio">A brief and impactful summary of your professional background and goals. Include links to relevant online profiles if applicable.</p>
        <p id="email">contact@email.com <span style="font-size: smaller;">👉</span></p>
    </div>
</section>
```

*   `<section id="wrapper--hero" class="section--page">`: A semantic section element to group the hero content. `id="wrapper--hero"` is used for specific hero section styling, and `class="section--page"` provides general styling applicable to all page sections.
*   `<img id="profile--pic" ...>`:  An `img` tag to display your profile picture.  `id="profile--pic"` is for styling the image.  `src="./assets/images/profile-pic.jpg"` specifies the image source path. `alt="Profile Picture"` provides alternative text for accessibility.
*   `<div> ... </div>`: A `div` to wrap the text content (name, bio, email) within the hero section.
*   `<h1 id="user-name">`:  An `h1` heading for your name. `id="user-name"` is for styling the name.
*   `<p id="bio">`:  A paragraph for your professional bio or summary. `id="bio"` is for styling the bio.
*   `<p id="email">`: A paragraph for your email address, including a pointing emoji for visual emphasis.

**3. Social Links Section:**

This section will list links to your social media profiles, portfolio website, and a downloadable resume.

```html
<section class="section--page">
    <div id="socials--list">
        <a href="#" target="_blank">YouTube</a>
        <a href="#" target="_blank">Twitter</a>
        <a href="#" target="_blank">LinkedIn</a>
        <a href="#" target="_blank">GitHub</a>
        <a href="./assets/resume.pdf" target="_blank">Download Resume</a>
    </div>
</section>
```

*   `<section class="section--page">`: Another section element, using the general `section--page` class for styling.
*   `<div id="socials--list">`: A `div` to contain the social links. `id="socials--list"` is for styling the list of social links.
*   `<a href="#" target="_blank"> ... </a>`: Anchor tags (`<a>`) for each social link.
    *   `href="#"`:  Replace `#` with the actual URL of your social profile or website.
    *   `target="_blank"`:  Opens the link in a new tab or window.

**4. Skills and Qualifications Section:**

This section will list your key skills and qualifications.

```html
<section class="section--page">
    <h2>Skills & Qualifications</h2>
    <ul id="qualifications--list">
        <li>✅ Proficient in various programming languages and technologies.</li>
        <li>✅ Experience in web development, mobile development, and database management.</li>
        <li>✅ Strong problem-solving and analytical skills.</li>
        <li>✅ Excellent communication and teamwork abilities.</li>
    </ul>
</section>
```

*   `<section class="section--page">`: Another section element with general page section styling.
*   `<h2>Skills & Qualifications</h2>`: An `h2` heading for the section title.
*   `<ul id="qualifications--list">`: An unordered list (`<ul>`) to list your skills. `id="qualifications--list"` is for styling the list.
*   `<li>✅ ... </li>`: List item tags (`<li>`) for each skill or qualification, using a checkmark emoji for visual appeal.

**5. Technical Stack Section:**

This section will showcase your technical skills categorized by technology type (e.g., Languages, Frameworks, Databases).

```html
<section class="section--page">
    <h2>Tech Stack</h2>
    <div id="wrapper--techstack__items">
        <div class="card card--techstack">
            <span>Python, JavaScript, Node.js</span>
        </div>

        <div class="card card--techstack">
            <span>Django, React, Express.js</span>
        </div>

        <div class="card card--techstack">
            <span>PostgreSQL, MySQL, MongoDB</span>
        </div>

        <div class="card card--techstack">
            <span>Git, Docker, AWS</span>
        </div>
    </div>
</section>
```

*   `<section class="section--page">`: Section element with general page section styling.
*   `<h2>Tech Stack</h2>`: `h2` heading for the section title.
*   `<div id="wrapper--techstack__items">`: A `div` to wrap the tech stack items. `id="wrapper--techstack__items"` is for styling the layout of the tech stack items.
*   `<div class="card card--techstack">`: `div` elements with classes `card` and `card--techstack` to represent individual tech stack cards. These are styled to visually separate tech categories.
*   `<span> ... </span>`: `span` elements within each card to display the list of technologies in each category.

**6. Work History Section:**

This section will detail your professional work experience in reverse chronological order.

```html
<section class="section--page" id="work-history--wrapper">
    <h2>Work History</h2>

    <div class="line-break"></div>

    <div class="card card--workhistory">
        <strong>Developer Advocate at Agora <span style="opacity: 0.5;"> (Nov 2021 - Present)</span></strong>
        <p>As a Developer Advocate at Agora, I focus on creating educational content and building tools to help developers effectively use Agora's real-time engagement platform. My responsibilities include developing tutorials, sample applications, and engaging with the developer community.</p>
        <ul>
            <li>✅ Doubled usage minutes from 15 million to 30 million minutes within the first four months.</li>
            <li>✅ Produced educational content (videos, articles, and workshops) on Agora's technology.</li>
            <li>✅ Led successful SEO campaigns resulting in increased organic traffic to Agora's developer resources.</li>
        </ul>
    </div>

    <!-- Repeat the card structure for each work experience entry -->

</section>
```

*   `<section class="section--page" id="work-history--wrapper">`: Section element with general styling and `id="work-history--wrapper"` for specific work history section styling.
*   `<h2>Work History</h2>`: `h2` heading for the section title.
*   `<div class="line-break"></div>`: A `div` with class `line-break` to create a visual separator line before each work experience entry.
*   `<div class="card card--workhistory">`: `div` elements with classes `card` and `card--workhistory` to represent individual work history cards.
*   `<strong> ... </strong>`: `strong` tag to emphasize the job title and company. `<span style="opacity: 0.5;"> ... </span>` within the strong tag to display the employment period with reduced opacity.
*   `<p> ... </p>`: Paragraph tag for a brief description of the role and responsibilities.
*   `<ul> ... </ul>`: Unordered list to highlight key achievements and responsibilities, using checkmark emojis for visual emphasis.

**7. Projects & Accomplishments Section (Optional):**

This section provides a space to showcase specific projects and accomplishments in more detail.

```html
<section class="section--page">
    <h2>Projects & Accomplishments</h2>

    <div class="card card--project">
        <a href="./project1.html">Built a Laboratory Management System for a Forensics Lab  🏆 </a>
        <p>Developed a web-based laboratory management system to streamline workflows, manage samples, and generate reports for a forensics laboratory. </p>
    </div>

    <!-- Repeat the card structure for each project or accomplishment -->

</section>
```

*   `<section class="section--page">`: Section element with general page section styling.
*   `<h2>Projects & Accomplishments</h2>`: `h2` heading for the section title.
*   `<div class="card card--project">`: `div` elements with classes `card` and `card--project` to represent individual project cards.
*   `<a href="./project1.html"> ... </a>`: Anchor tag linking to a separate project details page (`project1.html`). `🏆` trophy emoji added for visual emphasis of accomplishments.
*   `<p> ... </p>`: Paragraph tag for a brief description of the project.

This completes the basic HTML structure for the digital resume.  Save `index.html` and proceed to styling the resume with CSS.

## Styling the Resume with CSS (main.css)

Now, let's style our digital resume using CSS in the `main.css` file. CSS will control the visual presentation of our HTML content, including layout, colors, fonts, and responsiveness.

First, let's set up some global styles and CSS variables to manage our design system and theme switching.

### Global Styles and CSS Variables

At the top of your `main.css` file, add the following:

```css
@import url('https://fonts.googleapis.com/css2?family=Redex+Pro:wght@200;300;400;500;600;700;800;900&display=swap');

:root {
    --main-text-color-light: #000;
    --secondary-text-color-light: #5c5c62;
    --main-link-color-light: #1775ee;
    --main-border-color-light: #cdd2d7;
    --main-bg-color-light: #f8f8fa;

    --main-text-color-dark: #fff;
    --secondary-text-color-dark: #c5c6cb;
    --main-link-color-dark: #4abfff;
    --main-border-color-dark: #4d545d;
    --main-bg-color-dark: #192734;

    --main-text-color: var(--main-text-color-dark); /* Default to dark mode */
    --secondary-text-color: var(--secondary-text-color-dark);
    --main-link-color: var(--main-link-color-dark);
    --main-border-color: var(--main-border-color-dark);
    --main-bg-color: var(--main-bg-color-dark);
}
```

*   `@import url(...)`: Imports the "Redex Pro" font from Google Fonts. This line should be placed at the very top of your CSS file.

> **@import**
> A CSS at-rule used to import style rules from other style sheets. It allows for modularization and reuse of CSS code.

*   `:root { ... }`: Defines CSS variables within the `:root` pseudo-class, making them globally accessible throughout the stylesheet.

> **CSS Variables (Custom Properties)**
> Entities defined by CSS authors that contain specific values to be reused throughout a document. They enable greater control over styling and theme management.

    *   `--main-text-color-light`, `--secondary-text-color-light`, etc.:  Variables defined for the light theme, specifying colors for text, links, borders, and background.
    *   `--main-text-color-dark`, `--secondary-text-color-dark`, etc.: Variables defined for the dark theme, similarly specifying colors for the dark theme.
    *   `--main-text-color: var(--main-text-color-dark);`: Sets the default color variables to use the dark theme variables initially.  To switch to light mode, you would change `-dark` to `-light` in these default variable assignments.

Next, define global styles that apply to the entire page:

```css
* {
    font-family: 'Redex Pro', sans-serif;
    line-height: 1.5em;
    box-sizing: border-box;
    color: var(--main-text-color);
}

body {
    background-color: var(--main-bg-color);
}

p, span, li {
    color: var(--secondary-text-color);
    font-size: 1em;
}

a {
    text-decoration: none;
    color: var(--main-link-color);
    font-weight: 500;
}

li {
    line-height: 1.9em;
}
```

*   `* { ... }`:  The universal selector, applying styles to all elements on the page.
    *   `font-family: 'Redex Pro', sans-serif;`: Sets the font family to the imported "Redex Pro" font, with "sans-serif" as a fallback.
    *   `line-height: 1.5em;`: Sets the default line height for text.
    *   `box-sizing: border-box;`:  Changes the box-sizing model to `border-box`, which includes padding and border in the element's total width and height.

> **box-sizing: border-box**
> A CSS property that alters the default CSS box model. When set to `border-box`, the padding and border of an element are included in the element's total width and height, simplifying layout calculations.

    *   `color: var(--main-text-color);`: Sets the default text color using the `--main-text-color` CSS variable.
*   `body { ... }`: Styles for the `<body>` element.
    *   `background-color: var(--main-bg-color);`: Sets the background color of the body using the `--main-bg-color` CSS variable.
*   `p, span, li { ... }`: Styles for paragraph (`<p>`), span (`<span>`), and list item (`<li>`) elements.
    *   `color: var(--secondary-text-color);`: Sets the text color to the `--secondary-text-color` variable.
    *   `font-size: 1em;`: Sets the font size to 1em (equivalent to the default font size).
*   `a { ... }`: Styles for anchor (`<a>`) elements (links).
    *   `text-decoration: none;`: Removes the default underline from links.
    *   `color: var(--main-link-color);`: Sets the link color to the `--main-link-color` variable.
    *   `font-weight: 500;`: Sets the font weight to 500 for slightly bolder links.
*   `li { ... }`: Styles specifically for list items.
    *   `line-height: 1.9em;`: Increases the line height for list items to create more vertical spacing.

### Section-Specific Styling

Now, let's style the different sections of our resume using their IDs and classes.

**1. Main Container Styling:**

```css
#container--main {
    max-width: 700px;
    margin: 0 auto; /* Centers the container horizontally */
}
```

*   `#container--main { ... }`: Styles for the main container `div` (with `id="container--main"`).
    *   `max-width: 700px;`: Sets the maximum width of the container to 700 pixels, limiting the content width on larger screens.
    *   `margin: 0 auto;`: Centers the container horizontally within its parent element. `0` sets the top and bottom margins to zero, and `auto` distributes the remaining horizontal space equally on both sides.

**2. Page Section Styling:**

```css
.section--page {
    padding-top: 1em;
    padding-bottom: 1em;
}
```

*   `.section--page { ... }`: Styles for elements with the class `section--page` (applied to all `<section>` elements).
    *   `padding-top: 1em;`: Adds padding at the top of each section.
    *   `padding-bottom: 1em;`: Adds padding at the bottom of each section, creating vertical spacing between sections.

**3. Hero Section Styling:**

```css
#wrapper--hero {
    display: flex;
    align-items: center;
    gap: 4em;
}
```

*   `#wrapper--hero { ... }`: Styles for the hero section wrapper (`id="wrapper--hero"`).
    *   `display: flex;`: Enables flexbox layout for the hero section, allowing for flexible arrangement of its child elements (image and text).

> **Flexbox (Flexible Box Layout)**
> A CSS layout module that provides an efficient way to lay out, align, and distribute space among items in a container, even when their size is unknown or dynamic.

    *   `align-items: center;`: Vertically aligns items along the cross-axis (in this case, vertically) to the center of the flex container.
    *   `gap: 4em;`: Sets the gap (space) between flex items to 4em units.

**4. Bio Styling:**

```css
#bio {
    font-weight: 300; /* Lighter font weight */
}
```

*   `#bio { ... }`: Styles for the bio paragraph (`id="bio"`).
    *   `font-weight: 300;`: Sets a lighter font weight for the bio text, making it visually distinct from headings and stronger text.

**5. User Name Styling:**

```css
#user-name {
    font-size: 3em;
    line-height: 1em;
}
```

*   `#user-name { ... }`: Styles for the user name heading (`id="user-name"`).
    *   `font-size: 3em;`: Sets a large font size (3 times the default font size) for the name.
    *   `line-height: 1em;`: Adjusts the line height to 1em for tighter vertical spacing around the name.

**6. Profile Picture Styling:**

```css
#profile--pic {
    border-radius: 50%; /* Makes the image circular */
    width: 150px;
    height: 150px;
    object-fit: cover; /* Ensures the image covers the circular area without distortion */
}
```

*   `#profile--pic { ... }`: Styles for the profile picture (`id="profile--pic"`).
    *   `border-radius: 50%;`: Makes the image circular by setting the border radius to 50% of its width or height.
    *   `width: 150px;`: Sets the width of the image to 150 pixels.
    *   `height: 150px;`: Sets the height of the image to 150 pixels.
    *   `object-fit: cover;`: Specifies how the image should be resized to fit its container. `cover` ensures the image covers the entire container, cropping if necessary to maintain aspect ratio.

**7. Email Styling:**

```css
#email {
    color: var(--main-text-color); /* Ensures email color follows theme */
}
```

*   `#email { ... }`: Styles for the email paragraph (`id="email"`).
    *   `color: var(--main-text-color);`: Sets the email text color to the `--main-text-color` variable, ensuring it adapts to the chosen theme.

**8. Socials List Styling:**

```css
#socials--list {
    display: flex;
    justify-content: space-between;
    column-gap: 1em;
    flex-wrap: wrap; /* Allows links to wrap to the next line on smaller screens */
}

#socials--list a {
    font-size: 0.9em;
}

#socials--list a:hover {
    color: var(--secondary-text-color);
    transition: 0.3s; /* Smooth color transition on hover */
}
```

*   `#socials--list { ... }`: Styles for the socials list container (`id="socials--list"`).
    *   `display: flex;`: Enables flexbox layout for the social links.
    *   `justify-content: space-between;`: Distributes space evenly between links, pushing the first link to the start and the last link to the end of the container.
    *   `column-gap: 1em;`: Sets a gap of 1em between columns (between links).
    *   `flex-wrap: wrap;`: Allows the links to wrap to the next line if they exceed the container width.
*   `#socials--list a { ... }`: Styles for anchor tags (`<a>`) within the socials list.
    *   `font-size: 0.9em;`: Sets a slightly smaller font size for social links.
*   `#socials--list a:hover { ... }`: Styles for link hover state within the socials list.
    *   `color: var(--secondary-text-color);`: Changes the link color to `--secondary-text-color` on hover.
    *   `transition: 0.3s;`: Applies a smooth color transition over 0.3 seconds on hover.

> **CSS Transition**
> A CSS feature that allows property changes in CSS values to occur smoothly over a specified duration. It enhances user experience by providing visual feedback for interactions.

**9. Qualifications List Styling:**

```css
#qualifications--list {
    list-style: none; /* Removes default bullet points */
}
```

*   `#qualifications--list { ... }`: Styles for the qualifications list (`id="qualifications--list"`).
    *   `list-style: none;`: Removes the default bullet points from the unordered list.

**10. Tech Stack Items Wrapper Styling:**

```css
#wrapper--techstack__items {
    display: flex;
    flex-wrap: wrap;
    gap: 1em;
    font-size: 0.9em;
}
```

*   `#wrapper--techstack__items { ... }`: Styles for the tech stack items wrapper (`id="wrapper--techstack__items"`).
    *   `display: flex;`: Enables flexbox layout for tech stack items.
    *   `flex-wrap: wrap;`: Allows tech stack cards to wrap to the next line if they exceed the container width.
    *   `gap: 1em;`: Sets a gap of 1em between tech stack cards.
    *   `font-size: 0.9em;`: Sets a slightly smaller font size for the tech stack section.

**11. Tech Stack Card Styling:**

```css
.card--techstack {
    border: 1px solid var(--main-border-color);
    padding: 0.5em 1em;
    border-radius: 5px;
}
```

*   `.card--techstack { ... }`: Styles for elements with the class `card--techstack` (tech stack cards).
    *   `border: 1px solid var(--main-border-color);`: Adds a 1-pixel solid border using the `--main-border-color` variable.
    *   `padding: 0.5em 1em;`: Sets vertical padding to 0.5em and horizontal padding to 1em inside the card.
    *   `border-radius: 5px;`: Rounds the corners of the card with a 5-pixel radius.

**12. Work History Card Styling:**

```css
.card--workhistory {
    border-left: 1px solid var(--main-border-color);
    margin-top: 3em;
    margin-bottom: 3em;
    padding-left: 2em;
}
```

*   `.card--workhistory { ... }`: Styles for elements with the class `card--workhistory` (work history cards).
    *   `border-left: 1px solid var(--main-border-color);`: Adds a 1-pixel solid border on the left side of the card, using the `--main-border-color` variable.
    *   `margin-top: 3em;`: Adds top margin for vertical spacing.
    *   `margin-bottom: 3em;`: Adds bottom margin for vertical spacing.
    *   `padding-left: 2em;`: Adds left padding to create space between the left border and the content.

**13. Line Break Styling:**

```css
.line-break {
    background-color: var(--main-border-color);
    height: 1px;
}
```

*   `.line-break { ... }`: Styles for elements with the class `line-break` (separator lines).
    *   `background-color: var(--main-border-color);`: Sets the background color of the line using the `--main-border-color` variable.
    *   `height: 1px;`: Sets the height of the line to 1 pixel, creating a thin horizontal line.

**14. Project Card Styling:**

```css
.card--project {
    padding-top: 1em;
    padding-bottom: 1em;
    border-top: 1px solid var(--main-border-color);
}

.card--project a {
    color: var(--main-text-color);
    transition: 0.3s;
}

.card--project a:hover {
    color: var(--main-link-color);
}
```

*   `.card--project { ... }`: Styles for elements with the class `card--project` (project cards).
    *   `padding-top: 1em;`: Adds top padding to the card.
    *   `padding-bottom: 1em;`: Adds bottom padding to the card.
    *   `border-top: 1px solid var(--main-border-color);`: Adds a 1-pixel solid border at the top of the card, using the `--main-border-color` variable.
*   `.card--project a { ... }`: Styles for anchor tags (`<a>`) within project cards.
    *   `color: var(--main-text-color);`: Sets the link color to `--main-text-color`.
    *   `transition: 0.3s;`: Adds a transition effect.
*   `.card--project a:hover { ... }`: Styles for link hover state in project cards.
    *   `color: var(--main-link-color);`: Changes the link color to `--main-link-color` on hover.

### Responsive Design with Media Queries

To ensure our digital resume looks good on different screen sizes, we will implement responsive design using CSS media queries. We will adjust the layout for smaller screens (e.g., mobile devices).

```css
@media (max-width: 600px) {
    #wrapper--hero {
        flex-direction: column; /* Stack image and text vertically */
        gap: 1em; /* Reduce gap in mobile view */
    }

    #profile--pic {
        width: 200px; /* Increase image size on mobile */
        height: 200px;
    }

    .section--page {
        padding-top: 1em; /* Reduce padding on mobile */
        padding-bottom: 1em;
    }

    .card--workhistory {
        border-left: none; /* Remove left border on mobile */
        padding-left: 0; /* Remove left padding on mobile */
    }
}
```

> **Media Queries**
> A CSS feature that allows conditional application of styles based on media type and media features, such as screen width, height, and orientation. It is crucial for creating responsive web designs.

*   `@media (max-width: 600px) { ... }`:  Applies the enclosed styles only when the screen width is 600 pixels or less.
    *   `#wrapper--hero { ... }`: Adjustments for the hero section on smaller screens.
        *   `flex-direction: column;`: Changes the flex direction to column, stacking the image and text vertically instead of horizontally.
        *   `gap: 1em;`: Reduces the gap between flex items to 1em.
    *   `#profile--pic { ... }`: Adjustments for the profile picture on smaller screens.
        *   `width: 200px;`: Increases the width of the image to 200 pixels.
        *   `height: 200px;`: Increases the height of the image to 200 pixels.
    *   `.section--page { ... }`: General page section padding adjustments for smaller screens.
        *   `padding-top: 1em;`: Reduces top padding.
        *   `padding-bottom: 1em;`: Reduces bottom padding.
    *   `.card--workhistory { ... }`: Adjustments for work history cards on smaller screens.
        *   `border-left: none;`: Removes the left border.
        *   `padding-left: 0;`: Removes left padding.

These media query adjustments ensure that the digital resume layout adapts gracefully to smaller screens, providing a better viewing experience on mobile devices.

## Creating the Project Details Page (project1.html)

For the "Projects & Accomplishments" section, we linked to a separate page, `project1.html`. Let's create this page to provide more details about a specific project.

Create a new file named `project1.html` in the root directory of your `resume-website` project.

Add the following HTML structure to `project1.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Project Details</title>
    <link rel="stylesheet" href="./styles/main.css">
</head>
<body>
    <div id="container--main">
        <a href="./index.html" style="display:block; text-align:right;">Go Back ⬅</a>

        <h1>Laboratory Management System for Forensics Lab</h1>

        <ul>
            <li><a href="#">Source Code</a></li>
            <li><a href="#">Live Demo</a></li>
        </ul>

        <br>

        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>

        <p>Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>

        <br>

        <ul>
            <li>Key Learnings:
                <ul>
                    <li>Improved workflow efficiency by 40%.</li>
                    <li>Reduced report generation time by 50%.</li>
                    <li>Enhanced data security and compliance.</li>
                </ul>
            </li>
        </ul>
    </div>
</body>
</html>
```

*   `<!DOCTYPE html>`, `<html lang="en">`, `<head>`:  Standard HTML boilerplate, similar to `index.html`.
    *   `<title>Project Details</title>`: Sets the title for the project details page.
    *   `<link rel="stylesheet" href="./styles/main.css">`: Links to the same `main.css` stylesheet to maintain consistent styling.
*   `<body>`: Contains the project details content.
    *   `<div id="container--main">`:  Uses the same main container to center content and control width.
        *   `<a href="./index.html" ...>Go Back ⬅</a>`: A link to navigate back to the main resume page (`index.html`).  `style="display:block; text-align:right;"` is added inline to position the "Go Back" link to the right.
        *   `<h1>Laboratory Management System for Forensics Lab</h1>`:  An `h1` heading for the project title.
        *   `<ul> ... </ul>`: An unordered list to provide links to the source code and live demo (replace `#` with actual URLs).
        *   `<p> ... </p>`: Paragraphs (`<p>`) with placeholder text (Lorem Ipsum) to describe the project in more detail. Replace this with your actual project description.
        *   `<ul> ... </ul>`: A nested unordered list to highlight key learnings or achievements from the project.

Remember to replace the placeholder content (URLs, project description, Lorem Ipsum) with your actual project details.

## Deploying the Digital Resume with GitHub Pages

Finally, let's deploy our digital resume online for free using GitHub Pages. GitHub Pages allows you to host static websites directly from your GitHub repository.

> **GitHub Pages**
> A static site hosting service offered by GitHub that hosts websites directly from a GitHub repository. It's free to use for public repositories and is ideal for hosting personal websites, project documentation, and simple web applications.

**Steps to Deploy:**

1.  **Create a GitHub Repository:** If you haven't already, create a new public repository on GitHub. Name it `resume-website` (or any name you prefer).

2.  **Initialize Git and Commit Files:**
    *   Open a terminal or command prompt and navigate to your `resume-website` project directory.
    *   Initialize a Git repository: `git init`
    *   Add all project files to the repository: `git add .`
    *   Commit the files: `git commit -m "Initial commit"`

> **Git**
> A distributed version control system that tracks changes in source code during software development. It is designed for coordinating work among programmers, but it can be used to track changes in any set of files.

3.  **Connect to Remote Repository:**
    *   Add your GitHub repository as the remote origin: `git remote add origin <repository_url>` (Replace `<repository_url>` with the URL of your GitHub repository).

4.  **Push to GitHub:**
    *   Push your local repository to the remote GitHub repository: `git push -u origin master`

5.  **Enable GitHub Pages:**
    *   Go to your GitHub repository on the GitHub website.
    *   Click on the "Settings" tab.
    *   Scroll down to the "GitHub Pages" section in the left sidebar.
    *   Under "Source," select "Deploy from a branch."
    *   Choose "master" (or your main branch name) as the branch.
    *   Select "root" as the folder.
    *   Click "Save."

6.  **Access Your Live Resume:**
    *   GitHub Pages will provide you with a URL for your live website in the "GitHub Pages" section of your repository settings. It will typically be in the format `https://<your_github_username>.github.io/<repository_name>`.

It might take a few minutes for GitHub Pages to build and deploy your site after enabling it. Once deployed, your digital resume will be live and accessible via the provided URL, ready to be shared with the world.

## Conclusion

Congratulations! You have successfully built and deployed a digital resume using HTML, CSS, and GitHub Pages. This project has covered essential web development concepts and provided a practical way to create an engaging and shareable online resume.

By understanding HTML structure, CSS styling, and deployment with GitHub Pages, you have gained valuable skills that can be applied to various web development projects. You can further enhance this digital resume by adding more sections, features like a theme switcher, and deeper project details on individual pages. Remember to keep your digital resume updated and share your live URL to showcase your professional profile online.
