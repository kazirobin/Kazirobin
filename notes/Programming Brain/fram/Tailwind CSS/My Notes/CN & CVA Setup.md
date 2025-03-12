# CN & CVA Setup

React and Tailwind CSS are popular technologies used to develop modern web applications. While Tailwind CSS is used as a CSS framework, React is used as a JavaScript library to build user interfaces. By combining these two technologies, you can take advantage of Tailwind’s features to make designing user interfaces easier.

When combining Tailwind and React, you may experience class name collisions. To prevent this, there are several methods for combining class names. One of them is the `clsx` library. The clsx function combines all inputted class names and returns a single string as output.

To combine Tailwind CSS and React class names, you can use a library called `tailwind-merge`. This library provides a `twMerge` function to combine Tailwind class names with other class names.

1. `clsx` can be installed using npm. Open your terminal and run one of the following commands:

```bash
npm install clsx
```

2. `tailwind-merge` can also be installed using npm. Run one of the following commands in your terminal:

```bash
npm install tailwind-merge
```

Once both packages are installed, you can use them in your React project. In the code you provided, `clsx` and `twMerge` are imported from their respective packages using the following lines:

Create a file named **src/lib/utils.ts**

```tsx
import { ClassValue, clsx } from "clsx";
import { twMerge } from "tailwind-merge";

export default function cn(...inputs: ClassValue[]) {
  console.log(inputs);
  return twMerge(clsx(inputs));
}
```

## Class Variance Authority

You may need full control over your StyleSheet output. Your job might require you to use a framework such as Tailwind CSS. You might just prefer writing your own CSS.

Creating variants with the "traditional" CSS approach can become an arduous task; manually matching classes to props and manually adding types.

`cva` aims to take those pain points away, allowing you to focus on the more fun aspects of UI development.

### Installation

Run one of the following commands in your terminal:

```bash
npm i class-variance-authority
```

If you're a Tailwind user, here are some additional (optional) steps to get the most out of cva IntelliSense, You can enable autocompletion inside `cva` using the steps below:

Add the following to your `settings.json` to your VSCode

```json
// Tailwind CSS CVA IntelliSense Config Here
  "tailwindCSS.experimental.classRegex": [
    ["cva\\(([^)]*)\\)", "[\"'`]([^\"'`]*).*?[\"'`]"],
    ["cx\\(([^)]*)\\)", "(?:'|\"|`)([^']*)(?:'|\"|`)"]
  ]
```

### Creating Button Variants

To kick things off, let's build a "basic" `button` component, using `cva` to handle our variant's classes

Create a file named **src/components/ui/Button.tsx**

```tsx
"use client";

import cn from "@/lib/utils";
import { cva } from "class-variance-authority";
import * as React from "react";

function button({ children, className, variant, size, ...props }, ref) {
const buttonVariants = cva(
    "inline-flex items-center justify-center whitespace-nowrap rounded-md text-sm font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50",
    {
      variants: {
        variant: {
          default: "bg-red-500 text-white",
          destructive: "bg-blue-500 text-white hover:bg-blue-600",
          outline: "bg-red-500 text-white hover:bg-red-600",
          secondary: "bg-green-500",
          ghost: "hover:bg-accent hover:text-accent-foreground",
          link: "text-primary underline-offset-4 hover:underline",
        },
        size: {
          default: "h-10 px-4 py-2",
          sm: "h-9 rounded-md px-3",
          lg: "h-11 rounded-md px-8",
          icon: "h-10 w-10",
        },
      },
      defaultVariants: {
        variant: "default",
        size: "default",
      },
    },
  );

  return (
    <button
      className={cn(buttonVariants({ variant, size, className }))}
      ref={ref}
      {...props}>
      {children}
    </button>
  );
}

const Button = React.forwardRef(button);
export default Button;
```