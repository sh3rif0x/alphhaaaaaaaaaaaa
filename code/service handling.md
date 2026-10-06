Yeah — the thing you're describing is usually called the **architecture** of the project.

More specifically:

- **Project structure** → how files and folders are organized.
    
- **Application architecture** → how different parts of the app are organized and work together.
    
- **Module structure** → how code is split into modules/files and imported/exported.
    
- **Data flow** → how data moves between files/components.
    
- **Routing** → how URLs map to pages/components (e.g. `/services/:id`).
    
- **Dependencies / imports** → how one file communicates with another through `import` / `export`.
    
- **API/data layer** → how code gets data from things like `services.json`, a database, or an API.
    

For what you were describing earlier — **a URL contains a service ID, the app reads that ID, finds the matching service in `services.json`, then displays it** — I'd call that the **application architecture + routing + data flow**.

A simple picture is:

```text
URL
 ↓
Router
 ↓
Service ID
 ↓
services.json
 ↓
Find matching service
 ↓
Service Page
 ↓
Render service data
```

And the overall organization of the folders/files is the **project structure**.