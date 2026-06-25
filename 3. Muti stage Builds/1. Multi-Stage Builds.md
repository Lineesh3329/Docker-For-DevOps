# Multi-Stage Builds

## What is a Multi-Stage Build?

A Multi-Stage Build is a Docker build technique that uses multiple `FROM` instructions within a single Dockerfile. It separates the **build environment** from the **runtime environment**, resulting in smaller, cleaner, and more secure Docker images.

Instead of including build tools and dependencies in the final image, only the necessary application files are copied into the production image.

---

## Why Use Multi-Stage Builds?

- Reduces the final image size
- Removes unnecessary build dependencies
- Improves security by excluding development tools
- Optimizes application performance
- Simplifies Dockerfile management

---

## How It Works

```text
Source Code
      │
      ▼
Build Stage
(Compile / Install Dependencies)
      │
      ▼
Copy Required Files
      │
      ▼
Runtime Stage
      │
      ▼
Lightweight Production Image
```

---

## Example

### Multi-Stage Dockerfile

```dockerfile
# Stage 1 - Build Stage
FROM python:3.12-slim AS builder

WORKDIR /app

COPY . .

RUN pip install --no-cache-dir flask

# Stage 2 - Runtime Stage
FROM python:3.12-alpine

WORKDIR /app

COPY --from=builder /app /app

CMD ["python3", "app.py"]
```
---
## How This Multi-Stage Dockerfile Works Internally

1. Docker starts building the **first stage** using the `python:3.12-slim` image.

2. A working directory (`/app`) is created inside the builder stage.

3. The application source code is copied into the `/app` directory.

4. Docker installs the required dependency (`Flask`) in the builder stage.

5. Once the build stage is complete, Docker starts a **second stage** using the lightweight `python:3.12-alpine` image.

6. The runtime stage starts with a clean environment and does not contain the files or tools from the builder stage.

7. Docker copies only the required application files from the builder stage using:

   ```dockerfile
   COPY --from=builder /app /app
   ```

8. Build tools, temporary files, and unnecessary dependencies from the builder stage are **not copied** to the runtime stage.

9. Docker sets the default command:

   ```dockerfile
   CMD ["python3", "app.py"]
   ```

10. The final Docker image contains only the application, required files, and the lightweight runtime, making it smaller, faster, and more secure.


---

## Single-Stage vs Multi-Stage Build

| Feature | Single-Stage Build | Multi-Stage Build |
|----------|--------------------|-------------------|
| `FROM` Instructions | One | Multiple |
| Build Tools | Included in final image | Excluded from final image |
| Final Image Size | Larger | Smaller |
| Storage Usage | Higher | Lower |
| Security | Lower | Higher |
| Image Transfer | Slower | Faster |
| Build Process | Single stage | Separate build and runtime stages |
| Production Ready | Less optimized | Highly optimized |
| Best Use Case | Development & Testing | Production Deployments |

### Single-Stage Build

```text
                 Docker Image
┌──────────────────────────────────────┐
│ Application                          │
│ Source Code                          │
│ Dependencies                         │
│ Build Tools                          │
│ Compiler                             │
│ Runtime                              │
└──────────────────────────────────────┘

Final Image Size: ~900 MB
```

### Multi-Stage Build

```text
            Stage 1 (Builder)
┌──────────────────────────────────────┐
│ Source Code                          │
│ Dependencies                         │
│ Build Tools                          │
│ Compiler                             │
└──────────────────────────────────────┘
               │
               │ COPY Required Files
               ▼
          Stage 2 (Runtime)
┌──────────────────────────────────────┐
│ Application                          │
│ Runtime                              │
└──────────────────────────────────────┘

Final Image Size: ~120 MB
```

> **Example Image Size**
>
> - **Single-Stage Build:** ~900 MB
> - **Multi-Stage Build:** ~120 MB
---

## Key Points

- Multi-stage builds are a best practice for creating optimized Docker images, regardless of the programming language.
- By separating the build and runtime environments, they eliminate unnecessary files, reduce image size, improve security, and simplify deployments.
- Whether we're developing applications in **Go**, **Java**, **Python**, **Node.js**, or any other language, the core principle remains the same: **build in one stage, run in another**.
- Resulting in lightweight, efficient, and production-ready Docker images.
n.
