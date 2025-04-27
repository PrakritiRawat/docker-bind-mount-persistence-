

# 🚀 docker-bind-mount-persistence 🐳

## 📌 Introduction
This lab demonstrates how to use Docker **bind mounts** with a **Linux container** to achieve **persistent data storage** beyond a container’s lifecycle.  
By mounting a local directory into a container, any data written inside the container stays preserved even after the container is removed — a critical concept for managing containerized applications.

---

## 🔧 Steps & Observations

### 🏗 Step 1: Run a Container with a Bind Mount
Command executed:

```bash
docker run -dit --name alpine_with_bind_mount -v C:\Users\Ryuk\docker_data:/data alpine:latest sh
```

### 🔍 What Happened:
- Since `alpine:latest` was not found locally, Docker pulled it from the official repository.
- A new container named **alpine_with_bind_mount** was created.
- The `-v` flag mounted the local directory `C:\Users\Ryuk\docker_data` to `/data` inside the container.
- The container started a shell (`sh`) in **detached mode**.

---

### 📝 Step 2: Create a File Inside the Bind Mount
Inside the container, you created a file:

```bash
docker exec -it alpine_with_bind_mount sh -c "echo 'Hello, Prakriti!' > /data/testfile.txt"
```

### 🔍 What Happened:
- The command executed a shell inside the running container.
- It created a file `testfile.txt` inside `/data` containing the text **"Hello, Prakriti!"**.
- Since `/data` is a bind-mounted directory, the file was actually stored **on the host machine** in `C:\Users\Ryuk\docker_data`.

---

### ✅ Step 3: Verify the File Exists
Check the file contents:

```bash
docker exec -it alpine_with_bind_mount sh -c "cat /data/testfile.txt"
```

### 📋 Output:
```
Hello, Prakriti!
```
✅ *Confirms that the file was created successfully and accessible inside the container.*

---

### 🗑 Step 4: Remove the First Container
You removed the container:

```bash
docker rm -f alpine_with_bind_mount
```

### 🔍 What Happened:
- The container was **forcefully stopped and deleted**.
- However, since `testfile.txt` was inside the **bind-mounted directory**, the file **remained safely on the host system**.

---

### 🔄 Step 5: Create a New Container with the Same Bind Mount
Start a new container:

```bash
docker run -dit --name new_alpine -v C:\Users\Ryuk\docker_data:/data alpine sh
```

### 🔍 What Happened:
- A new container named **new_alpine** was launched.
- It reused the same bind-mounted directory (`C:\Users\Ryuk\docker_data`) mapped to `/data`.

---

### 🔎 Step 6: Verify Data Persistence
Inside the new container, check if the file still exists:

```bash
docker exec -it new_alpine sh -c "cat /data/testfile.txt"
```

### 📋 Output:
```
Hello, Prakriti!
```
✅ *Confirms that bind mounts enable **data persistence** even after container deletion.*

---

## 🎯 Conclusion
- ✅ **Bind mounts** allow persistent storage that survives container deletion.
- ✅ **Data remains** on the host even if containers are removed.
- ✅ **New containers** can access existing data if they use the same bind mount path.
- ✅ Critical for **persistent volumes**, **data sharing** between containers, and **stateful containerized applications**.

---

## 🚀 Next Steps
- 🛠 Explore **named volumes** (`docker volume create`) for managed persistent storage.
- 🐳 Try **bind mounts with other container images** like MySQL, Nginx, or Redis.
- 🔐 Investigate how **file permissions** behave between the host and container in bind mounts.
- 🔄 Automate mounts using **Docker Compose**.

---

🎨 **Keep exploring, Prakriti!**  
**Understanding Docker storage strategies is essential for scalable cloud-native applications!** 🚀🐳

---
