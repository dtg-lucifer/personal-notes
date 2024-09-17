---
tags:
  - frontend
  - javascript
  - typescript
  - programming
---
# Type guards
Type guards are special type of functions which essentially checks and tells that whether the passes object is of which type which is marked with `unknown`

```ts
type Species = "cat" | "dog";

interface Pet {
  species: Species;
}

class Cat implements Pet {
  public species: Species = "cat";
  public meow(): void {
    console.log("Meow");
  }

  public jump(): void {
    console.log("Jumping...");
  }

  public walk(): void {
    console.log("Walking...");
  }
}

function petIsCat(pet: Pet): pet is Cat {
  return pet.species === "cat";
}

function petIsCatBoolean(pet: Pet): boolean {
  return pet.species === "cat";
}

const p: Pet = new Cat();

//Bad ❌
// p.meow(); // ERROR: Property 'meow' does not exist on type 'Pet'.

if (petIsCatBoolean(p)) {
  // p.meow(); // ERROR: Property 'meow' does not exist on type 'Pet'.

  (p as Cat).meow();

  //What if we have many properties? Do you wanna repeat the same casting
  //Over and over again...
}

//Good ✅
if (petIsCat(p)) {
  p.meow(); // now compiler knows for sure that the variable is of type Cat and it has meow method
}
```


# Satisfies
It allows wherer some expression matchess some type, but also want to keep the most specific type of that expression for interference purposes.

```ts
//Custom interface for rendering images
interface ICustomImage {
  data: string;
  width: number;
  height: number;
}

//Sample of a Custom Image
const myCustomImage: ICustomImage = {
  data: "base64",
  width: 200,
  height: 150,
};

//Image type for the user
type UserImage = string | ICustomImage; // this will tell the ide to take the methods which are common in both the type 'string' and ICustomImage. But if we use the datisfies keyword for the type inference then the type safety is being permanently ensured by the ide

//User interface
interface IUser {
  id: number;
  firstName: string;
  lastName: string;
  image: UserImage;
}

//Bad ❌
const badUser: IUser = {
  id: 1,
  firstName: "Alex",
  lastName: "Brooks",
  image: "image-url",
};

//Good ✅
const goodUser = {
  id: 1,
  firstName: "Alex",
  lastName: "Brooks",
  image: myCustomImage,
} satisfies IUser;
```


# Read only type converter

For the purpose of protecting the object values to be overriden we can either write `readonly` to each of type and create another type without the `readonly` for having the same type which we can or want to override in future. 

**OR**

We can create a helper utility type which will convert the specific types to readonly types as we need those

```ts
type ReadonlyProps<T> = {
	readonly [P in keyof T]: T[P];
}

interface Props {
	title: string;
	content: string;
}

type ReadOnlyPageProps = ReadonlyProps<Props>;
```

---

![[TypeScript Types.png]]

![[TypeScript Classes.png]]

![[TypeScript Control Flow Analysis.png]]

![[TypeScript Interfaces.png]]