---
tags:
  - snappy-notes
  - frontend
  - canvas
  - rich-text-editor
  - roughjs
  - css
  - drawing
  - design
share_link: https://share.note.sx/scnfffqs#r0Al3+87s9XWkb5f8wNNHJQZMoPOLcc+JdvwurbkelQ
share_updated: 2024-07-03T12:07:26+05:30
---
# Rich Text Editor Libraries

1. **Tiptap**: A renderless and extendable rich text editor for Vue.js, but it also has a React wrapper. #tiptap #rich-text-editor
   - **Website**: [Tiptap](https://tiptap.dev/)
   - **Features**: Extensible, collaborative editing, and markdown support.
   - **Documentation**: [Starter-kit documentation](https://github.com/ueberdosis/tiptap/blob/develop/docs/api/extensions/starter-kit.md), [Details about each node and extension](https://tiptap.dev/docs/editor/extensions/nodes/)
   - **Example:** [Github Repo](https://github.com/dtg-lucifer/demo-rich-text-editor)
```jsx
"use client";  

import { useEditor, EditorContent } from "@tiptap/react";
import StarterKit from "@tiptap/starter-kit";
import React from "react";

const Tiptap = () => {
  const editor = useEditor({
    extensions: [StarterKit],
    content: "<p>Hello World! 🌎️</p>",
  });

  return (
    <React.Fragment>
      <EditorContent editor={editor} controls={true} />
    </React.Fragment>
  );
};

export default Tiptap;
```

2. **Novel.js**: [Notion-style Rich Text Editor in NextJs - YouTube](https://www.youtube.com/watch?v=hP0TcRcr95Q)
	- Documentation: [Introduction - Novel Docs](https://novel.sh/docs/introduction)
	- Example: [HamedBahram/next-novel (github.com)](https://github.com/HamedBahram/next-novel)

---
# Sketching libraries

**For the hand drawn like feeling of the drawings we make on the canvas** #drawing #canvas #svg #roughjs #excallidraw 
1. **Rough.js**: A react library which is also used by excallidraw
	- **Wiki:** [Rough.js Documentation](https://github.com/rough-stuff/rough/wiki#roughjs-api)
	- **Full code:** [Repo](https://github.com/redhwannacef/youtube-tutorials/tree/main/excalidraw-tutorial)
	- **Playlist**: [Youtube](https://youtube.com/playlist?list=PLSxgVLtIB0IFmQGuVMSE_wDHPW5rq4Ik7&si=OgGB2EujWbn2meW1)
	-  **Example:**
		![[Pasted image 20240628113628.png]]
	- **Code:** 
```js
import rough from 'roughjs';

const rc = rough.canvas(document.getElementById('canvas'));
rc.rectangle(10, 10, 200, 200); // x, y, width, height

rc.circle(50, 50, 80, { fill: 'red' }); // fill with red hachure
rc.rectangle(120, 15, 80, 80, { fill: 'red' });
rc.circle(50, 150, 80, {
	fill: "rgb(10,150,10)",
	fillWeight: 3 // thicker lines for hachure
});
rc.rectangle(220, 15, 80, 80, {  
	fill: 'red',  
	hachureAngle: 60, // angle of hachure,  
	hachureGap: 8
});
rc.rectangle(120, 105, 80, 80, {  
	fill: 'rgba(255,0,200,0.2)',  
	fillStyle: 'solid' // solid fill
});
```
2. **Fonts for the text and symbolic handwriting like feeling:**
	- **Excallidraw+ home page fonts:**
		![[Screenshot 2024-06-29 014402.png]]
	- **Excallidraw's UI fonts:** [Github issue for the reference](https://github.com/excalidraw/excalidraw/issues/2945)
	
---

# Markdown Parsing and Rendering

1. **Remark**: A powerful markdown processor powered by unified.
   - **Website**: [Remark](https://remark.js.org/)
   - **Features**: Plugins for processing markdown, converting markdown to React components.

2. **Markdown-it**: A markdown parser with high speed and flexibility.
   - **Website**: [Markdown-it](https://github.com/markdown-it/markdown-it)
   - **Features**: Plugins, custom syntax, and high performance.

# File System and Storage

1. **File System API**: Use the native file system API to read and write local files.
   - **Website**: [File System API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API)
   - **Features**: Direct access to the user’s file system.

2. **IndexedDB**: A low-level API for client-side storage of significant amounts of structured data.
   - **Website**: [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)
   - **Features**: Efficient storage and retrieval of data.

# State Management

1. **Redux**: A predictable state container for JavaScript apps.
   - **Website**: [Redux](https://redux.js.org/)
   - **Features**: Centralized state management, easy debugging, and tools for development.

2. **Recoil**: A state management library for React developed by Facebook.
   - **Website**: [Recoil](https://recoiljs.org/)
   - **Features**: Fine-grained state updates, easy to use, and interoperable with React.

# Next.js Specific

1. **API Routes**: Utilize Next.js API routes to handle backend logic.
   - **Website**: [API Routes](https://nextjs.org/docs/api-routes/introduction)
   - **Features**: Serverless functions, easy to set up and deploy.

2. **Static Generation and Server-side Rendering**: Use Next.js capabilities for efficient rendering.
   - **Website**: [Next.js Rendering](https://nextjs.org/docs/basic-features/pages#static-generation-recommended)
   - **Features**: Optimized for performance and SEO.

# Collaboration and Real-time Features

1. **Socket.io**: Enables real-time, bidirectional communication.
   - **Website**: [Socket.io](https://socket.io/)
   - **Features**: Real-time data transfer, easy integration with Next.js.

2. **Yjs**: A CRDT (Conflict-free Replicated Data Type) for building collaborative applications.
   - **Website**: [Yjs](https://yjs.dev/)
   - **Features**: Real-time collaboration, offline support, conflict resolution.

# Other Useful Tools

1. **Tailwind CSS**: A utility-first CSS framework for rapid UI development.
   - **Website**: [Tailwind CSS](https://tailwindcss.com/)
   - **Features**: Highly customizable, responsive design, and reusable styles.
   - **Ui libraries**: shadcn/ui - magicui - aceternity ui

2. **Prism.js**: A lightweight, extensible syntax highlighter.
   - **Website**: [Prism.js](https://prismjs.com/)
   - **Features**: Syntax highlighting, plugins, and language support.
   - **Example code:**

```js
const Prism = require('prismjs');

const code = `var data = 1;`;

const html = Prism.highlight(code, Prism.languages.javascript, 'javascript');
```
