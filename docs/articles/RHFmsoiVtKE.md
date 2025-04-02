---
layout: "../../layouts/BlogPost.astro"
title: "Authentication and User Management in Web Applications: A Comprehensive Guide Using Clerk"
description: ""
pubDate: "2025-02-28"
youtubeVideoID: "RHFmsoiVtKE"
channel: ""
index: 34
---

# Authentication and User Management in Web Applications: A Comprehensive Guide Using Clerk

> 



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/RHFmsoiVtKE" frameborder="0" allowfullscreen></iframe>

## Introduction: The Necessity and Challenges of Authentication

Building web applications today invariably involves tackling the critical aspect of **authentication** and **user management**.  This process, while essential for security and personalization, is often cited as one of the most complex aspects of web development.

> **Authentication:** The process of verifying the identity of a user or device. It ensures that users are who they claim to be, granting access to resources and functionalities based on their verified identity.

Traditionally, developers have had to implement authentication systems from scratch, often relying on methods like **JSON Web Tokens (JWT)** or **OAuth**.

> **JSON Web Tokens (JWT):**  A standard for creating access tokens that assert claims. They are commonly used for authentication and authorization in web APIs and applications. JWTs are self-contained and securely transmit information as a JSON object.

> **OAuth:** An open standard authorization protocol and framework that allows a user to grant a third-party application limited access to their resources on an HTTP service, without sharing their credentials. It is often used for "Sign in with Google," "Sign in with Facebook," etc.

While these methods offer control and flexibility, they can be time-consuming and require significant expertise to implement securely and effectively.  Furthermore, managing user accounts, profiles, and security features adds another layer of complexity.

## Introducing Clerk: Simplifying Authentication and User Management

This chapter introduces **Clerk**, a powerful tool designed to streamline and simplify authentication and user management, particularly within **React** projects.

> **React:** A JavaScript library for building user interfaces or UI components. It allows developers to create reusable UI components and manage the state of these components efficiently, making it popular for building interactive web applications.

Clerk offers a comprehensive suite of features that significantly reduce the development effort associated with authentication, allowing developers to focus on building core application functionalities.  It is compatible with various React-based frameworks, including **Single Page Applications (SPAs)**, **Next.js**, and **Remix**.

> **Single Page Applications (SPAs):** Web applications that load a single HTML page and dynamically update the page content as the user interacts with the application, without requiring full page reloads. This provides a more fluid and responsive user experience.

> **Next.js:** A popular React framework for building server-rendered and statically generated web applications. It provides features like routing, API routes, and optimized performance, making it a robust choice for production-ready applications.

> **Remix:** Another full-stack web framework built on React that emphasizes web fundamentals and a focus on user experience. It is known for its data loading and mutation capabilities, aiming for fast and resilient web applications.

This chapter will focus on using Clerk with Next.js to demonstrate its capabilities in a practical project.

### Key Features of Clerk:

*   **Simplified Implementation:** Clerk offers an intuitive and easy-to-integrate solution for adding full authentication to your React projects.
*   **Comprehensive User Management:** Provides a complete user management system, including user registration, login, profile management, and administrative controls.
*   **Pre-built UI Components:** Offers ready-to-use UI components for common authentication flows like sign-in and sign-up forms, accelerating development.
*   **Customization Options:** Allows customization of UI elements and authentication flows for a tailored user experience.
*   **Multiple Authentication Methods:** Supports a wide range of authentication providers, including email/password, social logins (Google, GitHub, and many more), phone numbers, and usernames.
*   **Security Features:** Incorporates built-in security features, reducing the burden of implementing security measures from scratch.
*   **Free Tier Availability:** Offers a free tier, making it accessible for learning and development purposes.

## Project Demo: A Next.js Application with Clerk Authentication

Before diving into implementation, let's examine a demo application built with Next.js and Clerk to illustrate the functionalities we will be creating.

The demo application showcases:

*   **Sign-in and Sign-up Pages:**  Dedicated pages for user registration and login, seamlessly integrated into the application.
*   **Social Login Options:**  Integration with providers like GitHub and Google, allowing users to authenticate using their existing accounts.
*   **Email/Password Registration:**  Standard email and password-based registration flow, including email verification.
*   **User Profile Page:** A dedicated page for users to manage their account details, connected accounts, and profile information.
*   **Admin User Management System:**  A backend interface within Clerk's platform for administrators to manage users, authentication settings, and application configurations.
*   **Customizable UI:** Demonstrates both pre-defined UI components provided by Clerk and the ability to create completely custom UI for authentication flows.

### Authentication Flow Demonstration:

1.  **Sign-up Process:** Users can choose to sign up using various methods:
    *   **Social Logins (GitHub, Google):**  Utilizing pre-built forms from the Clerk package, users can authenticate via their social accounts.
    *   **Email and Password:** Users can register using an email address and password.  Clerk handles email verification by sending a verification code to the provided email.
    *   **Customizable Forms:**  For more control, developers can create custom sign-up forms using Clerk's tools, maintaining the same authentication flow but with a unique UI.

2.  **Sign-in Process:**  Similar to sign-up, users can sign in using their chosen method. Pre-built forms or custom UI can be employed.

3.  **User Account Management:** Upon successful login, users gain access to:
    *   **Manage Account Modal:**  A modal provided by Clerk allows users to:
        *   Add or change email addresses.
        *   Connect additional social accounts.
        *   Delete their account.
        *   Manage password settings.
    *   **Profile Page:**  A dedicated page displaying user profile information, which can be embedded into the application using Clerk's components.

4.  **Clerk Dashboard (Admin Side):**  Logging into the Clerk platform (clerk.com) provides administrators with:
    *   **User Management Interface:**  A comprehensive system to view and manage registered users.
    *   **User Profiles:** Detailed profiles for each user, including their authentication methods and activities.
    *   **Authentication Settings:** Configuration options for authentication methods, verification processes (email links, SMS), and user data collection (first name, last name).
    *   **Integration Options:** Settings for integrating Clerk with other services and platforms.

## Setting up a Next.js Project with Clerk

Let's now move on to the practical implementation of Clerk authentication within a Next.js project.

### 1. Creating a New Next.js Project

Begin by creating a new Next.js project using the `create-next-app` command. Open your terminal and navigate to your desired project directory. Run the following command:

```bash
npx create-next-app@latest clerk-app
```

Follow the prompts and choose the default options for a basic Next.js setup. Ensure you select "App Router" as the routing system.

### 2. Project Setup and Cleanup

Once the project is created, navigate into the project directory:

```bash
cd clerk-app
```

Open the project in your preferred code editor (e.g., VS Code).

*   **Rename Page Extensions (Optional):**  For consistency, you can rename the default `page.js` and `layout.js` files in the `app` directory to `page.jsx` and `layout.jsx` respectively. This is a matter of preference and does not affect functionality.

*   **Clean up `page.jsx`:**  Open `app/page.jsx` and remove the boilerplate code within the `return` statement. Replace it with a basic structure to display a "Home" heading:

    ```jsx
    export default function Home() {
      return (
        <>
          <h1>Home</h1>
        </>
      );
    }
    ```

*   **Clean up `globals.css`:** Open `app/globals.css` and remove the default styles, leaving only the Tailwind CSS directives:

    ```css
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
    ```

### 3. Running the Development Server

Start the Next.js development server to ensure the basic project is running correctly:

```bash
npm run dev
```

Open your browser and navigate to `http://localhost:3000`. You should see a simple page displaying "Home."

### 4. Installing the Clerk Package

Open a new terminal in your project directory and install the Clerk Next.js package:

```bash
npm install @clerk/nextjs
```

This command adds the necessary Clerk library to your project.

### 5. Setting up a Clerk Application and Obtaining API Keys

1.  **Go to Clerk Website:** Navigate to [clerk.com](https://clerk.com) and sign up or log in.
2.  **Create a New Application:** Click on "Add application" or a similar button to create a new Clerk application.
3.  **Application Name:** Provide a name for your application (e.g., "Clerk YouTube App").
4.  **Authentication Methods:** Choose the authentication methods you want to enable for your application (e.g., Email address, Google, GitHub). You can select from a wide range of providers.
5.  **Create Application:** Click "Create application."
6.  **Obtain API Keys:** After creating the application, Clerk will display your **API keys**. These keys are crucial for connecting your Next.js application to your Clerk backend. **Copy these keys.**

### 6. Configuring Environment Variables

1.  **Create `.env.local` File:** In the root directory of your Next.js project, create a new file named `.env.local`.
2.  **Paste API Keys:** Paste the API keys you copied from Clerk into the `.env.local` file. They should look similar to this:

    ```
    NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_publishable_key_here
    CLERK_SECRET_KEY=your_secret_key_here
    ```

    > **API Keys:**  Codes used to authenticate and authorize access to an Application Programming Interface (API). In the context of Clerk, API keys are used to connect your frontend application with Clerk's backend services, enabling authentication and user management features.

    **Note:**  While the transcript mentions only copying two keys, Clerk might provide more depending on the setup. Ensure you copy all relevant keys provided by Clerk and prefix the publishable key with `NEXT_PUBLIC_`.

3.  **Clerk Provider in `layout.jsx`:** Open `app/layout.jsx`. Import the `ClerkProvider` component from `@clerk/nextjs` at the top of the file:

    ```jsx
    import { ClerkProvider } from '@clerk/nextjs';
    ```

    Wrap the `children` prop within the `body` tag with the `ClerkProvider`:

    ```jsx
    import { ClerkProvider } from '@clerk/nextjs';
    import './globals.css'

    export const metadata = {
      title: 'Create Next App',
      description: 'Generated by create next app',
    }

    export default function RootLayout({ children }) {
      return (
        <ClerkProvider>
          <html lang="en">
            <body>{children}</body>
          </html>
        </ClerkProvider>
      )
    }
    ```

    The `ClerkProvider` makes Clerk's authentication context available throughout your application.

### 7. Basic Styling with Tailwind CSS (Optional)

The transcript utilizes Tailwind CSS for styling. You can add basic container styling to your `layout.jsx` to center content on the page.

1.  **Modify `body` in `layout.jsx`:**  Update the `body` tag in `app/layout.jsx` to include Tailwind CSS classes for centering content:

    ```jsx
    <body>
      <main className="container mx-auto flex items-start justify-center min-h-screen">
        <div className="mt-20">
          {children}
        </div>
      </main>
    </body>
    ```

    This adds a container, centers content horizontally and vertically, and adds top margin.

2.  **Tailwind Configuration (Optional Centering):** To automatically center containers without explicitly adding `mx-auto` each time, you can modify your `tailwind.config.js` file. Inside the `theme` object, within `extend`, add the container configuration:

    ```javascript
    /** @type {import('tailwindcss').Config} */
    module.exports = {
      content: [
        './src/pages/**/*.{js,ts,jsx,tsx,mdx}',
        './src/components/**/*.{js,ts,jsx,tsx,mdx}',
        './src/app/**/*.{js,ts,jsx,tsx,mdx}',
      ],
      theme: {
        extend: {
          container: {
            center: true,
          },
        },
      },
      plugins: [],
    }
    ```

    This configuration ensures that any element with the `container` class will be automatically centered.

## Creating UI Components: Header and Navigation

To enhance the user interface, let's create a header component with navigation links.

### 1. Create `components` Folder and `Header.jsx`

In the `app` directory, create a new folder named `components`. Inside the `components` folder, create a new file named `Header.jsx`.

### 2. Header Component Code

Add the following code to `Header.jsx`:

```jsx
import Link from 'next/link';
import { auth, UserButton } from '@clerk/nextjs';

const Header = () => {
  const { userId } = auth();

  return (
    <nav className="bg-blue-700 py-4 px-6 flex items-center justify-between mb-5">
      <div className="flex items-center">
        <Link href="/" className="text-lg uppercase font-bold text-white">
          Clerk App
        </Link>
      </div>
      <div className="flex items-center text-white">
        {!userId ? (
          <>
            <Link href="/sign-in" className="text-gray-300 hover:text-white mr-4">
              Sign In
            </Link>
            <Link href="/sign-up" className="text-gray-300 hover:text-white">
              Sign Up
            </Link>
          </>
        ) : (
          <>
            <Link href="/profile" className="text-gray-300 hover:text-white mr-4">
              Profile
            </Link>
            <UserButton afterSignOutUrl="/" />
          </>
        )}
      </div>
    </nav>
  );
};

export default Header;
```

**Explanation:**

*   **Imports:** Imports `Link` from `next/link` for navigation and `auth` and `UserButton` from `@clerk/nextjs` for authentication state and user button component.
*   **`auth()` Hook:**  The `auth()` hook from Clerk is used to retrieve the current user's authentication state. `userId` is destructured from the return value.
*   **Conditional Rendering:**
    *   `!userId`: If `userId` is not present (user is not logged in), it renders "Sign In" and "Sign Up" links.
    *   `userId`: If `userId` is present (user is logged in), it renders a "Profile" link and the `UserButton` component.
*   **`UserButton` Component:**  This component, provided by Clerk, displays the user's avatar (if available) and a dropdown menu with options like "Manage Account" (profile settings) and "Sign Out." The `afterSignOutUrl` prop specifies the URL to redirect to after sign-out (in this case, the home page "/").
*   **Styling:** Tailwind CSS classes are used for basic styling of the header and links.

### 3. Integrate Header into `layout.jsx`

Open `app/layout.jsx` and import the `Header` component:

```jsx
import Header from './components/Header'; // Adjust path if needed
// ... other imports
```

Place the `<Header />` component within the `body` tag, before the `main` tag:

```jsx
<body>
  <Header />
  <main className="...">
    {children}
  </main>
</body>
```

Now, when you run your application, you should see a header with "Clerk App" logo and "Sign In" and "Sign Up" links (when logged out) or "Profile" and user avatar (when logged in).

## Protecting Pages with Middleware

To secure specific pages and require authentication to access them, Clerk utilizes **middleware**.

> **Middleware:** Functions that execute before a request reaches your application's routes or handlers. In the context of web applications, middleware is commonly used for tasks like authentication, authorization, logging, and request modification.

### 1. Create `middleware.js` File

In the root directory of your project (the same level as `app` and `pages` if you have one), create a file named `middleware.js`.

### 2. Middleware Configuration

Add the following code to `middleware.js`:

```javascript
import { authMiddleware } from '@clerk/nextjs';

export default authMiddleware({
  publicRoutes: ['/', '/sign-in(.*)', '/sign-up(.*)', '/register'], // Add '/register' here
});

export const config = {
  matcher: ['/((?!.*\\..*|_next).*)', '/', '/(api|trpc)(.*)'],
};
```

**Explanation:**

*   **`authMiddleware`:** This function from `@clerk/nextjs` is the core of Clerk's middleware.
*   **`publicRoutes` Option:**  This array defines routes that should be publicly accessible, even without authentication.
    *   `'/'`:  The home page is set as public.
    *   `'/sign-in(.*)'`, `'/sign-up(.*)'`:  These use regular expressions to match any route starting with `/sign-in` or `/sign-up`, including catch-all routes we'll create later.
    *   `'/register'`:  We add `/register` to make our custom registration page public.
*   **`matcher` Config:**  This configuration specifies which paths should be processed by the middleware. The provided matcher is a common pattern in Next.js to apply middleware to all routes except static files and Next.js internal routes.

**Functionality:** With this middleware, any route *not* listed in `publicRoutes` will be protected. If an unauthenticated user tries to access a protected route, they will be redirected to the sign-in page.

### 3. Customizing Sign-in and Sign-up URLs (Environment Variables)

By default, Clerk redirects to its hosted sign-in and sign-up pages. To use custom pages within your application, configure environment variables.

1.  **Create `.env` File:** In the root directory (alongside `.env.local`), create a new file named `.env`.
2.  **Add Clerk URL Variables:** Add the following environment variables to `.env`:

    ```
    NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
    NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up
    NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL=/dashboard
    NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL=/dashboard
    ```

    > **Environment Variables:**  Variables set outside the application code to configure its behavior in different environments (development, production, etc.). They are commonly used to store sensitive information like API keys or configuration settings. In Next.js, environment variables prefixed with `NEXT_PUBLIC_` are accessible in the browser.

    **Explanation:**

    *   `NEXT_PUBLIC_CLERK_SIGN_IN_URL`:  Sets the URL for your custom sign-in page (`/sign-in`).
    *   `NEXT_PUBLIC_CLERK_SIGN_UP_URL`: Sets the URL for your custom sign-up page (`/sign-up`).
    *   `NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL`:  Specifies the URL to redirect users to after successful sign-in (`/dashboard`).
    *   `NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL`: Specifies the URL to redirect users to after successful sign-up (`/dashboard`).

## Creating Sign-in and Sign-up Pages

Now, let's create the sign-in and sign-up pages within your Next.js application. We'll use Clerk's pre-built components initially for ease of setup.

### 1. Create `sign-in` and `sign-up` Folders with Catch-all Routes

In the `app` directory, create two folders:

*   `sign-in`
*   `sign-up`

Inside each of these folders, create another folder using bracket notation for a **catch-all route**:

*   `sign-in/[[...sign-in]]`
*   `sign-up/[[...sign-up]]`

> **Catch-all Routes:**  A Next.js routing feature that allows a single route segment to match multiple path segments. Using `[[...routeName]]` creates an optional catch-all route, meaning it will match both `/routeName` and any paths under it (e.g., `/routeName/something`).

Inside each catch-all route folder, create a `page.jsx` file.

### 2. Sign-in Page Code (`app/sign-in/[[...sign-in]]/page.jsx`)

```jsx
'use client';
import { SignIn } from "@clerk/nextjs";

const SignInPage = () => {
  return (
    <div>
      <SignIn />
    </div>
  );
};

export default SignInPage;
```

### 3. Sign-up Page Code (`app/sign-up/[[...sign-up]]/page.jsx`)

```jsx
'use client';
import { SignUp } from "@clerk/nextjs";

const SignUpPage = () => {
  return (
    <div>
      <SignUp />
    </div>
  );
};

export default SignUpPage;
```

**Explanation:**

*   **`'use client'` Directive:**  This directive at the top of the file marks these components as **client-side components**.

    > **Client-side Component:** In React and Next.js, components that are rendered in the user's browser (client-side) rather than on the server. Client-side components are necessary for using React hooks like `useState`, `useEffect`, and for handling browser-specific interactions.

*   **Import `SignIn` and `SignUp`:** Imports the `SignIn` and `SignUp` components from `@clerk/nextjs`. These are pre-built UI components provided by Clerk.
*   **Component Rendering:**  Each page simply renders the respective `SignIn` or `SignUp` component.

Now, when you navigate to `/sign-in` or `/sign-up`, you should see Clerk's pre-built sign-in and sign-up forms, respectively, integrated into your application's layout.

## Creating a Protected Dashboard Page

Let's create a dashboard page that is protected by authentication, meaning only logged-in users can access it.

### 1. Create `dashboard` Folder and `page.jsx`

In the `app` directory, create a folder named `dashboard`. Inside the `dashboard` folder, create a file named `page.jsx`.

### 2. Dashboard Page Code (`app/dashboard/page.jsx`)

```jsx
const DashboardPage = () => {
  return (
    <div>
      <h1 className="text-2xl font-bold mb-5">Dashboard</h1>
      <p className="mb-5">Welcome to the dashboard!</p>
    </div>
  );
};

export default DashboardPage;
```

This is a simple dashboard page with a heading and welcome message.

**Functionality:**  Because `/dashboard` is not listed in `publicRoutes` in `middleware.js`, it is automatically protected. If you try to access `/dashboard` without being logged in, you will be redirected to the sign-in page. After successful sign-in, you will be redirected to `/dashboard` as configured in the `.env` file (`NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL`).

## Creating a User Profile Page

Let's create a user profile page to display user account information.

### 1. Create `profile` Folder and `page.jsx`

In the `app` directory, create a folder named `profile`. Inside the `profile` folder, create a file named `page.jsx`.

### 2. Profile Page Code (`app/profile/page.jsx`)

```jsx
'use client';
import { UserProfile } from "@clerk/nextjs";

const ProfilePage = () => {
  return (
    <div>
      <UserProfile />
    </div>
  );
};

export default ProfilePage;
```

**Explanation:**

*   **`'use client'` Directive:**  Marks this component as client-side.
*   **Import `UserProfile`:** Imports the `UserProfile` component from `@clerk/nextjs`.
*   **Component Rendering:** Renders the `UserProfile` component. This component displays a user interface for managing user account information, similar to the "Manage Account" modal accessible from the `UserButton`.

Now, a "Profile" link is available in the header when logged in, leading to `/profile` where the `UserProfile` component is rendered.

## Customizing Themes

Clerk allows customization of the visual appearance of its pre-built components through **themes**.

> **Themes:**  Sets of styles and configurations that define the visual appearance of UI components. Themes allow developers to easily change the look and feel of their application without modifying individual component styles directly.

### 1. Install `@clerk/themes` Package

Open a terminal and install the `@clerk/themes` package:

```bash
npm install @clerk/themes
```

### 2. Apply a Theme in `layout.jsx`

1.  **Import `darkTheme` (or `lightTheme`, `baseTheme`):** In `app/layout.jsx`, import a theme from `@clerk/themes`. For example, to use a dark theme:

    ```jsx
    import { ClerkProvider } from '@clerk/nextjs';
    import { darkTheme } from '@clerk/themes'; // Import darkTheme
    // ... rest of imports
    ```

2.  **Add `appearance` Prop to `ClerkProvider`:**  Add the `appearance` prop to the `ClerkProvider` in `layout.jsx` and set the `baseTheme` option to the imported theme:

    ```jsx
    <ClerkProvider appearance={{ baseTheme: darkTheme }}> {/* Apply darkTheme */}
      <html lang="en">
        <body>{children}</body>
      </html>
    </ClerkProvider>
    ```

    You can replace `darkTheme` with `lightTheme` (for a light theme) or `baseTheme` (for the default theme) or explore creating custom themes as documented by Clerk.

## Creating a Custom Registration Form

For more UI control and customization, you can build completely custom sign-up and sign-in forms using Clerk's hooks and APIs. Let's create a custom registration (sign-up) form as an example.

### 1. Create `register` Folder and `page.jsx`

In the `app` directory, create a folder named `register`. Inside the `register` folder, create a file named `page.jsx`.

### 2. Custom Register Page Code (`app/register/page.jsx`)

```jsx
'use client';
import { useState } from 'react';
import { useSignUp } from '@clerk/nextjs';
import { useRouter } from 'next/navigation';

const RegisterPage = () => {
  const [firstName, setFirstName] = useState('');
  const [lastName, setLastName] = useState('');
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [code, setCode] = useState('');
  const [pendingVerification, setPendingVerification] = useState(false);

  const { isLoaded, signUp, setActive } = useSignUp();
  const router = useRouter();

  const handleSubmit = async (e) => {
    e.preventDefault();

    if (!isLoaded) {
      return;
    }

    try {
      await signUp.create({
        first_name: firstName,
        last_name: lastName,
        email_address: email,
        password: password,
      });

      await signUp.prepareEmailAddressVerification({ strategy: 'email_code' });
      setPendingVerification(true);

    } catch (error) {
      console.error(error);
    }
  };

  const onPressVerify = async () => {
    if (!isLoaded) {
      return;
    }

    try {
      const completeSignUp = await signUp.attemptEmailAddressVerification({
        code,
      });

      if (completeSignUp.status !== 'complete') {
        // Investigate the response for more details.
        console.error("Sign up not complete", completeSignUp);
        return;
      }

      await setActive({ session: completeSignUp.createdSessionId });
      router.push('/'); // Redirect to home page after successful registration
    } catch (error) {
      console.error('Verification error:', error);
    }
  };


  return (
    <div className="border p-5 rounded" style={{ width: '500px' }}>
      <h1 className="text-2xl font-bold mb-4">Register</h1>
      {!pendingVerification ? (
        <form onSubmit={handleSubmit}>
          <div>
            <label htmlFor="firstName">First Name:</label>
            <input
              type="text"
              id="firstName"
              className="border rounded p-2 block w-full mb-3"
              value={firstName}
              onChange={(e) => setFirstName(e.target.value)}
            />
          </div>
          <div>
            <label htmlFor="lastName">Last Name:</label>
            <input
              type="text"
              id="lastName"
              className="border rounded p-2 block w-full mb-3"
              value={lastName}
              onChange={(e) => setLastName(e.target.value)}
            />
          </div>
          <div>
            <label htmlFor="email">Email Address:</label>
            <input
              type="email"
              id="email"
              className="border rounded p-2 block w-full mb-3"
              value={email}
              onChange={(e) => setEmail(e.target.value)}
            />
          </div>
          <div>
            <label htmlFor="password">Password:</label>
            <input
              type="password"
              id="password"
              className="border rounded p-2 block w-full mb-3"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
            />
          </div>
          <button type="submit" className="bg-blue-500 text-white py-2 px-4 rounded hover:bg-blue-600">
            Create Account
          </button>
        </form>
      ) : (
        <div>
          <p className="mb-4">Verification code sent to your email.</p>
          <form onSubmit={onPressVerify}>
            <div>
              <label htmlFor="code">Verification Code:</label>
              <input
                type="text"
                id="code"
                className="border rounded p-2 block w-full mb-3"
                value={code}
                onChange={(e) => setCode(e.target.value)}
              />
            </div>
            <button type="submit" className="bg-green-500 text-white py-2 px-4 rounded hover:bg-green-600">
              Verify Email
            </button>
          </form>
        </div>
      )}
    </div>
  );
};

export default RegisterPage;
```

**Explanation:**

*   **`'use client'` Directive:**  Marks this as a client-side component to use React hooks.
*   **Imports:**
    *   `useState`:  From React for managing component state (form input values, verification state).
    *   `useSignUp`: From `@clerk/nextjs` to access Clerk's sign-up functionality.
    *   `useRouter`: From `next/navigation` for client-side routing (redirecting after successful registration).

    > **Hooks:** Special functions in React that let you "hook into" React state and lifecycle features from within functional components. Hooks were introduced to make state and other React features accessible in functional components, simplifying component logic. `useState` is a hook for managing state, `useSignUp` is a custom hook provided by Clerk, and `useRouter` is a hook from Next.js for navigation.

*   **State Variables:**
    *   `firstName`, `lastName`, `email`, `password`:  State variables to store form input values.
    *   `code`:  State variable to store the email verification code entered by the user.
    *   `pendingVerification`:  Boolean state to control conditional rendering of the form (either registration form or verification code form).
*   **`useSignUp` Hook:**
    *   `isLoaded`:  Indicates if the `signUp` object is loaded and ready to use.
    *   `signUp`:  Object containing methods for sign-up actions (e.g., `create`, `prepareEmailAddressVerification`, `attemptEmailAddressVerification`).
    *   `setActive`:  Function to set the user session as active after successful verification.
*   **`useRouter` Hook:**  Used for redirecting the user after successful registration.
*   **`handleSubmit` Function:**
    *   Called when the registration form is submitted.
    *   Prevents default form submission behavior.
    *   Checks if `isLoaded` is true.
    *   Calls `signUp.create()` to create a new user with provided details.
    *   Calls `signUp.prepareEmailAddressVerification()` to send the email verification code.
    *   Sets `pendingVerification` to `true` to switch to the verification code form.
    *   Handles potential errors with `try...catch`.
*   **`onPressVerify` Function:**
    *   Called when the verification code form is submitted.
    *   Prevents default form submission.
    *   Checks if `isLoaded` is true.
    *   Calls `signUp.attemptEmailAddressVerification()` to verify the code.
    *   Checks `completeSignUp.status`:
        *   If not `'complete'`, logs an error.
        *   If `'complete'`, calls `setActive()` to activate the user session using `completeSignUp.createdSessionId`.
        *   Redirects to the home page using `router.push('/')`.
    *   Handles potential errors with `try...catch`.
*   **Conditional Rendering in `return`:**
    *   `!pendingVerification`: Renders the initial registration form with fields for first name, last name, email, and password.
    *   `pendingVerification`: Renders the verification code form with a field for entering the verification code.

**Functionality:** This custom registration page implements the same email verification flow as Clerk's pre-built components but with a completely custom UI. You can further customize the styling and form fields as needed.

## Conclusion

This chapter has provided a comprehensive guide to implementing authentication and user management in Next.js applications using Clerk. By leveraging Clerk's pre-built components and hooks, developers can significantly simplify the process of adding robust authentication features to their web applications. Furthermore, the ability to customize UI and authentication flows offers flexibility to tailor the user experience to specific application requirements. Clerk empowers developers to focus on building core application functionalities while ensuring secure and efficient user management.

