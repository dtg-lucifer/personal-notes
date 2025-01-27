---
tags:
  - auth
  - backend
  - frontend
  - html
  - javascript
  - deployment
  - canvas
  - rich-text-editor
  - drawing
  - "#project"
  - career
Repository Link: https://github.com/dtg-lucifer/snappy-notes
share_link: https://share.note.sx/f6ox8dr5#G5yYDVK6JSGpi+mJQLC5vSqy2QKSdRCp7QE+uD+jNeY
share_updated: 2024-06-30T13:44:43+05:30
---
# Objective:

The main objective of creating such app is to have both the benefits of the note taking apps available on the market such as ***OneNote***, ***Obsidian***, ***Excallidraw***. Where the rich text editor like apps such as the ***Obsidian*** is based on the Markdown language for taking the notes on itself, on the other hand ***OneNote*** is based on pure rich text editing provided by Microsoft itself but the drawing and sketching performance of both apps is not as good as the ***Excallidraw***. But also ***Excallidraw*** can't handle the notebook management as like the other two apps can do. So keeping all of those benefits in a single place is the basic objective of this project.

We want to give the app the look of an actual hand written note base like the ***Excallidraw*** provides out of the box on their #ui, shown below:

![[Pasted image 20240628113628.png]]

---
## Why do we need to create this type of project ?

- As we all know that we developers have to keep learning new things more more and day by day as there are new technologies coming everyday in the industry and keeping up to the new knowledge everyday is kind of scary for every one of us as we have to memorize some of the things.
- And taking notes is another thing. Because research shows that only just learning things and noting down everything is lot more helpful than trying to only memorizing everything.
- Any note taking app which is currently available in the market has their own PROS and CONS, such as some app have a better writing experience where as some other have better sketching experience which helps visualizing things better.
>***So keeping all of above mentioned features into a well packed app is the main goal of this project***

---
## Key features

- This project should contain a well defined and simple #ui 
- It will also have the feature of ==creating ***Notebooks*** and each of those will have multiple ***Notes*** and which will have a simple page consisting of a **Text area** and a **Sketching area**==.
- It should have a feature of seamlessly export the **Markdown** part or the written part of the note itself as a ***PDF*** and the **Sketch** part should have export as a ***PNG*** file and to be attached to the original ***PDF***
- The #ui must not have a very complex type of design 
- We should be able to share notes across other users
- Users should be able to note down in a single note which will be provided to them at the on boarding page without authenticating, so that the single note work could be saved inside the local store so that the next time the user comes in all of their work could be saved.
- But for multiple notes saving and sharing he has to authenticate himself.
- The rich text editor should look like ***One Note***
- The ***Sketch*** section should have a ==**Laser pointer type tool which will be used in presentation mode**==
- Every user should be able to attach their own sketches to the text area whenever and wherever they want.
- Each user should get a space to hold their own written notes inside the name of their username as the href of the slug as `/notes/user_name/{slug}`