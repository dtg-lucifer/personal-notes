---
tags:
  - frontend
  - ui
  - nextjs
  - theme
  - components
  - css
  - tailwindcss
documentation: https://ui.shadcn.com/docs
---
# What is shadcn/ui ??

It is not a typical component library where we just go and install the whole library and which just increases the bundle size of our whole app. Rather it just gives us the only component we need from it and gives us the whole code for the component using the help of **TailwindCSS**

---
# Introduction

Beautifully designed components that you can copy and paste into your apps. Accessible. Customizable. Open Source.
This is **NOT** a component library. It's a collection of re-usable components that you can copy and paste into your apps.

**What do you mean by not a component library?**
> I mean you do not install it as a dependency. It is not available or distributed via npm.
> Pick the components you need. Copy and paste the code into your project and customize to your needs. The code is yours.
> _Use this as a reference to build your own component libraries._

---

# Example

Suppose we want to have a button from shadcn then we have to install the button to our project using their CLI which looks something like this

![[Pasted image 20240701000250.png]]

The button itself is ==**TOTALLY CUSTOMIZABLE**== so we have the full control of the component like this

```tsx
import { Slot } from "@radix-ui/react-slot";
import { cva, type VariantProps } from "class-variance-authority";
import * as React from "react";
import { cn } from "~/lib/utils";

const buttonVariants = cva("inline-flex items-center justify-center whitespace-nowrap rounded-md text-sm font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50",
  {
    variants: {
      variant: {
        default: "bg-primary text-primary-foreground hover:bg-primary/90",
        destructive: "bg-destructive text-destructive-foreground hover:bg-destructive/90",
        outline: "border border-input bg-background hover:bg-accent hover:text-accent-foreground",
        secondary: "bg-secondary text-secondary-foreground hover:bg-secondary/80",
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
  }
);

export interface ButtonProps
  extends React.ButtonHTMLAttributes<HTMLButtonElement>,
    VariantProps<typeof buttonVariants> {
  asChild?: boolean;
}

const Button = React.forwardRef<HTMLButtonElement, ButtonProps>(({ className, variant, size, asChild = false, ...props }, ref) => {

    const Comp = asChild ? Slot : "button";

    return (
      <Comp
        className={cn(buttonVariants({ variant, size, className }))}
        ref={ref}
        {...props}
      />
    );
  }
);

Button.displayName = "Button";

export { Button, buttonVariants };
```

---

# What can be achieved with the help of this library ??

As of my oversee of the library and the capabilities of he library I think we can use multi functional components with the library itself by combining the small components provided by the library.

Such as a full fledged form component which will have all of the available components from the library, i.e **Button, Input, Dropzone, Label, Radiobutton, Checkbox, etc** and many more possibilities.

---

# Best works with Next.js ??

Yes, it is best combined with **Next.js** with the help of **Typescript** & **TailwindCSS**. It has both easy setup and low code base for the full stack framework.

---
