# lab8
Below is a **clean, exact, step-by-step guide for Program-8**
❌ No extra theory
❌ No optional steps skipped
✅ Exactly follows your lab manual and screenshots

---

# ✅ Program-8

## Create Kubernetes Pods using YAML Descriptors

---

## 🔹 Step 0: Prerequisites

Make sure **Minikube** and **kubectl** are running.

```bash
minikube status
```

---

## 📁 Step 1: Create Project Folder

```bash
mkdir Program-8
cd Program-8
```

---

## 🟢 Step 2: Create Node.js App (`server.js`)

```bash
nano server.js
```

**Paste EXACT content:**

```javascript
const http = require("http");
const port = 3000;

const server = http.createServer((req, res) => {
  res.end("Hello from Node.js running inside Kubernetes!");
});

server.listen(port, () => {
  console.log(`Server running at port ${port}`);
});
```

Save → **CTRL + X → Y → Enter**

---

## 🧩 Step 3: Create ConfigMap (`nodejs-configmap.yaml`)

```bash
nano nodejs-configmap.yaml
```

**Paste EXACT content:**

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: nodejs-app-config
data:
  server.js: |
    const http = require("http");
    const port = 3000;

    const server = http.createServer((req, res) => {
      res.end("Hello from Node.js running inside Kubernetes!");
    });

    server.listen(port, () => {
      console.log(`Server running at port ${port}`);
    });
```

Save and exit.

---

## 📦 Step 4: Create Pod YAML (`nodejs-pod.yaml`)

```bash
nano nodejs-pod.yaml
```

**Paste EXACT content:**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: program-8
  labels:
    app: nodejs
spec:
  containers:
    - name: nodejs
      image: node:18
      command: ["node", "/usr/src/app/server.js"]
      volumeMounts:
        - name: app-code
          mountPath: /usr/src/app
      ports:
        - containerPort: 3000
  volumes:
    - name: app-code
      configMap:
        name: nodejs-app-config
```

Save and exit.

---

## 🚀 Step 5: Apply YAML Files

```bash
kubectl apply -f nodejs-configmap.yaml
kubectl apply -f nodejs-pod.yaml
```

---

## 📊 Step 6: Check Pod Status

```bash
kubectl get pods
```

Ensure status is **Running**.

---

## 🌐 Step 7: Access the Node.js App (Port Forwarding)

```bash
kubectl port-forward pod/program-8 3000:3000
```

---

## 🌍 Step 8: Check Output in Browser

Open:

```
http://localhost:3000
```

✅ Output:

```
Hello from Node.js running inside Kubernetes!
```

---

## 🧹 Step 9: Delete All Pods

```bash
kubectl delete pods --all
```

---

## 🧹 Step 10: Delete All Services

```bash
kubectl delete svc --all
```

---

## 🧹 Step 11: Delete All Deployments

```bash
kubectl delete deployments --all
```

---

## 📁 Final Project Structure

```
Program-8/
│
├── server.js
├── nodejs-configmap.yaml
└── nodejs-pod.yaml
```

---
